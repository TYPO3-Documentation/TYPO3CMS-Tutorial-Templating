.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../Includes.txt


.. _working-template:

Working with the HTML template
""""""""""""""""""""""""""""""


.. _shortinformation:

Short information about markers and subparts
********************************************

This section will tell you what markers and subparts are, how they look like and what they are used for.

A marker is a word in your HTML template, which is wrapped by "###" on both sides.
The marker "TITLE" would for example look like this:

.. code-block:: html

  <h1>###TITLE###</h1>

(Note that you may not insert markers inside HTML-comment-tags. They would not be replaced.)

TYPO3 will later replace the marker (that is the part "###TITLE###") with what you configured TYPO3 to put there. Everything around the marker will remain as it is.

In contrast a subpart is a pair of two markers in your HTML template, which have the same name. Between these two markers there may be some HTML code.

Example:

.. code-block:: html

  ###METANAV###
  <p>
    This is HTML code.
    It will be replaced by TYPO3, when we configure the subpart "METANAV".
  </p>
  ###METANAV###

Opposite to single markers (like "###TITLE###" from above) you may insert the subpart-markers inside HTML-comment-tags. That way they do not show up, when you open your template file in the browser. Inside the comment tag, you can also add other notes. In this tutorial we add the information, if it is the beginning or the end of the subpart like done in the next example.

Example:

.. code-block:: html

  <!-- ###METANAV### Start -->
  <p>
    This is HTML code.
    It will be replaced by TYPO3, when we configure the subpart "METANAV".
  </p>
  <!-- ###METANAV### End -->

TYPO3 will later replace the whole subpart (that is everything between and including the two markers "###METANAV###") with what you configured TYPO3 to put there. Everything around the subpart will remain as it is, everything in it will be replaced.

The name of markers and subparts is only important for TYPO3 to replace them. It does not have anything to do with the IDs or classes, which some HTML tags have, or with CSS styles, which are associated with these IDs or classes. However, you can use names for markers and subparts, which somehow fit to the IDs or classes, so that it is easier for you to remember, where which marker/subpart is used and for what.

.. hint::
   When you put your own markers and subparts in a template later, use short but meaningful marker names.


.. _open-template:

Open the HTML template
**********************

.. note::
   You can open and edit HTML files with any text editor. However, you will make your life much easier,
   if you use an editor, which supports syntax highlighting. With syntax highlighting you will see directly
   where a certain tag begins, where it ends, where there are attributes and so on.
   A very good editor with syntax highlighting is Notepad++, but there also are many others.
   Choose the one you like!

- In one of the last chapters you have copied the template files to the folder fileadmin/template/.

- Our HTML template is the file fileadmin/template/index.html. You will notice that this is just a normal HTML document. You can open it with your webbrowser and you will see the design.

- Open the HTML template with your text editor.


.. _add-marker-subparts:

Add markers/subparts
********************

We will now modify the HTML template by adding markers and subparts.
Later we will configure TYPO3 to replace each of them with the content we want (see the next chapter).


.. _add-subpart-document:

Add the subpart "DOCUMENT"
~~~~~~~~~~~~~~~~~~~~~~~~~~

Add a subpart called "DOCUMENT" inside the body tag. The first marker of this subpart should be directly behind the opening body tag and the second one directly in front of the closing body tag so that everything in the body tag is inside that subpart. TYPO3 will later create its own HTML structure for us and we will configure TYPO3 to only put the HTML code inside that structure, which is inside this subpart (and not also the head tag or the html tags or so). That is the reason, why we need it here.

