.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../Includes.txt


.. _working-template:

Working with the HTML template
""""""""""""""""""""""""""""""


.. _shortinformation:

A quick explanation on markers and subparts
********************************************

This section will tell you what markers and subparts are, what they look like and what they are used for.

A marker is a word in your HTML template, which is wrapped in three hash tags (###) on either side.
It is very important to understand the difference between a marker and a subpart. Markers come in "singles" whereas subparts come in "pairs".
In a more everyday way of saying it, markers are "loners", and subparts are "couples".
The marker "TITLE" would for example look like this:

.. code-block:: html

  <h1>###TITLE###</h1>

Notice how it comes alone without any other marker. This is different from the subpart as we will see soon.
An important characteristic of a marker is that one CANNOT insert them inside HTML comment tags (comment tags are allowed with a subpart). This is important to remember, for, if you do wrap a marker (NOT a subpart) in HTML comment tags, it will not be replaced. 
Here is an example of what CANNOT be done with a marker in the HTML template file:
.. code-block:: html

(THIS CANNOT BE DONE WITH A MARKER).
  <!-- ###TITLE### --> 
  
So, with our marker properly tagged and inserted, TYPO3 will later replace it (<h1>###TITLE###</h1>) with what you configured TYPO3 to put there. Everything around the marker (above and below) will remain untouched by it.

Markers work in "singles". In contrast, subparts work in "pairs" in your HTML template. Subparts look just like markers for, they actually are two markers that work together. Yet, when they work together they function differently and have some different characteristics. 
Let´s see two of them. First, HTML code can be added in between the two markers that make up the subpart. Notice how the <p> </p> tags are being used between the two ###METANAV### markers. 
(NOTE: Remember -- a subpart is the two ###METANAV### markers and all that comes between.)
Example:

.. code-block:: html

  ###METANAV###
  <p>
    This is HTML code.
    It will be replaced by TYPO3, when we configure the subpart "METANAV" in the backend.
  </p>
  ###METANAV###

Another characteristic of subparts is they can be inserted in HTML comment tags (remember, this cannot be done with markers). 
That way they do not show up, when you open your template file in the browser and still do their work with TYPO3. Inside the comment tag, you can also add other notes. 
In this tutorial we add the information to show which is the "opening" marker and which is the "closing" marker for the subpart. In the following example, we use the word "Start" to indicate the opening marker and the word "End" to indicate the closing marker.

Example:

.. code-block:: html

  <!-- ###METANAV### Start -->
  <p>
    This is HTML code.
    It will be replaced by TYPO3, when we configure the subpart "METANAV".
  </p>
  <!-- ###METANAV### End -->

Here is how it works. The two ###METANAV### markers, in the  <!-- ###METANAV### Start --> and <!-- ###METANAV### End --> subpart and everything that comes between them are what TYPO3 will replace. 
Everything outside (above and below) the subpart will remain as it is. The comment tags (<!--  -->) help hide the markers so that they won´t show up on our website page. The "Start" and "End" parts are only there to help us keep our bearings with which marker is which in the subpart.

A question that often arises on markers and subparts is how to name them. The fact is, you can create or invent the names. The important thing is that TYPO3 will know how to replace them (more on this up ahead). There is going to be an interplay, or communication, between the markers and the subparts in the HTML template file and TYPO3. 
Markers and subparts have nothing to do with IDs or classes, which some HTML tags have, or with CSS styles, which are associated with these IDs or classes. However, you can use names for markers and subparts, which somehow fit the IDs or classes, so that it is easier for you to remember (where which marker or subpart is used and for what).

.. hint::
   Create relevant, meaningful and short marker and subpart names in your templates. 

.. _open-template:

Open the HTML template
**********************

.. note::
   It is possible to use any text editor to edit HTML files. However, it is recommended that you use an editor which supports syntax highlighting. 
   With syntax highlighting you will see directly where a certain tag begins and ends, where there are attributes among other things.
   For Linux users, there is a large amount of these editors. According to your GUI (KDE, GNOME, Xfce, etc.) you can find the one appropriate to you in your package manager: kwrite, kate, gedit, Emacs, vim-gnome, vim-gtk, bluefish, etc.
   A very good MS Windows editor with syntax highlighting is Notepad++, but there also are many others.
   For Mac OSX, there are Brackets, Textmate, and TextWrangler, just to mention a few. Of course, there may be many others.
   Some text editors can be used in all three operating systems (called multi-platform) such as different vim and emacs versions.
   Another tool that can be used is an online text editor. Many internet hosting companies offer this.
   The important thing is to choose the one you like best! A little research on the internet will give you a very long and big list of possibilities.

- In one of the previous chapters we copied the template files from /typo3conf/ext/doc_tut_templating/Resources/Private/Template to the folder fileadmin/template/.

- Our HTML template is the file fileadmin/template/index.html. You will notice that this is just a normal HTML document. You can open it with your web browser and you see the design. There are two versions, index.html and index-with-markers.html. It would be best if you chose index.html so you can learn and look at index-with-markers.hmtl to compare what you have done.

- Open the HTML template with your text editor.


.. _add-marker-subparts:

Add markers/subparts
********************

We will now modify the HTML template by adding markers and subparts.
Later we will configure TYPO3 to replace each of them with the content we want (see the next chapter).


.. _add-subpart-document:

Add the subpart "DOCUMENT"
~~~~~~~~~~~~~~~~~~~~~~~~~~

Add a subpart called "DOCUMENT" inside the body tag (remember, subparts come in pairs). The first marker of this subpart should be directly behind the opening body tag and the second one directly in front of the closing body tag so that everything in the body tag is inside that subpart. TYPO3 will later recreate its own HTML structure for us and we will configure TYPO3 to only put the HTML code inside that structure, which is inside this subpart (all tags "outide" the two ###DOCUMENT### markers, i.e., <html>, <head>, <title>, <meta />, <link> and <body> will not be influenced). That is the reason, why we need it here.

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
            .......................
              <!--###METANAV### Start-->
              <div id="metanav">
    <!-- The middle of the HTML document ist not shown here! -->
            <div id="footer">
               Design: Sabine&nbsp;Hueber,&nbsp;designeon
            </div>
    <!-- Footer Ende -->
          </div>
       </div>
            .......................
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
            .......................

.. _marker-title:

Add the marker "HEADERTITLE"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Below the metanavigation there is a div with the id "headertitle".
Replace its content with the marker "HEADERTITLE". Remember that a "marker" works alone, i.e., it is "single" and there won´t be a second ###HEADERTITLE###.

.. code-block:: html

  <div id="headertitle">###HEADERTITLE###</div>


.. _subpart-topnav:

Add the subpart "TOPNAV"
~~~~~~~~~~~~~~~~~~~~~~~~

Inside the div, which has the id "nav", we have our main navigation.
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

As you might already have noticed, the template has three columns.

- Let's begin with the left column, column 1, which has the id "col1".

  - Inside of column 1 there is the div with the id "col1_content".
    It will hold the submenu. Wrap the whole content of that div in the subpart "SUBNAV".

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

- Column 2, the div with the id "col2", is the right column of our layout.

  - In the div below there will be the content of that column.
    Wrap the content of that div into the subpart "CONTENTRIGHT".

A screenshot follows after we added the markers and subparts of column 3.


.. _col3-markers:

Column 3: Add the markers "DATE", "BREADCRUMB" and "TITLE" and the subpart "CONTENTMIDDLE"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Column 3, the div with the id "col3", is the column which will be displayed in the middle.
  In our layout, it is the main content area.

  - Inside the div with the id "breadcrumb" replace the date with a marker called "DATE"
    and the rootline with a marker called "BREADCRUMB".

  - Next there is the page title. Replace the content of the <h1> </h1> tag with the marker "TITLE" This was demonstrated at the beginning of this chapter.

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

