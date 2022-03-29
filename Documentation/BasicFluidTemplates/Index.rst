.. include:: /Includes.rst.txt
.. highlight:: typoscript

.. _basic-fluid-templates:

=====================
Basic Fluid templates
=====================

Here, we intend to concentrate most design work in a single file at a time.


Prepare TypoScript
==================

First, in the TYPO3 CMS backend, create a standard page named :name:`Home`
just under (inside) the page tree TYPO3 logo container. On this standard page,
create a new TypoScript template record. Give the new TypoScript template a
title, make it a rootlevel template, and include the
:name:`Fluid Content Elements (fluid_styled_content)` static template. In
the TypoScript template Setup field, write the following lines::

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
   }

This TypoScript template provides the :name:`fluid_styled_content` static
template and two library objects, :ts:`topNavigation` and
:ts:`breadcrumbTrail`, to the :name:`Home` page and any of its subpages.

A single column page design
===========================

This design produces a basic web page having a header, one column for
content, and a footer. Each of the page sections has a uniquely identified
HTML :html:`<div>` tag, allowing for future stylesheet application.

In the TYPO3 CMS backend, create a standard page named :name:`SingleColumn`
just under (inside) the :name:`Home` page. On the :name:`SingleColumn` standard page,
create a TypoScript extension template. In the TypoScript template Setup
field, write the following lines::

   page = PAGE
   page.1 = FLUIDTEMPLATE
   page.1 {
      templateName = Basic1Column
      templateRootPaths.1 = fileadmin/sitedesign/Resources/Private/Templates
      variables {
         contentNormal < styles.content.get
      }
   }

This :name:`SingleColumn` page TypoScript template tells TYPO3 CMS the name of
the Fluid template and where to find it, using a slightly different syntax than
the :name:`Minimal design` page TypoScript template. Additionally, the
:name:`SingleColumn` TypoScript creates a :ts:`contentNormal` variable that
obtains all available content from the TYPO3 backend :name:`SingleColumn` page
Normal column.

Create a file named :file:`Basic1Column.html` in the
:file:`fileadmin/sitedesign/Resources/Private/Templates` folder, and write
the following lines in the file:

.. code-block:: html

   <div id="page">
      <div id="page-header">
         <div id="navigation-top-level">
            <f:cObject typoscriptObjectPath="lib.topNavigation" />
         </div>
         <div id="navigation-trail">
            {f:cObject(typoscriptObjectPath:'lib.breadcrumbTrail')->f:format.raw()}
         </div>
      </div>
      <div id="page-body">
         <div id="page-title">{data.title}</div>
         <div id="whole-content">
            <f:format.raw>{contentNormal}</f:format.raw>
         </div>
         <div id="page-body-end">&nbsp;</div>
      </div>
      <div id="page-footer">
         <div id="footer-notice">
            <p>This is the page footer area.</p>
         </div>
      </div>
   </div>

This :name:`SingleColumn` page Fluid template tells TYPO3 CMS how to assemble
an HTML :html:`<body>` element for output. Notice that the template does not
define the default markup seen in the minimal design resulting web page HTML
source.

Much of this :name:`SingleColumn` page Fluid template has typical HTML notation.
The :html:`f:` prefixed items denote the Fluid namespace and follow Fluid
rules. Examples here include :html:`<f:cObject />` (shown in tag notation) and
:html:`f:cObject()->f:format.raw()` (shown in inline notation). Fluid also
operates on the bracketed :html:`{…}` items, such as :html:`{contentNormal}`
and even the long :html:`{f:cObject…}` item in :html:`navigation-trail`. The
:html:`{data.title}` item here fetches the web page title from the
underlying repository.

A double column page design
===========================

This design produces a basic web page having a header, two columns for
content, and a footer.

In the TYPO3 CMS backend, create a standard page named :name:`DoubleColumn`
just under (inside) the :name:`Home` page. On the :name:`DoubleColumn` standard page,
create a TypoScript extension template record. In the TypoScript template
Setup field, write the following lines::

   page = PAGE
   page.1 = FLUIDTEMPLATE
   page.1 {
      templateName = Basic2ColumnPage
      templateRootPaths.1 = fileadmin/sitedesign/Resources/Private/Layouts
      variables {
         contentNormal < styles.content.get
         contentRight < styles.content.get
         contentRight.select.where = colPos = 2
      }
   }

This :name:`DoubleColumn` page TypoScript template tells TYPO3 CMS a different
location to find the Fluid template, and adds a :ts:`contentRight`
variable that obtains all available content from the TYPO3 backend
:name:`DoubleColumn` page Right column. The :ts:`contentNormal` variable will
obtain content from the :name:`DoubleColumn` page Normal column.

Create a file named :file:`Basic2ColumnPage.html` in a
:file:`fileadmin/sitedesign/Resources/Private/Layouts` folder, and write the
following lines in the file:

.. code-block:: html

   <div id="page">
      <div id="page-header">
         <div id="navigation-top-level"><f:cObject typoscriptObjectPath="lib.topNavigation" /></div>
         <div id="navigation-trail">{f:cObject(typoscriptObjectPath:'lib.breadcrumbTrail')->f:format.raw()}</div>
      </div>
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
      <div id="page-footer">
         <div id="footer-notice"> <p>This is the page footer area.</p> </div>
      </div>
   </div>

This :name:`DoubleColumn` page Fluid template puts :html:`contentNormal` and
:html:`contentRight` into separate :html:`<div>` elements, and uses
:html:`f:format.htmlentitiesDecode` instead of :html:`f:format.raw`.
