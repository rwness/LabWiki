---
title: "TheNessLab : Standard Chlamydomonas reinhardtii PCR"
---

::: {#page}
::: {#main .aui-page-panel}
::: {#main-header}
::: {#breadcrumb-section}
1.  [TheNessLab](index.html)
2.  [The Ness Lab Wiki](The-Ness-Lab-Wiki_11436042.html)
3.  [Chlamydomonas information and
    protocols](Chlamydomonas-information-and-protocols_11436157.html)
:::

# [ TheNessLab : Standard Chlamydomonas reinhardtii PCR ]{#title-text} {#title-heading .pagetitle}
:::

::: {#content .view}
::: page-metadata
Created by [ Robert Ness]{.author}, last modified by [ Shanza
Ayub]{.editor} on Feb 05, 2019
:::

::: {#main-content .wiki-content .group}
# PCR reaction recipe {#StandardChlamydomonasreinhardtiiPCR-PCRreactionrecipe}

::: table-wrap
  ------------ --------------- ------------------------- ---------------------
  Ingredient   Concentration   Amount in 20µL PCR (µL)   Final Concentration
  ddH~2~O      \-              10.8                      \-
  Buffer       5× ^1,2^        4.0                       1×
  MgCl~2~      25mM            2.0                       2.5 mM
  dNTP         10mM            1.0                       0.5 mM
  Primer 1     10µM            0.5                       0.25 µM
  Primer 2     10µM            0.5                       0.25 µM
  Taq          5units/µL       0.2                       1 unit
  DNA^4^       10ng/µL         1                         0.5 ng/µL
  ------------ --------------- ------------------------- ---------------------
:::

1.  The concentration of buffers varies by vendor - 5× and 10× are most
    common. Adjust the volume to ensure 1X final concentration and
    adjust the ddH~2~O to match
2.  Some buffers have MgCl~2~. This protocol is assuming the
     MgCl~2~-free buffer, usually labelled -MgCl~2~
3.  The final concentration of MgCl~2~ really alters a PCRs behaviour
    (more Mg means more permissive binding). In reality it can range
    from about 1-6mM final concentration. 
4.  According to the manual, the lab\'s current Taq DNA polymerase stock
    (#EP0401) tolerates 4 pg - 0.4 µg DNA per 20 µL PCR reaction. 

\

## PCR Reaction conditions {#StandardChlamydomonasreinhardtiiPCR-PCRReactionconditions}

::: table-wrap
+----------------------+-----------+------+------------+
| Stage                | Temp      | Time | Cycles     |
+----------------------+-----------+------+------------+
| Initial denaturation | 95^o^C    | 60s  | 1×         |
+----------------------+-----------+------+------------+
| Denaturation         | 95^o^C    | 60s  | ↑          |
|                      |           |      |            |
|                      |           |      | Repeat 35× |
|                      |           |      |            |
|                      |           |      | ↓          |
+----------------------+-----------+------+------------+
| Annealing            | 55-60^o^C | 30s  |            |
+----------------------+-----------+------+------------+
| Extension            | 72^o^C    | 60s  |            |
+----------------------+-----------+------+------------+
| Final Extentsion     | 72^o^C    | 5m   | 1×         |
+----------------------+-----------+------+------------+
:::

\

## PCR Protocol:  {#StandardChlamydomonasreinhardtiiPCR-PCRProtocol:}

\*All steps below can be performed on a regular lab bench but you should
still wear gloves and use sterile techniques.

1.  Prepare a Styrofoam box filled with ice. 
2.  Prepare mastermix. The standard ***x***** **uL of DNA sample is 1
    uL. Before adding each component of the Mastermix, thaw out the
    solutions and vortex/flick the tubes briefly. 
    1.  For PCR reactions with many DNA sample but only using one pair
        of primers and ***x ***µL of DNA sample:\

        Total volume of Mastermix = 19 uL \* ***N** ,\
        *where ***N** = *1.10 \* \# of reactions needed (or \# of DNA
        samples). This makes sure you prepare an extra 10% volume of
        Mastermix to account for pipetting errors. 

        Mastermix= ***N ***\*  (2.0 µL 10X buffer + 2.0 µL 25mM
        MgCl~2~ + 1.0 µL 10 mM dNTP + 0.5 µL 10 µM forward primer +
        0.5 µL 10 µM reverse primer + (12.8-***x***) uL ddH2O)

    2.  For PCR reactions with many DNA sample but  using more than one
        pair of primers and only ***x*** µL of DNA sample:\

        Total volume of Mastermix = 18 uL \* ***N** ,\
        *where ***N** = *1.10 \* \# of reactions needed (or \# of DNA
        samples). This makes sure you prepare an extra 10% volume of
        Mastermix to account for pipetting errors. 

        Mastermix= ***N ***\*  (2.0 µL 10X buffer + 2.0 µL 25mM
        MgCl~2~ + 1.0 µL 10 mM dNTP + ~~0.5 µL 10 µM forward primer +
        0.5 µL 10 µM reverse primer~~ + (12.8-***x***) uL ddH2O)

    3.  Good luck with the other scenarios!
3.  Load ***x*** uL of DNA sample onto the wall of each PCR tube so that
    the drop of DNA sample is visible. Be careful not to load so many
    samples at once that the drops of DNA dry up before you start the
    subsequent steps.
4.  If you performed Step 2b, add 0.5 µL 10 µM forward primer and 0.5 µL
    10 µM reverse primer to the drop of DNA sample in each PCR tube. 
5.  Add*** N** \* *0.5 uL Taq polymerase stock to the Mastermix. Freeze
    the Taq polymerase stock at -20C immediately.
6.  Vortex the Mastermix briefly. 
7.  Load 20-**x** uL Mastermix into each PCR tube by pipetting it onto
    the drop of DNA sample from Step 3. Let the Mastermix roll down to
    the bottom of the tube with the DNA sample. Whenever you complete a
    PCR tube or a strip of PCR tubes, place it on ice.
8.  Centrifuge the tubes briefly using the mini centrifuge if any drops
    are stuck on the wall in the PCR tubes. 
9.  Place the PCR tubes in the thermocycler using \"nesslab\"→
    \"basics\" program or other customized programs. 
10. Once the cycle is done, pick up the PCR products and leave the lid
    open until room temperature to prevent condensation buildup. 

\

::: {.confluence-information-macro .confluence-information-macro-information}
Tips

[]{.aui-icon .aui-icon-small .aui-iconfont-info
.confluence-information-macro-icon}

::: confluence-information-macro-body
-   If you will be doing a lot of PCR, you should prepare your own
    stocks of dNTPs. Ideally, the stocks should be several small stocks
    rather than one large stock.\
    **\
    Y** uL 10 mM dNTP stock = 0.1 \* **Y** uL dNTP \*4 dNTPs + 0.6 \*
    **Y** uL ddH~2~O\
    \
-   You may end the PCR with a long pause at 4ºC if you are picking up
    the PCR product within a few hours. Do not leave it at 4ºC past
    those hours, because condensation will accumulate in the
    thermocycler and break the machine. It is ok to store PCR product at
    10ºC overnight.
:::
:::

\

\
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
