.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../Includes.txt


.. _creating-page-structure:

Creating a page structure
"""""""""""""""""""""""""

Now, let´s go through the steps for creating the page structure.
The screenshots are from the :ref:`Introduction Package <t3start:start>`.
You can also use the blank package; you just need to ignore the extra pages in the tree (i.e., the "Home" and
"TypoScript-Templates" branches [pages, folders] of the Introduction Package).

In the TYPO3 CMS backend make sure you are in the Page module by first opening the "Web" section
on the left side of the Backend and then clicking on the "Page" module underneath.
This will open the page tree of your TYPO3 CMS installation.

.. figure:: ../../Images/TBT-page-module.jpg
   :alt: The Page Module

Create a first page, which is hierarchically located directly below the TYPO3 CMS
logo at the top. We call this page a "root" page. We are also going to give it the name Root.

1. Right-click on the logo of "New TYPO3 site", then left-click New from the pop-up menu.

.. figure:: ../../Images/TBT-page-structure-new.jpg
   :alt: Creating a new root page

2. Place the page at the bottom of the present pages and folders (Home and TypoScript Templates).

.. figure:: ../../Images/TBT-page-structure-new-2.jpg
   :alt: Select position for the root page

3. Change the page type to "Standard" and confirm that change on your browser´s pop-up menu
(note: this is not the same as TYPO3 CMS' context pop-up menu). Give the page the title "Root".

.. figure:: ../../Images/TBT-page-structure-new-3.jpg
   :alt: Customising the root page

4. Switch to the "Behaviour" tab, the fourth to the right. Go down to the "Miscellaneous" palette and
mark the checkbox "Use as root page"

.. figure:: ../../Images/TBT-page-structure-new-4.jpg
   :alt: Use page as root page

5. Click "Save and close document" (the diskette icon with an "x" on the lower left).
Now you see the new page (Root) with a globe icon in the page tree:

.. figure:: ../../Images/TBT-page-structure-new-5.jpg
   :alt: Active root page

At this point we will now create subpages hierarchically located inside the "Root" page you just created.

6. Right-click on the "Root" page and from the context menu select "Page Actions >
New".

.. figure:: ../../Images/TBT-page-structure-new-6.jpg
   :alt: Create subpages

7. Place the new page hierarchically inside (under) the "Root" page.

.. figure:: ../../Images/TBT-page-structure-new-7.jpg
   :alt: Select position for a subpage

8. Under the "General" tab go to the palette "Title" > "Page Title" and type in "Home" .
Next, switch to the "Access" tab to the right and, in the "Visibility" palette, uncheck the "Disable" option under "Page".

.. figure:: ../../Images/TBT-page-structure-new-8.jpg
   :alt: Customising the subpage

9. Click "Save and Close document" (the diskette icon with an "x" on the lower left).

Create some more subpages inside (under) the root page by following the instructions from 1-9. Place them on the
same hierarchichal level as the page "Home" but below it.

10. Switch into the page tree by clicking on the small triangle in front of the globe icon with the page "Root".

.. figure:: ../../Images/TBT-page-structure-new-9.jpg
   :alt: Expanding subpages below root

Here you can see the complete page structure. This is what the result should, or might, look
like:

.. figure:: ../../Images/TBT-page-structure-new-10.jpg
   :alt: A new page structure

11. Now, we are going to edit the Root page again by right-clicking on the globe icon.
When the context menu pops up, click on edit (the paper and pencil icon).

.. figure:: ../../Images/TBT-page-structure-new-11.jpg
   :alt: Editing the root page

12. On the "General" tab, change the Type from "Standard" to "Shortcut" in the drop-down menu and confirm that change
in the pop-up menu from your browser.

.. figure:: ../../Images/TBT-page-structure-new-12.jpg
   :alt: Root page becomes Shortcut

13. Click the small folder icon to the lower left under "Shortcut Target" to select the target page.
A TYPO3 CMS pop-up menu will appear in a new window in your browser.

.. figure:: ../../Images/TBT-page-structure-new-13.jpg
   :alt: Selecting a target page

In the pop-up window, you can now select the target.

14. Choose the first page of the subpages. In our case, this is the page which we named "Home". Navigate there
by clicking the small triangles in front of the page names. Click on the page "Home" and the pop-up menu will disappear.

.. figure:: ../../Images/TBT-page-structure-new-14.jpg
   :alt: Home becomes target for root page

15. Now that you are back in the editing form from which you came, click "Save and close document".

.. figure:: ../../Images/TBT-page-structure-new-14a.jpg
   :alt: Button "Save and close document"

Now you have created a complete page structure.