.. code-block:: html

    <!DOCTYPE html>
    <html>
      <head>
        <title>
          Here is the title
        </title>
        <meta charset="utf-8" />
        <meta name="description" content="Here is a description" />
        <meta name="keywords" content="Some keywords regarding the content" />
        <meta name="audience" content="All" />
        <meta name="author" content="Sabine Hueber" />
        <meta name="publisher" content="..." />
        <meta name="Robots" content="index,follow" />
        <meta name="Language" content="English" />
        <meta name="revisit-after" content="1 Day" />
        <meta name="Content-Language" content="en" />

        <link href="style.css" rel="stylesheet" type="text/css" />
      </head>
      <body>
    <!--###DOCUMENT### Start-->
        <div id="page_margins">
          <div id="page" class="hold_floats">
            <div id="header">
              <!--###METANAV### Start-->
              <div id="metanav">
    <!-- The middle of the HTML document ist not shown here! -->
            <div id="footer">
               Design: Sabine&nbsp;Hueber,&nbsp;designeon
            </div>
    <!-- Footer Ende -->
          </div>
       </div>
    <!--###DOCUMENT### end-->
      </body>
    </html>


.. _subpart-metanav:

Add the subpart "METANAV"
~~~~~~~~~~~~~~~~~~~~~~~~~

Inside the div box with the id "metanav" there is our metanavigation.
Add a subpart called "METANAV", so that the whole content of that box is inside the subpart.

.. code-block:: html

    <body>
        <!-- ###DOCUMENT### Start -->
        <div id="page_margins">
            <div id="page" class="hold_floats">

                <div id="header">

                    <div id="metanav">
                        <!-- ###METANAV### Start -->
                        <ul>
                           <li><a>Contact</a></li>
			   <li><a>Imprint</a></li>
                        </ul>
                        <!-- ###METANAV### End -->
                    </div>


.. _marker-title:

Add the marker "HEADERTITLE"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Below the metanavigation there is a div with the id "headertitle".
Replace its content with the marker "HEADERTITLE".

.. code-block:: html

  <div id="headertitle">###HEADERTITLE###</div>


.. _subpart-topnav:

Add the subpart "TOPNAV"
~~~~~~~~~~~~~~~~~~~~~~~~

Inside the div, which has the id "nav", we have our mainnavigation.
Do the same as for "metanav" but call that subpart "TOPNAV".

.. code-block:: html

	<div id="nav">
		<!-- ###TOPNAV### Start -->
			<div id="nav_main">
				<ul>
					<li><a>Menu Item 1</a></li>
					<li><a>Menu Item 2</a></li>
					<li id="current"><a>Menu Item 3</a></li>
					<li><a>Menu Item 4</a></li>
				</ul>
			</div>
		<!-- ###TOPNAV### End -->
	</div>


.. _col1-subpart:

Column 1: Add the subpart "SUBNAV"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As you might already have seen the template has three columns.

- Let's begin with the left column, column 1, which has the id "col1".

  - Inside of column 1 there is the div with the id "col1_content".
    It will hold the sub menu. Wrap the whole content of that div in the subpart "SUBNAV".

.. code-block:: html

    <!-- #col1: Left Column of the Content Area -->
    <div id="col1">
        <div id="col1_content" class="clearfix">
            <!-- ###SUBNAV### Start -->
            <ul id="submenu">
                <li><a >Submenu Item 1</a></li>
                <li id="active"><a>Submenu Item 2</a></li>
                <li>Submenu Item 3
                    <ul>
                        <li><a>Subitem 1</a></li>
                        <li><a>Subitem 2</a></li>
                    </ul>
                </li>
                <li><a>Submenu Item 4</a></li>
            </ul>
            <!-- ###SUBNAV### End -->
        </div>
    </div>
    <!-- #col1: Left Column End -->


.. _col2-subpart:

Column 2: Add the subpart "CONTENTRIGHT"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Column 2, the div with the id "col2" is the right column of our layout.

  - In the div below there will be the content of that column.
    Wrap the content of that div into the subpart "CONTENTRIGHT".

A screenshot follows after we added the markers and subparts of column 3.


.. _col3-markers:

