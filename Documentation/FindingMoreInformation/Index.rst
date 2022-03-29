.. include:: ../Includes.txt

.. _finding-more-information:

========================
Finding more information
========================

Source Code
===========

The most authoritative and most current reference for TYPO3 Fluid information
is, of course, the TYPO3 CMS source code itself.

Here are some source code folders and files you may find useful.

:file:`vendor/typo3fluid/fluid/doc`

:file:`typo3/sysext/fluid_styled_content/Documentation/Introduction/Index.rst`

:file:`typo3/sysext/fluid`

TYPO3 CMS source code also includes Fluid examples you may find useful.

:file:`typo3/sysext/fluid_styled_content/Resources/Private`

:file:`typo3/sysext/fluid/Resources/Private`

:file:`typo3/sysext/about/Resources/Private`

The [ https://api.typo3.org/ ] website provides an applications programming
interface (API) viewer that can help you navigate parts of the TYPO3 CMS
source code. Once you choose the TYPO3 CMS version, here are some navigation
paths that may be useful.

`Classes > TYPO3 > CMS > Fluid`

`Classes > TYPO3 > CMS > FluidStyledContent`

`Classes > TYPO3 > CMS > Frontend > ContentObject > FluidTemplateContentObject`

Official Documentation
======================

There is a centralized documentation library at https://docs.typo3.org containing links to
tutorials, guides, reference manuals and code snippets.


These are the potentially useful manuals we will be referring to:

* :ref:`t3ts45:start`: This is an introductory tutorial to TypoScript Templating
* :ref:`t3coreapi:typoscript-syntax-start` in the manual "TYPO3 Explained" walks you through
  everything you need to know about the TypoScript syntax
* :ref:`t3tsref:start`
* :ref:`t3extbasebook:start` This is a resource for developing extensions using
  Extbase and Fluid. The part about Extbase will not be relevant for you when
  creating a site template, but you might find useful information in the Fluid
  section :ref:`t3extbasebook:fluid`. Do note that this manual has a different scope,
  as the Fluid here is used for generating output for Plugins.

Fluid

* https://typo3buddy.com/typo3-template-tutorial/fluid/
* :ref:`t3viewhelper:typo3-fluid-cobject` (ViewHelper Reference)
* :ref:`t3extbasebook:moving-repeating-snippets-to-partials` ("Developing TYPO3 Extensions with Extbase and Fluid")
* :ref:`t3extbasebook:creating-a-consistent-look-and-feel-with-layouts` ("Developing TYPO3 Extensions with Extbase and Fluid")
* `TYPO3/Fluid: doc <https://github.com/TYPO3/Fluid/tree/master/doc>`__, especially the :file:`FLUID_STRUCTURE.md` text file.


TypoScript Templating

* :ref:`t3coreapi:typoscript-syntax-start` (TYPO3 Explained)
* :ref:`TypoScript syntax: conditions <t3coreapi:typoscript-syntax-conditions>` (TYPO3 Explained)
* :ref:`t3tsref:cobj-fluidtemplate` (TypoScript Reference)
* :ref:`t3tsref:cobj-hmenu` (TypoScript Reference)
* :ref:`t3tsref:hmenu-special-rootline` (TypoScript Reference)
* function: :ref:`t3ts45:function-if` (TypoScript in 45 Minutes), see also :ref:`t3tsref:if` in "TypoScript Reference"
* :ref:`t3tsref:page` (TypoScript Reference)


Videos
======

TYPO3 has an `official YouTube channel <https://www.youtube.com/channel/UCwpl8LY9Tr3PB26Kk2FYW_w>`__.

You can find helpful videos about TYPO3 there, but not very much about templating on a beginner
level.

A video that may be useful:

2017-11-10 **Tutorial - Site Packages - Part 1** by Mathias Schreiber

.. youtube:: HtBmim7pc0o


Searches
========

Other than the docs.typo3.org references, you can find additional information by
searching the Web. For example, try a search phrase such as
[ :aspect:`typo3 fluid` ] on a popular video website. If you have a specific
problem, think of key words or concepts to use in a search phrase. While
writing this tutorial, Web searches led to these specific references.

Questions
=========

Lastly, after searching to find information already published, you may want
to ask the TYPO3 community.

You can get information about where to get help on https://typo3.org/help.

Specifically, choose one of these options:

#. Ask **programming related questions** on
   `Stack Overflow <https://stackoverflow.com/search?q=typo3>`__ using the tag "typo3"
#. Ask general TYPO3 questions in the Slack channel #typo3-cms in the
   `TYPO3 Slack workspace <https://typo3.slack.com>`__.
   `Get your Slack invitation <https://my.typo3.org/slack/invite>`__ first.


Credit
======

The retired TYPO3 Wiki was fundamental to starting the work leading to this tutorial.

The following Web search results contributed directly to the tutorial’s final
template design.

[ https://stackoverflow.com/questions/27052098/how-do-i-check-for-column-content-in-a-typo3-fluid-template
], answer by lorenz on 2014-11-27 14:14.

[ https://forum.typo3.org/index.php/t/189892/ ], comment from Claus Due on
2012-06-20 21:24.

[ https://forge.typo3.org/issues/34152 ], comment #31 by Ernesto Baschny.
