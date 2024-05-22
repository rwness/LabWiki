---
title: "TheNessLab : Intro to Awk"
---

::: {#page}
::: {#main .aui-page-panel}
::: {#main-header}
::: {#breadcrumb-section}
1.  [TheNessLab](index.html)
2.  [The Ness Lab Wiki](The-Ness-Lab-Wiki_11436042.html)
3.  [Coding tips and tutorials](Coding-tips-and-tutorials_11436186.html)
:::

# [ TheNessLab : Intro to Awk ]{#title-text} {#title-heading .pagetitle}
:::

::: {#content .view}
::: page-metadata
Created by [ Jimmy Issa]{.author}, last modified on Dec 23, 2022
:::

::: {#main-content .wiki-content .group}
[Linux comes with useful commands like sort, cut, grep, etc. But the awk
command is a little different. It is not only a command, but is its own
(Turing-complete) programming language. It is mainly intended for
writing one-liner programs, but it is also possible to write complex
programs in awk. (However, if your awk program or script begins getting
too complex or long, it\'s better to switch over to
Python.)]{style="letter-spacing: 0.0px;"}

The awk program is used to enter into a file, parse it line by line, and
perform certain actions depending on what is in the line. You can also
use filtering options to only perform actions on lines that meet
specific conditions. For example, you can perform an action on only the
third line in an entire file, or on every third line. You can perform an
action only on lines that contain a certain keyword. The main components
of the awk program are specifying the pattern you want awk to recognize
and the action you want it to commit upon recognizing the pattern. If a
pattern is specified, the action only happens on lines in a file which
match the pattern. If no pattern is specified, then the action applies
to every line. The basic syntax of using awk is:

awk \'pattern {action}\' file

Notice all action-patterns are enclosed in \' \' single-quotes. Also
notice all actions are enclosed in { } curly braces. You can omit the
pattern to perform an action on all lines:

awk \'{action}\' file

Or you can omit the action, leave only a pattern, and lines matching
that pattern will appear:

awk \'pattern\' file

You can have as many blocks of actions as you want. Furthermore, you are
not actually required to specify the action after the pattern, depending
on what you want awk to do.

awk \'{action} pattern {action}{action}\' file

The most common way to use awk, though, is with the \'pattern {action}\'
syntax. You can also feed multiple files into awk and it will go through
each file in the order you specify.

awk \'pattern {action}\' file1 file2 file3

You can use the wildcard \* to make awk apply to all files in the
directory:

awk \'pattern {action}\' \*

Now, let\'s get into actually using the awk program. We will explore
what we can do with both the patterns and actions of awk. Imagine we
have a file called \'random.txt\' which contains the following lines:

a b c d

hello my name is

the best name ever

Let\'s say we want to make awk go through this file and print every
line, one by one. To make awk print anything it sees in a line, you must
use the print keyword (similar to print() in python or other languages).
If the print keyword is the only thing in your action, it will simply
print the entire line.

awk \'{print}\' random.txt

This will print each line in the order they appear in. One of the main
and most useful features of awk is its built-in variables. When awk
processes each line, it assigns the entire line to the variable 0, which
you can refer to in awk as \$0 (the way you would call any variable in
Bash). In other words, the following is equivalent to what we just
wrote:

awk \'{print \$0}\' random.txt

Because \$0 refers to the entire line. In our original random.txt file,
notice every word/letter on each line is separated by a space. The awk
program will interpet the space as a *separator*, and whatever appears
around the separator as a column or field. If every separator in your
file is a tab instead of a space, awk will also correctly interpret
that. If the separator is something else, like a comma, then you have to
specify this to awk using the -F flag, eg 

ask -F\",\" \'{print}\' file

Each field of a line is assigned, in the order in which they appear, to
the variables \$1, \$2, ..., \$n, where n simply represents the *n*th
field in a line. In random.txt, there are four fields in each line, and
so we could access each field as \$1, \$2, \$3, or \$4. To print the
first field of every line:

awk \'{print \$1}\' random.txt

This would return:

a

hello

the

If our file was a dataframe or a table, running awk \'{print \$1}\'
would be the equivalent of printing every element in the first column
(which is the same thing as just printing the first column). Notice
that, depending on the order in which we print fields, we can actually
rearrange a dataframe or table.

awk \'{print \$3, \$1, \$4, \$2}\' random.txt

This returns:

c a d b

name hello is my

name the ever best

I have put commas between each statement I wanted awk to print. The
comma separates each printed statement with a space. If I omitted the
comma, then every printed statement would be concatenated, i.e. the
first line would be printed as cadb and the second would be printed as
namehelloismy. If I want to manually insert a space, or any string for
that matter into what I am printing, I enclose the string I want to
insert in \" \" quotes. (It is important you use double-quotes \" \"
instead of single-quotes \' \', because single-quotes are reserved for
enclosing the entire action-pattern statement.) So, this:

awk \'{print \$3 \" \" \$1 \" \" \$4 \" chicken \" \$2}\' random.txt

Returns:

c a d chicken b

name hello is chicken my

name the ever chicken best

Notice that inserting strings into the output allows us to change an
existing table or dataframe by inserting any user-specified columns we
want wherever we want. We can also remove any column, e.g. the second
column, by simply not writing \$2 in the print. We can also manipulate
columns by concatenating any string we want to the elements of that
column.

Furthermore, awk supports escape characters like \\n (newline) and \\t
(tab). Namely, writing \"\\t\" will add a tab wherever you put it.

awk \'{print \$3 \"\\t\" \$1 \"\\t\" \$4 \"\\t\" \$2}\' random.txt

c    a    d    b

name    hello    is    my

name    the    ever    best

Feel free to google all the escape characters available (there are a
lot). Two more built-in variables in awk are NR and NF. NR means \'row
number\', and NF means \'field number\'. NR represents which row awk is
in as it processes the file. NF represents the number of fields in each
row. In the above file, there are three rows and each row contains four
fields. Let\'s see what happens when we print both NR and NF as awk
processes each line of the file:

awk \'{print NR, NF}\' random.txt

1 4

2 4

3 4

When awk is in the first line, it prints 1 for NR. When it is in the
second line, it prints 2. When it is in the third line, it prints 3.
Each line has four fields, so NF is 4 in each field. When you print NR
in each line, once NR is printed in the very last line of your file, you
will notice that the final NR printed is equal to the number of lines in
your file. Therefore, you could print NR to see how many lines your file
has.

However, what if you *only* wanted to print the number of lines in your
file? This would be convenient if your file has thousands of lines, and
you don\'t want to print thousands of line numbers into your terminal
just to see what the last one is. As it happens, awk has specific
keywords you can place around the action braces { } so that it *only*
performs the action *before* parsing through the first line in the file,
or *after* it has finished parsing the last line in the file. Namely,
these are the BEGIN and END keywords. To make an action apply before
parsing any lines at all, write BEGIN{ }. To only make it happen at the
end, do END{ }. So, to only print the number of rows in the entire file:

awk \'END{print NR}\' random.txt

The only return of this command will be 3, because NR will have reached
3 when it reached the end of the file, and so there are 3 lines in the
file. Let\'s say we want awk to print the third then first field in
every row, followed by printing the number of rows in the entire file.

awk \'{print \$3, \$1}END{print NR}\' random.txt

One useful part of any language is the use of conditional statements,
such as if-then statements. An if-then statement can go inside an
{action} in awk, and it results in the action only being executed if the
condition applies. The syntax for if-then statements in awk is:

awk \'{if (condition) action}\' file

Awk also supports comparison operators between numbers, such as == \>
\>= \< \<= != (ie: equal to, greater than, greater than or equal to,
less than, less than or equal to, not equal to). Say we have this file
called numbers.txt:

10 20 30

50 70 30

99 99 50

To only print a line if its second field is a number greater than 50:

awk \'{if (\$2 \> 50) print \$0}\' numbers.txt

50 70 30

99 99 50

Let\'s say we want to see the *sum of all the numbers* in a line *if*
the second number is greater than 50. Awk also supports arithmetic
operators between numbers like + (addition), - (subtraction), \*
(multiplication), / (division), % (remainder), \^ (to the power of).

awk \'{if (\$2 \> 50) print \$1+\$2+\$3}\' numbers.txt 

Let\'s say we want to know *how many lines in the file* have a second
value greater than 50. Earlier, I noted awk supports built-in variables
like NF and NR. It also supports user-defined variables, similar to when
you write x = 0 in Python or initialize variables in another language.
Initializing variables is where the BEGIN statement becomes useful, i.e.
creating variables before you begin parsing any lines of the file, and
then acting on those variables as awk runs through the file. (Another
use of BEGIN is to create header lines for your file.) Note that awk
also supports shorthand assignment operators for incrementing a
variable, such as += -= \*= /= %= \^=. If you don\'t know what a
shorthand assignment operator, it might be worth separately searching
into this to understand. These shorthand assignment operators are useful
for changing variables as awk runs through a file. So, again, what is a
way we can print *the number of lines in a file* where the second number
is greater than 50? One approach, in principle, is to first initialize a
variable (say, the variable x) as 0. Then, we check if the second number
in the line is greater than 50. If it is, we increment x by one. Then,
after we finish running through the file, we print x and see what value
it has. How can we implement this in awk? As follows:

awk \'BEGIN{x = 0} {if (\$2 \> 50) x += 1} END{print \$x}\' numbers.txt

This will give us the correct answer for our file, 2. 

This has hopefully served as a meaningful introduction into using
actions in awk. Although keep in mind, it does not even begin to scratch
the potential functionality of the awk language. Patterns are much
simpler to use. Let\'s say we wanted to print a line *if* the the number
30 occurs anywhere in the line. To do this, we will use the \~ operator.
The syntax of the \~ operator is location \~ pattern. The \'location\'
is which part of the line you want to look to find a pattern in. The
pattern itself is the pattern you\'re looking for in the file. So, to
print a line if 30 occurs anywhere in it:

awk \'\$0 \~ 30 {print}\' numbers.txt

A pattern statement does not need to use the \~ operator. It can simply
specify a condition that must be true. Say we wanted only to print lines
where the third number is greater than the sum of the first two numbers:

awk \'\$3 \> \$1 + \$2 {print}\' numbers.txt

For numbers.txt, none of the lines meet this condition, and so nothing
will be printed. Furthermore, awk supports the use of regular
expressions (regex). If you don\'t know what regex is, you should learn
about this separately. But it is basically a super advanced way of
finding complex patterns in lines. In regex, the pattern fire.\*fighter
can match both \"firefighter\" and \"fireflappingfighter\". While awk
supports regex in its patterns, it does not do so by default. You have
to specify to awk that your pattern is using a regular expression. To
indicate this to awk, you have to wrap your pattern in / / forward
slashes. For example:

awk \'/fire.\*fighter/ \~ \$2 {print}\' file1 file2

This pattern ill print any line where the regex pattern fire.\*fighter
is found in the second field of the row, and it will do so for both
file1 and then file2. 

The last thing I will mention about awk is that it contains many
built-in functions, for example the length() function which gives you
the number of characters of whatever you pass into it (roughly
equivalent to len() in Python). Functions can be used either in patterns
or actions or both. For example, if you want to print any line where the
total number of characters in the line is more than 10, you can do it in
two ways from what we\'ve learned so far:

awk \'length(\$0) \> 10\' file

awk \'{if ( (length(\$0) \> 10) print}\' file

The first method uses the length of the line as the pattern awk checks
before executing the action. Note that if an action statement in awk is
preceded by a pattern, it will only execute if the pattern is found in
the line. In the second method, we use an if-then statement to print the
line if its length is greater than 10. There are a large number of
built-in functions in awk that are capable of performing all sorts of
useful tasks you\'d like to accomplish when parsing a file. Even more
advanced, there\'s actually a way to build your own functions in awk.
However, if you\'re going to be building functions in awk, you\'re
already getting into the territory of writing programs in awk longer
than is usually used for. If you absolutely need to do this instead of
doing so in Python instead, you should put your awk script into a file
that ends in a .awk extension. Then, you can specify to awk that you
want to run a set of awk commands found in your .awk file instead of
writing them out directly by specifying your .awk file with the -f flag.
An awk file might be named commands.awk and it may look like this:

#! /bin/awk -f \# this is called a \'shebang\' and your .awk file needs
it at the top

{print}

This script simply contains the commands for printing every line. To
call your awk commands from your .awk script, indicate you\'re passing
in a .awk file to the awk program using the -f flag:

awk -f commands.awk file

But again, you generally shouldn\'t be writing programs in awk complex
enough that you need to store them into a separate file. That is for
more-advanced and quite niche use.

This has been a very simple and short introduction to using awk. Once
you begin learning more about awk and become competent enough that you
actually begin using it for various tasks, and once you feel like
you\'re ready to get to the next stage of exploiting the power of this
programming language, you can consult the awk manual:
[https://www.gnu.org/software/gawk/manual/gawk.html](https://www.gnu.org/software/gawk/manual/gawk.html){.external-link
rel="nofollow"}. If there\'s a specific thing you need to get done,
though, and you\'re having a hard time figuring it out, you should just
google how to do it in awk instead of trying to go through the awk
manual.
:::
:::
:::

::: {#footer role="contentinfo"}
::: {.section .footer-body}
Document generated by Confluence on May 22, 2024 11:44

::: {#footer-logo}
[Atlassian](https://www.atlassian.com/)
:::
:::
:::
:::