Column 3: Add the markers "DATE", "BREADCRUMB" and "TITLE" and the subpart "CONTENTMIDDLE"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Column 3, the div with the id "col3" is the column, which will be displayed in the middle.
  In our layout it is the main content area.

  - Inside the div with the id "breadcrumb" replace the date with a marker called "DATE"
    and the rootline with a marker called "BREADCRUMB".

  - Next there is the page title. Replace the content of the h1 tag with the marker "TITLE".

  - In the div below there will be the content of that column. Wrap the content of that div
    into the subpart "CONTENTMIDDLE".

.. code-block:: html

    <!-- #col2: Right Column of the Content Area -->
    <div id="col2">
        <div id="col2_content" class="clearfix">
            <div>
                <!-- ###CONTENTRIGHT### Start -->
                <h2>Right Column - Only Element</h2>
                <p>Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod
                    tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At
                    vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren,
                    no sea takimata sanctus est Lorem ipsum dolor sit amet.</p>
                <!-- ###CONTENTRIGHT### End -->
            </div>
        </div>
    </div>
    <!-- #col2: Right Column End -->

    <!-- #col3:  Middle Column of the Content Area -->
    <div id="col3">
        <div id="col3_content" class="clearfix">
            <div id="breadcrumb">###DATE###&nbsp;:::&nbsp;###BREADCRUMB###</div>
            <h1>###TITLE</h1>
            <div>
                <!-- ###CONTENTMIDDLE### Start -->
                <h2>Middle Column - Element 1</h2>
                <p>Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod
                    tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At
                    vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren,
                    no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit
                    amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut
                    labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam
                    et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata
                    sanctus est Lorem ipsum dolor sit amet.</p>
                <h2>Middle Column - Element 2</h2>
                <p>Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod
                    tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At
                    vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren,
                    no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit
                    amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut
                    labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam
                    et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata
                    sanctus est Lorem ipsum dolor sit amet.</p>
                <!-- ###CONTENTMIDDLE### End -->
            </div>
        </div>
    </div>
    <!-- #col3: Middle Column End -->


This completes the changes, which we had to make in the HTML template.


.. _working-template-result:

Result
~~~~~~

This is how our HTML template now looks like:

