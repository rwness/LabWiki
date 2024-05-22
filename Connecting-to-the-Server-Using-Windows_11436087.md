---
title: "TheNessLab : Connecting to the Server Using Windows"
---

::: {#page}
::: {#main .aui-page-panel}
::: {#main-header}
::: {#breadcrumb-section}
1.  [TheNessLab](index.html)
2.  [The Ness Lab Wiki](The-Ness-Lab-Wiki_11436042.html)
3.  [HPCnode 1 Documentation](HPCnode-1-Documentation_11436057.html)
:::

# [ TheNessLab : Connecting to the Server Using Windows ]{#title-text} {#title-heading .pagetitle}
:::

::: {#content .view}
::: page-metadata
Created by [ Unknown User (moham727)]{.author}, last modified by [ Jimmy
Issa]{.editor} on Dec 20, 2022
:::

::: {#main-content .wiki-content .group}

------------------------------------------------------------------------

## 2022 Update -- using WSL2 {#ConnectingtotheServerUsingWindows-2022Update–usingWSL2}

Accessing a Unix shell like Bash on Windows has become substantially
easier and simpler in recent years. In 2017, Microsoft released the
**Windows Subsystem for Linux** (WSL), eliminating the need for using
third-party applications like MobaXterm. In 2019, WSL2 was released,
enabling the installation of a native Linux subsystem onto your
(otherwise) Windows computer. 

**Prerequisites:**

-   **Windows 10 or Windows 11**
-   **Make sure all recent updates are installed. Go to Settings, search
    Windows Update settings, check for updates and install any
    available.**

The steps for installing WSL2 are as follows:

1.  Open the Command Prompt in Administrator mode. (If you don\'t know
    how to do this, go to the Windows search box, type in \'Command
    Prompt\', and the application should show up. Right-click on it and
    click on \'Run as administrator\'.)
2.  Run the following command: wsl \--install
3.  Restart your computer. You\'re done.

You should now be able to search for the Bash terminal (by just
searching \'Bash\') in the Windows search box. If you know anything
about Linux, you might be wondering which Linux distro you installed
when you ran wsl \--install. You installed Ubuntu, Ubuntu is the most
widely-used Linux distro because it is also the simplest one. (While it
is possible to specify a different distro with the wsl command, I don\'t
see the actual need for using any other distro for the purpose of
bioinformatics. Not only that, but if you do something like install Arch
instead of Ubuntu without already being a power-user, you will suffer.)

Now that you can access a terminal like Bash, go to the other Wiki page
\"Connecting to the server\" and you can follow the exact same
instructions that everyone else follows to connect to the server. But
basically you just run this:

[ssh
-v ]{style="color: rgb(23,43,77);"}[utorid@hpcnode1.utm.utoronto.ca](mailto:utorid@hpcnode1.utm.utoronto.ca){.external-link
style="" rel="nofollow"}

And of course replacing \'utorid\' with your personal utorid.

**Tips**

You may also be prompted for your utor password upon getting into the
server. I recommend using a private key so that you don\'t need to enter
your password each time you get into the server, as well as adding an
alias for the ssh command above into your \~/.bashrc file so you don\'t
need to remember how to type the whole thing every time you want to get
into the server. Personally I\'ve added this alias to my bashrc file:

alias utmssh=\"ssh -v utorid@hpcnode1.utm.utoronto.ca\"

So I just type and enter \'utmssh\' into Bash to enter the server.

\

## Using MobaXterm {#ConnectingtotheServerUsingWindows-UsingMobaXterm}

\

1.  Take pride in the fact that you did not succumb to the Mac influence
    by purchasing an overpriced shiny piece of metal. Consumerism? Not
    today.
2.  Connect to the vpn by following the instructions on here:
    [http://vpn.utoronto.ca/win_install](http://vpn.utoronto.ca/win_install){.external-link
    rel="nofollow"}
3.  Download MobaXterm Home edition (Portable edition). This allows you
    to have a shell to work out of, similar to the built-in terminal you
    would find on a Mac.\
    [http://mobaxterm.mobatek.net/download-home-edition.html](http://mobaxterm.mobatek.net/download-home-edition.html){.external-link
    rel="nofollow"}
4.  Once you click on the application, a message will appear that you
    will need to extract all files before running it. Select "OK"

\

[![](attachments/11436087/11436078.png){.confluence-embedded-image
draggable="false" height="400"
image-src="attachments/11436087/11436078.png"
unresolved-comment-count="0" linked-resource-id="11436078"
linked-resource-version="2" linked-resource-type="attachment"
linked-resource-default-alias="p4.png"
base-url="https://wiki.utm.utoronto.ca"
linked-resource-content-type="image/png"
linked-resource-container-id="11436087"
linked-resource-container-version="7"}]{.confluence-embedded-file-wrapper
.confluence-embedded-manual-size}[![](attachments/11436087/11436077.png){.confluence-embedded-image
draggable="false" height="400"
image-src="attachments/11436087/11436077.png"
unresolved-comment-count="0" linked-resource-id="11436077"
linked-resource-version="2" linked-resource-type="attachment"
linked-resource-default-alias="p4.2.png"
base-url="https://wiki.utm.utoronto.ca"
linked-resource-content-type="image/png"
linked-resource-container-id="11436087"
linked-resource-container-version="7"}]{.confluence-embedded-file-wrapper
.confluence-embedded-manual-size}

5\. Run OpenVPN as an administrator and login with your UTORid and
password when it prompts.

\

[![](attachments/11436087/11436084.png){.confluence-embedded-image
draggable="false" height="400"
image-src="attachments/11436087/11436084.png"
unresolved-comment-count="0" linked-resource-id="11436084"
linked-resource-version="1" linked-resource-type="attachment"
linked-resource-default-alias="adminvpn pic.PNG"
base-url="https://wiki.utm.utoronto.ca"
linked-resource-content-type="image/png"
linked-resource-container-id="11436087"
linked-resource-container-version="7"}]{.confluence-embedded-file-wrapper
.confluence-embedded-manual-size}

\

6\. Open Mobaxterm and where it says "Find existing session" or server
name, begin typing the name of the server "hpcnode..". Once you start
typing, it gives you a drop-down menu. If you have previous sessions,
these will appear here. Since this is the first time connecting, you
will have to make a new session, so click on that option.

\

[![](attachments/11436087/11436080.png){.confluence-embedded-image
draggable="false" height="400"
image-src="attachments/11436087/11436080.png"
unresolved-comment-count="0" linked-resource-id="11436080"
linked-resource-version="1" linked-resource-type="attachment"
linked-resource-default-alias="p6.png"
base-url="https://wiki.utm.utoronto.ca"
linked-resource-content-type="image/png"
linked-resource-container-id="11436087"
linked-resource-container-version="7"}]{.confluence-embedded-file-wrapper
.confluence-embedded-manual-size}

\

7\. Where it says select session type, choose the SSH option.

8\. Type
in **"[hpcnode1.utm.utoronto.ca](http://hpcnode1.utm.utoronto.ca/){.external-link
rel="nofollow"}" **in the space where it says \"Remote host\". If you'd
like, you can also check off the "specify username" box and type in your
utorid there as well. This makes it so that you do not need to enter
your password with each subsequent login. 

\

[![](attachments/11436087/11436081.png){.confluence-embedded-image
draggable="false" height="400"
image-src="attachments/11436087/11436081.png"
unresolved-comment-count="0" linked-resource-id="11436081"
linked-resource-version="1" linked-resource-type="attachment"
linked-resource-default-alias="p8.png"
base-url="https://wiki.utm.utoronto.ca"
linked-resource-content-type="image/png"
linked-resource-container-id="11436087"
linked-resource-container-version="7"}]{.confluence-embedded-file-wrapper
.confluence-embedded-manual-size}

\

9\. Once that's done, click OK and it will ask for your password in the
main window.

\

[![](attachments/11436087/11436082.png){.confluence-embedded-image
draggable="false" height="400"
image-src="attachments/11436087/11436082.png"
unresolved-comment-count="0" linked-resource-id="11436082"
linked-resource-version="1" linked-resource-type="attachment"
linked-resource-default-alias="p9.png"
base-url="https://wiki.utm.utoronto.ca"
linked-resource-content-type="image/png"
linked-resource-container-id="11436087"
linked-resource-container-version="7"}]{.confluence-embedded-file-wrapper
.confluence-embedded-manual-size} 

\

10\. This is what the interface looks like once you're connected to the
server. The pane on the left lets you navigate through the directories
as well as create files/folders (kind of like the Transmit app on Macs
except that it is a built-in feature). This makes it easy to upload and
download files by dragging and dropping. That\'s it! The Ness lab
initiation is
complete ![(smile)](images/icons/emoticons/smile.svg){.emoticon
.emoticon-smile emoticon-name="smile"}

\

[![](attachments/11436087/11436083.png){.confluence-embedded-image
draggable="false" height="400"
image-src="attachments/11436087/11436083.png"
unresolved-comment-count="0" linked-resource-id="11436083"
linked-resource-version="1" linked-resource-type="attachment"
linked-resource-default-alias="p10.png"
base-url="https://wiki.utm.utoronto.ca"
linked-resource-content-type="image/png"
linked-resource-container-id="11436087"
linked-resource-container-version="7"}]{.confluence-embedded-file-wrapper
.confluence-embedded-manual-size}
:::

::: {.pageSection .group}
::: pageSectionHeader
## Attachments: {#attachments .pageSectionTitle}
:::

::: {.greybox align="left"}
![](images/icons/bullet_blue.gif){height="8" width="8"}
[p4.2.png](attachments/11436087/11436085.png) (image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[p4.png](attachments/11436087/11436086.png) (image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[p5.png](attachments/11436087/11436079.png) (image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[p6.png](attachments/11436087/11436080.png) (image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[p8.png](attachments/11436087/11436081.png) (image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[p9.png](attachments/11436087/11436082.png) (image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[p10.png](attachments/11436087/11436083.png) (image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[p4.2.png](attachments/11436087/11436077.png) (image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[p4.png](attachments/11436087/11436078.png) (image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"} [adminvpn
pic.PNG](attachments/11436087/11436084.png) (image/png)\
:::
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
