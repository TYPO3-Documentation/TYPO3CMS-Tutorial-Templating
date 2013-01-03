.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../Includes.txt

.. _tasks:

Tasks
^^^^^

.. note::
   This is a step by step instruction like a cooking recipe. It must be a logical thread from start to end divided steps. It gives additional information (but not to much!) and warns for difficult situation (e.g. data loss). After several steps a result may be well. The task end must be identifiable by a result.

In this tutorial we use the most common approach for building a website with TYPO3: We take one HTML file, which we call our HTML template. It will be used as a basis for the website. TYPO3 will use this file as a basis, but certain parts of this file will be replaced with the content, which you have in your TYPO3 installation. To tell TYPO3, which parts it should replace, we will modify the HTML template now. Inside the HTML template we will add so called markers and subparts. 

In a later chapter we will configure TYPO3 to replace these markers and subparts with the content, which has been inserted in TYPO3.

.. toctree::
   :maxdepth: 5
   :titlesonly:
   :glob:

   WorkingHTML/Index
   WorkingTypoScript/Index
   Result/Index
   Targets