.. code-block:: html

    <!DOCTYPE html>

    <html>
        <head>
            <title>Here goes the title</title>
            <meta charset="utf-8" />
            <meta name="description" content="Here goes a description" />
            <meta name="keywords" content="Some keywords regarding the content" />
            <meta name="audience" content="All" />
            <meta name="author" content="Sabine Hueber" />
            <meta name="publisher" content="..." />
            <meta name="Robots" content="index,follow" />
            <meta name="Language" content="English" />
            <meta name="revisit-after" content="1 Day" />
            <meta name="Content-Language" content="en" />

            <link href="style.css" rel="stylesheet" type="text/css" />
        </head>

        <body>
            <!-- ###DOCUMENT### Start -->
            <div id="page_margins">
                <div id="page" class="hold_floats">

                    <div id="header">

                        <div id="metanav">
                            <!-- ###METANAV### Start -->
                            <ul>
                                <li><a>Contact</a></li>
                                <li><a>Imprint</a></li>
                            </ul>
                            <!-- ###METANAV### End -->
                        </div>

                        <div id="headertitle">###HEADERTITLE###</div>
                    </div>


                    <div id="nav">
                        <!-- ###TOPNAV### Start -->
                        <div id="nav_main">
                            <ul>
                                <li><a>Menu Item 1</a></li>
                                <li><a>Menu Item 2</a></li>
                                <li id="current"><a>Menu Item 3</a></li>
                                <li><a>Menu Item 4</a></li>
                            </ul>
                        </div>
                        <!-- ###TOPNAV### End -->
                    </div>


                    <!-- 3 Column Content -->


                    <!-- #col1: Left Column of the Content Area -->
                    <div id="col1">
                        <div id="col1_content" class="clearfix">
                            <!-- ###SUBNAV### Start -->
                            <ul id="submenu">
                                <li><a>Submenu Item 1</a></li>
                                <li id="active"><a>Submenu Item 2</a></li>
                                <li><a>Submenu Item 3</a>
                                    <ul>
                                        <li><a>Subitem 1</a></li>
                                        <li><a>Subitem 2</a></li>
                                    </ul>
                                </li>
                                <li><a>Submenu Item 4</a></li>
                            </ul>
                            <!-- ###SUBNAV### End -->
                        </div>
                    </div>
                    <!-- #col1: Left Column End -->

                    <!-- #col2: Right Column of the Content Area -->
                    <div id="col2">
                        <div id="col2_content" class="clearfix">
                            <div>
                                <!-- ###CONTENTRIGHT### Start -->
                                <h2>Right Column - Only Element</h2>
                                <p>Lorem ipsum dolor sit amet, consetetur sadipscing elitr,
                                    sed diam nonumy eirmod tempor invidunt ut labore et
                                    dolore magna aliquyam erat, sed diam voluptua. At vero
                                    eos et accusam et justo duo dolores et ea rebum. Stet
                                    clita kasd gubergren, no sea takimata sanctus est Lorem
                                    ipsum dolor sit amet.</p>
                                <!-- ###CONTENTRIGHT### End -->
                            </div>
                        </div>
                    </div>
                    <!-- #col2: Right Column End -->

                    <!-- #col3:  Middle Column of the Content Area -->
                    <div id="col3">
                        <div id="col3_content" class="clearfix">
                            <div id="breadcrumb">###DATE###&nbsp;:::&nbsp;###BREADCRUMB###</div>
                            <h1>###TITLE</h1>
                            <div>
                                <!-- ###CONTENTMIDDLE### Start -->
                                <h2>Middle Column - Element 1</h2>
                                <p>Lorem ipsum dolor sit amet, consetetur sadipscing elitr,
                                    sed diam nonumy eirmod tempor invidunt ut labore et
                                    dolore magna aliquyam erat, sed diam voluptua. At vero
                                    eos et accusam et justo duo dolores et ea rebum. Stet
                                    clita kasd gubergren, no sea takimata sanctus est Lorem
                                    ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur
                                    sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut
                                    labore et dolore magna aliquyam erat, sed diam voluptua. At
                                    vero eos et accusam et justo duo dolores et ea rebum. Stet
                                    clita kasd gubergren, no sea takimata sanctus est Lorem ipsum
                                    dolor sit amet.</p>
                                <h2>Middle Column - Element 2</h2>
                                <p>Lorem ipsum dolor sit amet, consetetur sadipscing elitr,
                                    sed diam nonumy eirmod tempor invidunt ut labore et
                                    dolore magna aliquyam erat, sed diam voluptua. At vero
                                    eos et accusam et justo duo dolores et ea rebum. Stet
                                    clita kasd gubergren, no sea takimata sanctus est Lorem
                                    ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur
                                    sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut
                                    labore et dolore magna aliquyam erat, sed diam voluptua. At
                                    vero eos et accusam et justo duo dolores et ea rebum. Stet
                                    clita kasd gubergren, no sea takimata sanctus est Lorem ipsum
                                    dolor sit amet.</p>
                                <!-- ###CONTENTMIDDLE### End -->
                            </div>
                        </div>
                    </div>
                    <!-- #col3: Middle Column End -->

                    <!-- IE Column Clearing -->
                    <div id="ie_clearing">&nbsp;</div>
                    <!-- IE Column Clearing End -->


                    <!-- 3 Column Content End -->


                    <!-- Footer Start -->
                    <div id="footer">
                        Design: <a>Sabine&nbsp;Hueber,&nbsp;designeon</a>
                    </div>
                    <!-- Footer End -->

                </div>
            </div>
            <!-- ###DOCUMENT### End -->
        </body>
    </html>

