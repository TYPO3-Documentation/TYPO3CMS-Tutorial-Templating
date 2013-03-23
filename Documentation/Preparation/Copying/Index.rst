.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../Includes.txt


.. _copying-template:

Copying the template files to the right place
"""""""""""""""""""""""""""""""""""""""""""""

Now you have the extracted files in your file system. They are, from the folder
where you installed TYPO3, inside the subfolder
:file:`typo3conf/ext/doc_tut_templating/template`.
Next copy the folder :file:`template` with
its contents and paste it all into the folder :file:`fileadmin/`, so that you get the
folder :file:`fileadmin/template/` and the files inside. Creating a page structure

We will now create some pages inside TYPO3. These pages are helpful, when you
later want to check, if TYPO3 uses the instructions in the TypoScript template
as we want it to use them. When you created some pages and some subpages, you
will later be able to check if TYPO3 creates the desired output. After you have
configured the menu in the TypoScript template, the structure of these pages
should be visible in the menu. If you put some content on some of these pages
in TYPO3, you will also be able to see this content once you have configured
the corresponding part of the TypoScript template.