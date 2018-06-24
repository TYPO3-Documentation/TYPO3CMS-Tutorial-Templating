.. include:: ../Includes.txt

.. _introduction:

============
Introduction
============

One general approach to web design considers the production of a web page in
three layers. The structural layer holds the content and the skeleton of the
page: the text, images and other objects; and the markup language to declare
what’s what. The presentation layer holds styling information to tell the
content how and where to appear on the page. The behavioral layer, finally,
scripts the nuances of the interactions between person and page.

A templating system can help model the skeleton for the page content. TYPO3
Fluid and TypoScript work together as a templating system within TYPO3 CMS.

This tutorial introduces TYPO3 Fluid and TypoScript in minimal designs, then
moves into a basic design of a web page having a header, footer, top level
navigation menu, breadcrumb trail menu, and a body with either one or two
columns. The tutorial then modifies the basic design a few times to
illustrate different Fluid techniques. The finishing design is flexible
enough to produce a two column page structure on demand, when there is
content available for the second column.

This is a basic tutorial about templating with TYPO3 Fluid and TypoScript. We
assume you have an installed and working TYPO3 CMS version 8 or higher. You
should also be familiar with the general principles chapter in the typo3.org
*Getting Started Tutorial* document, and the content elements and pages 
chapters in *TYPO3 Tutorial for Editors*.

This tutorial will have you create pages and templates; but after the minimal
designs, it will assume you want to generate your own content elements for
testing the designs. Most of the templates here can be copied directly into
your system as you work through the tutorial.

The tutorial ends with some tips for finding further information about
templating within TYPO3 CMS.

~ `Andrew Murphy`_ wrote this tutorial in May, 2018.

.. _Andrew Murphy: front.desk@keystone-research-solutions.com
