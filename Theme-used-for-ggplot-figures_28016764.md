---
title: "TheNessLab : Theme used for ggplot figures"
---

::: {#page}
::: {#main .aui-page-panel}
::: {#main-header}
::: {#breadcrumb-section}
1.  [TheNessLab](index.html)
2.  [The Ness Lab Wiki](The-Ness-Lab-Wiki_11436042.html)
3.  [Coding tips and tutorials](Coding-tips-and-tutorials_11436186.html)
4.  [Making figures: ggplot examples](28016741.html)
:::

# [ TheNessLab : Theme used for ggplot figures ]{#title-text} {#title-heading .pagetitle}
:::

::: {#content .view}
::: page-metadata
Created by [ James Santangelo]{.author}, last modified on Jul 04, 2018
:::

::: {#main-content .wiki-content .group}
When plotting figures with ggplot, the code for any given figure can
often be unwieldy due to the large number of aesthetic adjustments we
impose to make the figures look pretty. However, we take advantage of
the fact that ggplot objects are built layer-by-layer. Because, we often
want many of our figure to look similar, this means we can save our
favourite theme as an object and simply add it to out base ggplot
objects to produce a figure with the desired appearance. 

Below is a figure from a recent paper produced using the default ggplot
aesthetics. The figure itself isn\'t important but the point is that it
doesn\'t look spectacular. For example, the grid is distracting, the
points are small, the labels are small and on the x-axis are almost
overlapping and the axes do not stand out. I used the following code to
produce this figure. 

    MeanSlope_Sel_Mig <- ggplot(MeansProps_Gen250, aes(x = max_s, y = mean, group = factor(Mig_rate))) + 

     geom_errorbar(aes(ymin = mean - ci_mean, ymax = mean + ci_mean), width=0.15, size=0.7,
                       position = position_dodge(width = 0.35)) +
     geom_line(size = 1, aes(linetype = factor(Mig_rate)), position = position_dodge(width = 0.35)) +
     geom_point(size = 3.5, aes(fill = factor(Mig_rate), shape = factor(Mig_rate)), position = position_dodge(width = 0.35)) + 
     scale_shape_manual(labels = c("0", "0.01", "0.05"), values = c(21, 22, 23)) +
     scale_fill_manual(labels = c("0", "0.01", "0.05"), values = c("white", "grey60", "black")) +
     scale_linetype_manual(labels = c("0", "0.01", "0.05"), values = c("dotted", "dashed", "solid")) + 
     ylab("Mean slope") + xlab("Selection coefficient") + 
     coord_cartesian(ylim = c(-0.007, 0.038)) + scale_y_continuous(breaks = seq(from = -0.006, to = 0.036, by = 0.006)) + 
     labs(fill = "Migration rate", shape = "Migration rate", linetype = "Migration rate")

\

[[![](rest/documentConversion/latest/conversion/thumbnail/28016762/1){height="400"
draggable="false"}](/download/attachments/28016764/Figure_ex_noTheme.pdf?version=1&modificationDate=1530752712000&api=v2){.confluence-embedded-file
nice-type="PDF Document"
file-src="/download/attachments/28016764/Figure_ex_noTheme.pdf?version=1&modificationDate=1530752712000&api=v2"
linked-resource-id="28016762" linked-resource-type="attachment"
linked-resource-container-id="28016764"
linked-resource-default-alias="Figure_ex_noTheme.pdf"
mime-type="application/pdf" has-thumbnail="true"
linked-resource-version="1" can-edit="true"
aria-label="Figure_ex_noTheme.pdf"
draggable="false"}[]{.companion-edit-button-placeholder
.edit-button-overlay linked-resource-container-id="28016764"
linked-resource-id="28016762" template-name="companionEditIcon"
source-location="embedded-attachment"}]{.confluence-embedded-file-wrapper}

\

To make this figure publication quality, we can create a \'theme\'
object, which can also be used to produce other figures in the project.
The theme object may look something like this (I have been using this
theme for every figure for the last 9 years and only slightly modify it
as needed).

\

    ggplot_theme <- theme(aspect.ratio=0.9,panel.background = element_blank(), 
     panel.grid.major = element_blank(), 
     panel.grid.minor = element_blank(),
     panel.border=element_blank(),
     axis.line.x = element_line(color="black",size=1), 
     axis.line.y = element_line(color="black",size=1),
     axis.ticks=element_line(color="black"), 
     axis.text=element_text(color="black",size=15), 
     axis.title=element_text(color="black",size=1), 
     axis.title.y=element_text(vjust=2,face="bold",size=15),
     axis.title.x=element_text(vjust=0.1,face="bold",size=15),
     axis.text.x=element_text(size=15,angle=45,hjust=1),
     axis.text.y=element_text(size=15),
     legend.position = "right", legend.direction="vertical", 
     legend.text=element_text(size=11), legend.key = element_rect(fill = "white"), 
     legend.title = element_text(size=13,face="bold"),legend.key.size = unit(0.5, "cm"))

\

All we have to do now is add this theme to our plot object, as follow:

\

    MeanSlope_Sel_Mig + ggplot_theme

\

Doing so produces the following figure:

\

[[![](rest/documentConversion/latest/conversion/thumbnail/28016765/1){height="400"
draggable="false"}](/download/attachments/28016764/plot.pdf?version=1&modificationDate=1530752799000&api=v2){.confluence-embedded-file
nice-type="PDF Document"
file-src="/download/attachments/28016764/plot.pdf?version=1&modificationDate=1530752799000&api=v2"
linked-resource-id="28016765" linked-resource-type="attachment"
linked-resource-container-id="28016764"
linked-resource-default-alias="plot.pdf" mime-type="application/pdf"
has-thumbnail="true" linked-resource-version="1" can-edit="true"
aria-label="plot.pdf"
draggable="false"}[]{.companion-edit-button-placeholder
.edit-button-overlay linked-resource-container-id="28016764"
linked-resource-id="28016765" template-name="companionEditIcon"
source-location="embedded-attachment"}]{.confluence-embedded-file-wrapper}

\

\

\
:::

::: {.pageSection .group}
::: pageSectionHeader
## Attachments: {#attachments .pageSectionTitle}
:::

::: {.greybox align="left"}
![](images/icons/bullet_blue.gif){height="8" width="8"}
[Figure_ex_noTheme.pdf](attachments/28016764/28016762.pdf)
(application/pdf)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[figure_ex_Theme.pdf](attachments/28016764/28016763.pdf)
(application/pdf)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[plot.pdf](attachments/28016764/28016765.pdf) (application/pdf)\
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
