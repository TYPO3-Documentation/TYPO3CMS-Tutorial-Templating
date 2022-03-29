.. include:: /Includes.rst.txt
.. highlight:: typoscript

.. _sharing-and-switching-design-elements:

=====================================
Sharing and switching design elements
=====================================

Our single column page design processed a Fluid template in a
:file:`Templates` folder; and our double column page design processed a Fluid
template in a :file:`Layouts` folder. The two designs had some identical
elements, including :html:`page-header` and :html:`page-footer`.

We can apply Fluid techniques to build more efficient and more flexible
designs.

A design using Fluid partials
=============================

This design produces a single column web page and a double column web page
that share one header and one footer.

In the TYPO3 CMS backend, create a standard page named
:name:`PartialSingleColumn` just under (inside) the :name:`Home` page. On the
:name:`PartialSingleColumn` standard page, create a TypoScript extension template.
In the TypoScript template Setup field, write the following lines::

   page = PAGE
   page.1 = FLUIDTEMPLATE
   page.1 {
      templateName = Partial1Column
      templateRootPaths.1 = fileadmin/sitedesign/Resources/Private/Templates
      partialRootPath = fileadmin/sitedesign/Resources/Private/Partials
      variables {
         contentNormal < styles.content.get
      }
   }

Notice the new :ts:`partialRootPath` instruction.

Create a file named :file:`Partial1Column.html` in the
:file:`fileadmin/sitedesign/Resources/Private/Templates` folder, and write
the following lines in the file:

.. code-block:: html

   <div id="page">
      <f:render partial="PageHeader" />
      <div id="page-body">
         <div id="page-title">{data.title}</div>
         <div id="whole-content">
            <f:format.raw>{contentNormal}</f:format.raw>
         </div>
         <div id="page-body-end">&nbsp;</div>
      </div>
      <f:render partial="PageFooter" />
   </div>

Notice the new :html:`<f:render partial="…" />` elements.

