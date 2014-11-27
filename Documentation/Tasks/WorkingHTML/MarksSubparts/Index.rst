.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


.. _open-template:

Open the HTML template
**********************

.. note::

   You can open and edit HTML files with any text editor. However, you will make your life much easier,
   if you use an editor, which supports syntax highlighting. With syntax highlighting you will see directly
   where a certain tag begins, where it ends, where there are attributes and so on.

   If you don't already have one of these, a quick search on Internet will turn up
   a lot of them and you should be able to find one which runs on your computer
   and with which you are comfortable.


- In one of the previous chapters you have copied the template files
  from :file:`/typo3conf/ext/doc_tut_templating/Resources/Private/Template`
  to :file:`fileadmin/template/`.

- Our HTML template is the file :file:`fileadmin/template/index.html`.
  You will notice that this is just a normal HTML document.
  You can open it with your web browser and see the design.

  .. tip::

     Do not use :file:`index-with-markers.html` which is the finished result,
     with all marks and subparts. You can check it out when you're done to validate
     your work, but using it right away would spoil your learning process.

- Open the HTML template with your text editor.


.. _add-marker-subparts:
.. _add-marks-subparts:

Add marks/subparts
******************

We will now modify the HTML template by adding marks and subparts.
Later we will configure TYPO3 to replace each of them with the content we want (see the next chapter).


.. _add-subpart-document:

Add the subpart "DOCUMENT"
~~~~~~~~~~~~~~~~~~~~~~~~~~

Add a subpart called "DOCUMENT" inside the body tag. Remember that subparts come in pairs.
Hence the first marker of this subpart should be directly behind the opening :code:`<body>` tag
and the second one directly in front of the closing :code:`<body>` tag so that
everything in the :code:`<body>` tag is inside that subpart.
TYPO3 CMS will later recreate its own HTML structure for us and we will configure TYPO3 CMS
to only put the HTML code inside that structure, which is inside this subpart
(all tags "outide" the two ###DOCUMENT### markers, i.e., :code:`<html>`,
:code:`<head>`, :code:`<title>`, :code:`<meta />`, :code:`<link>` and :code:`<body>`
will not be influenced). That is the reason, why we need it here.

.. code-block:: html
   :emphasize-lines: 14,38

	<!DOCTYPE html>
	<html>
		<head>
			<title>
				Here is the title
			</title>
			<meta charset="utf-8" />
			...
			<meta name="Content-Language" content="en" />

			<link href="style.css" rel="stylesheet" type="text/css" />
		</head>
		<body>
			<!--###DOCUMENT### Start-->
				<div id="page_margins">
					<div id="page" class="hold_floats">

						<div id="header">

							<div id="metanav">
								<ul>
									<li><a href="#">Contact</a></li>
									<li><a href="#">Imprint</a></li>
								</ul>
							</div>

							<div id="headertitle">TYPO3</div>
						</div>
						...
						<!-- Footer Start -->
						<div id="footer">
							Design: <a href="http://www.designeon.de">Sabine&nbsp;Hueber,&nbsp;designeon</a>
						</div>
						<!-- Footer End -->

					</div>
				</div>
			<!--###DOCUMENT### end-->
		</body>
	</html>


.. _subpart-metanav:

Add the subpart "METANAV"
~~~~~~~~~~~~~~~~~~~~~~~~~

Inside the div box with the id "metanav" comes the navigation
to some special pages. Add a subpart called "METANAV",
so that the whole content of that box is inside the subpart.
This is exactly the same process as the previous exercise.

.. code-block:: html
   :emphasize-lines: 9,14

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
						...


.. _marker-title:
.. _mark-title:

Add the mark "HEADERTITLE"
~~~~~~~~~~~~~~~~~~~~~~~~~~

Below the meta-navigation there is a div with the id "headertitle".
Replace its content with the mark "HEADERTITLE". Remember that marks
use a single marker, not a pair of them.

.. code-block:: html

	<div id="headertitle">###HEADERTITLE###</div>


.. _subpart-topnav:

Add the subpart "TOPNAV"
~~~~~~~~~~~~~~~~~~~~~~~~

Inside the div, which has the id "nav", we have our main navigation.
Do the same as for "metanav" but call that subpart "TOPNAV".

.. code-block:: html
   :emphasize-lines: 2,11

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

As you might already have noticed the template has three columns.

- Let's begin with the left column, column 1, which has the id "col1".

  - Inside of column 1 there is the div with the id "col1_content".
    It will hold the submenu. Wrap the whole content of that div in the subpart "SUBNAV".

.. code-block:: html
   :emphasize-lines: 4,16

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

The result is shown after adding the marks and subparts of column 3
in the next section.


.. _col3-markers:

Column 3: Add the marks "DATE", "BREADCRUMB" and "TITLE" and the subpart "CONTENTMIDDLE"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Column 3, the div with the id "col3", is the column, which will be displayed in the middle.
  In our layout it is the main content area.

  - Inside the div with the id "breadcrumb" replace the date with a mark called "DATE"
    and the rootline with a mark called "BREADCRUMB".

  - Next there is the page title. Replace the content of the :code:`<h1></h1>` tag with the mark "TITLE".
    This was demonstrated at the beginning of this chapter.

  - In the div below there will be the content of that column. Wrap the content of that div
    into the subpart "CONTENTMIDDLE".

.. code-block:: html
   :emphasize-lines: 5,11,20,21,23,42

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