In the TYPO3 CMS backend, create a standard page named
:name:`PartialDoubleColumn` just under (inside) the :name:`Home` page. On the
:name:`PartialDoubleColumn` standard page, create a TypoScript extension template
record. In the TypoScript template Setup field, write the following lines::

   page = PAGE
   page.1 = FLUIDTEMPLATE
   page.1 {
      templateName = Partial2ColumnPage
      templateRootPaths.1 = fileadmin/sitedesign/Resources/Private/Layouts
      partialRootPath = fileadmin/sitedesign/Resources/Private/Partials
      variables {
         contentNormal < styles.content.get
         contentRight < styles.content.get
         contentRight.select.where = {#colPos}=2
      }
   }

Create a file named :file:`Partial2ColumnPage.html` in the
:file:`fileadmin/sitedesign/Resources/Private/Layouts` folder, and write the
following lines in the file:

.. code-block:: html

   <div id="page">
      <f:render partial="PageHeader" />
      <div id="page-body">
         <div id="page-title">{data.title}</div>
         <div id="main-content">
            <f:format.htmlentitiesDecode>{contentNormal}</f:format.htmlentitiesDecode>
         </div>
         <div id="side-content">
            <f:format.htmlentitiesDecode>{contentRight}</f:format.htmlentitiesDecode>
         </div>
         <div id="page-body-end">&nbsp;</div>
      </div>
      <f:render partial="PageFooter" />
   </div>

Create a file named :file:`PageHeader.html` in a
:file:`fileadmin/sitedesign/Resources/Private/Partials` folder, and write the
following lines in the file:

.. code-block:: html

      <div id="page-header">
         <div id="navigation-top-level"><f:cObject typoscriptObjectPath="lib.topNavigation" /></div>
         <div id="navigation-trail">{f:cObject(typoscriptObjectPath:'lib.breadcrumbTrail')->f:format.raw()}</div>
      </div>

Create a file named :file:`PageFooter.html` in the
:file:`fileadmin/sitedesign/Resources/Private/Partials` folder, and write the
following lines in the file:

.. code-block:: html

   <div id="page-footer">
      <div id="footer-notice">
         <p>This is the page footer area.</p>
      </div>
   </div>

The combination of the :html:`<f:render partial="…" />` element and the
partial’s file name tells the TYPO3 CMS renderer which content goes where in
a web page.

This design puts each common partial element into its own file, making
editing more efficient and allowing more flexible editing access controls.

A design using Fluid sections
=============================

This design produces a single column web page having a header and footer, but
using a different technique than earlier.

In the TYPO3 CMS backend, create a standard page named
:name:`SectionSingleColumn` just under (inside) the :name:`Home` page. On the
:name:`SectionSingleColumn` standard page, create a TypoScript extension template.
In the TypoScript template Setup field, write the following lines::

   page = PAGE
   page.1 = FLUIDTEMPLATE
   page.1 {
      templateName = Section1Column
      templateRootPaths.1 = fileadmin/sitedesign/Resources/Private/Templates
      variables {
         contentNormal < styles.content.get
      }
   }

Notice the lack of a :ts:`partialRootPath` instruction.

Create a file named :file:`Section1Column.html` in the
:file:`fileadmin/sitedesign/Resources/Private/Templates` folder, and write
the following lines in the file:

.. code-block:: html

   <div id="page">
      <f:render section="PageHeader" />
      <div id="page-body">
         <div id="page-title">{data.title}</div>
         <div id="whole-content">
            <f:format.raw>{contentNormal}</f:format.raw>
         </div>
         <div id="page-body-end">&nbsp;</div>
      </div>
      <f:render section="PageHeader" />
      <f:render section="PageFooter" />
   </div>
   <f:section name="PageHeader">
      <div id="page-header">
         <div id="navigation-top-level"><f:cObject typoscriptObjectPath="lib.topNavigation" /></div>
         <div id="navigation-trail">{f:cObject(typoscriptObjectPath:'lib.breadcrumbTrail')->f:format.raw()}</div>
      </div>
   </f:section>
   <f:section name="PageFooter">
      <div id="page-footer">
         <div id="footer-notice"> <p>This is the page footer area.</p> </div>
      </div>
   </f:section>

Notice the :html:`<f:render section="…" />` and :html:`<f:section>` elements.
The :html:`<f:section>` element contains the content; but the
:html:`<f:render section="…" />` element tells the TYPO3 CMS renderer where
to render that content. We purposely included a second
:html:`<f:render section="PageHeader" />` element to illustrate the
capability for multiple appearances.

This design places common elements and unique elements into one file, thus
reducing the processing time required to produce a web page.

A design using Fluid layouts
============================

This design produces a single column web page having a header and footer, but
using yet another different technique than earlier.

In the TYPO3 CMS backend, create a standard page named
:name:`LayoutSingleColumn` just under (inside) the :name:`Home` page. On the
:name:`LayoutSingleColumn` standard page, create a TypoScript extension template.
In the TypoScript template Setup field, write the following lines::

   page = PAGE
   page.1 = FLUIDTEMPLATE
   page.1 {
      templateName = ForLayouts
      templateRootPaths.1 = fileadmin/sitedesign/Resources/Private/Templates
      layoutRootPath = fileadmin/sitedesign/Resources/Private/Layouts
      variables {
         contentNormal < styles.content.get
      }
   }

Notice the new :ts:`layoutRootPath` instruction.

Create a file named :file:`ForLayouts.html` in the
:file:`fileadmin/sitedesign/Resources/Private/Templates` folder, and write
the following lines in the file:

.. code-block:: html

   <f:layout name="Layout1ColumnPage" />

   <f:section name="WholeContent">
      <div id="whole-content">
         <f:format.raw>{contentNormal}</f:format.raw>
      </div>
   </f:section>

   <f:section name="MainContent">
      <div id="main-content">
         <f:format.htmlentitiesDecode>{contentNormal}</f:format.htmlentitiesDecode>
      </div>
   </f:section>

   <f:section name="SideContent">
      <div id="side-content">
         <f:format.htmlentitiesDecode>{contentRight}</f:format.htmlentitiesDecode>
      </div>
   </f:section>

   <f:section name="PageHeader">
      <div id="page-header">
         <div id="navigation-top-level"><f:cObject typoscriptObjectPath="lib.topNavigation" /></div>
         <div id="navigation-trail">{f:cObject(typoscriptObjectPath:'lib.breadcrumbTrail')->f:format.raw()}</div>
      </div>
   </f:section>

   <f:section name="PageFooter">
      <div id="page-footer">
         <div id="footer-notice"> <p>This is the page footer area.</p> </div>
      </div>
   </f:section>

Notice the :html:`<f:layout>` element, which specifies which Fluid layout to
use with this Fluid template. The remaining elements in this file are
:html:`<f:section>` elements, not all of which will be used in this design.

Create a file named :file:`Layout1ColumnPage.html` in the
:file:`fileadmin/sitedesign/Resources/Private/Layouts` folder, and write the
following lines in the file:

.. code-block:: html

   <div id="page">
      <f:render section="PageHeader" />
      <div id="page-body">
         <div id="page-title">{data.title}</div>
         <f:render section="WholeContent" />
         <div id="page-body-end">&nbsp;</div>
      </div>
      <f:render section="PageFooter" />
   </div>

This design places subordinate elements into one Fluid template file, and
places overall layout elements into another file. Doing so allows editing and
access control advantages similar to the Fluid partials technique, but limits
potential file loading and processing times.

Switching Fluid layouts
=======================

This design switches between a single column layout and a double column layout.

In the TYPO3 CMS backend, create a standard page named
:name:`LayoutDoubleColumn` just under (inside) the :name:`Home` page. On the
:name:`LayoutDoubleColumn` standard page, create a TypoScript extension template.
In the TypoScript template Setup field, write the following lines::

   page = PAGE
   page.1 = FLUIDTEMPLATE
   page.1 {
      templateName = ForLayouts
      templateRootPaths.1 = fileadmin/sitedesign/Resources/Private/Templates
      layoutRootPath = fileadmin/sitedesign/Resources/Private/Layouts
      variables {
         contentNormal < styles.content.get
         contentRight < styles.content.get
         contentRight.select.where = {#colPos}=2
      }
   }

Notice the additional :ts:`contentRight` element, which obtains content
elements from the default named “Right” column position (#2) in a TYPO3 CMS
backend page. Also, notice that the Fluid template name has not changed.

Create a file named :file:`Layout2ColumnPage.html` in the
:file:`fileadmin/sitedesign/Resources/Private/Layouts` folder, and write the
following lines in the file:

.. code-block:: html

   <div id="page">
      <f:render section="PageHeader" />
      <div id="page-body">
         <div id="page-title">{data.title}</div>
         <f:render section="MainContent" />
         <f:render section="SideContent" />
         <div id="page-body-end">&nbsp;</div>
      </div>
      <f:render section="PageFooter" />
   </div>

Compare this layout to :file:`Layout1ColumnPage.html`. A couple
:html:`<f:section>` elements differ, but the overall design structure is
similar.

Now, edit the :file:`Templates/ForLayouts.html` file. Replace its
:html:`<f:layout name="Layout1ColumnPage" />` line with the following line.

.. code-block:: html

   <f:layout name="{settings.layout}" />

Edit the :name:`LayoutSingleColumn` page TypoScript template in the TYPO3 CMS
backend. Replace or edit its Setup field content to become the following::

   page = PAGE
   page.1 = FLUIDTEMPLATE
   page.1 {
      templateName = ForLayouts
      templateRootPaths.1 = fileadmin/sitedesign/Resources/Private/Templates
      layoutRootPath = fileadmin/sitedesign/Resources/Private/Layouts
      variables {
         contentNormal < styles.content.get
      }
      settings.layout = Layout1ColumnPage
   }

We only added a new :ts:`settings.layout` instruction.

Edit the :name:`LayoutDoubleColumn` page TypoScript template in the TYPO3 CMS
backend. Replace or edit its Setup field content to become the following::

   page = PAGE
   page.1 = FLUIDTEMPLATE
   page.1 {
      templateName = ForLayouts
      templateRootPaths.1 = fileadmin/sitedesign/Resources/Private/Templates
      layoutRootPath = fileadmin/sitedesign/Resources/Private/Layouts
      variables {
         contentNormal < styles.content.get
         contentRight < styles.content.get
         contentRight.select.where = {#colPos}=2
      }
      settings.layout = Layout2ColumnPage
   }

Here, too, we only added a new :ts:`settings.layout` instruction.

We now control which layout the :file:`ForLayouts.html` template uses through a
:ts:`settings.layout` element in the applicable TypoScript templates.

Alternatively, we could remove the :ts:`settings.layout` instruction from
the :name:`LayoutSingleColumn` and :name:`LayoutDoubleColumn` page TypoScript templates,
and add the following lines to the :name:`Home` page TypoScript template Setup
field. Keep the previously prepared library objects, :ts:`topNavigation`
and :ts:`breadcrumbTrail`, in place::

   page = PAGE
   page.1 = FLUIDTEMPLATE
   page.1.settings.layout = Layout1ColumnPage

We now need change only this one :ts:`settings.layout` value in this one
TypoScript template to affect all the subordinate pages.

If we wanted one design for a few pages and the other design for the rest, we
could modify the :name:`Home` page TypoScript template Setup field again. Edit or
add the following lines. Insert your own page UID values::

   page = PAGE
   page.1 = FLUIDTEMPLATE
   [page["uid"] in [2,4]]
      page.1.settings.layout = Layout2ColumnPage
   [ELSE]
      page.1.settings.layout = Layout1ColumnPage
   [END]

This TypoScript template *condition* snippet applies the double column page
layout if the current page has identifier 2 or 4, and applies the single
column page layout for any other current page.


A flexible page column design
=============================

Alternatively, we may want to use the double column page layout only if there
is side content to show. To do so, modify both the :name:`Home` page TypoScript
template and the :file:`Templates/ForLayouts.html` Fluid template.

In the :name:`Home` page TypoScript template Setup field, keep the previously
prepared library objects, :ts:`topNavigation` and
:ts:`breadcrumbTrail`, in place. However, remove any other instructions
you may have added. Then, add the following lines at the bottom of the Setup
field::

   lib.contentTest = TEXT
   lib.contentTest.value = 1
   lib.contentTest.if.isTrue.numRows {
      table = tt_content
      select {
         orderBy = sorting
         where = {#colPos}=2
      }
   }

In the :file:`Templates/ForLayouts.html` file, replace its
:html:`<f:layout name="Layout1ColumnPage" />` line with the following line.

.. code-block:: html

   <f:layout name="{f:if(condition: '{f:cObject(typoscriptObjectPath:\'lib.contentTest\')} == 1', then: 'Layout2ColumnPage', else: 'Layout1ColumnPage')}" />

This design tests for content in the TYPO3 backend page Right (#2) column
position; and if it finds such content, uses the double column layout.
Otherwise, it uses the single column layout.

Finally, make the design more efficient.

Delete the TypoScript template records from the :name:`LayoutSingleColumn` and
:name:`LayoutDoubleColumn` pages in the TYPO3 CMS backend. Edit the :name:`Home` page
TypoScript template by replacing all its Setup field content with the
following instructions::

   lib {
      topNavigation = HMENU
      topNavigation {
         1 = TMENU
         1.NO.linkWrap = | |*| &nbsp;&nbsp;&nbsp; |*|
      }
      breadcrumbTrail = HMENU
      breadcrumbTrail {
         special = rootline
         special.range = 0|-1
         1 = TMENU
         1.NO {
            stdWrap.field = nav_title // title
            ATagTitle.field = nav_title // title
            linkWrap = | |*| &nbsp;&raquo;&nbsp; |*|
         }
         1.CUR = 1
         1.CUR {
            doNotLinkIt = 1
            stdWrap.field = nav_title // title
            linkWrap = | |*| &nbsp;&raquo;&nbsp;<em>|</em>|
         }
      }
      contentTest = TEXT
      contentTest.value = 1
      contentTest.if.isTrue.numRows {
         table = tt_content
         select {
            orderBy = sorting
            where = {#colPos}=2
         }
      }
   }

   page = PAGE
   page.1 = FLUIDTEMPLATE
   page.1 {
      templateName = ForLayouts
      templateRootPaths.1 = fileadmin/sitedesign/Resources/Private/Templates
      layoutRootPath = fileadmin/sitedesign/Resources/Private/Layouts
      variables {
         contentNormal < styles.content.get
         contentRight < styles.content.get
         contentRight.select.where = {#colPos}=2
      }
   }

This design has one TypoScript template, one static TypoScript template, and
three Fluid files. The TypoScript template is on the :name:`Home` page. The static
template is :name:`Fluid Content Elements (fluid_styled_content)`. The
Fluid files are: :file:`Templates/ForLayouts.html`,
:file:`Layouts/Layout1ColumnPage.html`, and
:file:`Layouts/Layout2ColumnPage.html`.

This is an efficient, flexible design. The :name:`Home` page TypoScript template
sets up library objects and page parameters unlikely to change often. The
:file:`Templates/ForLayouts.html` Fluid template file chooses a page layout
and provides content sections for the layout. The resulting web page will
show side content if there is side content to be shown.

