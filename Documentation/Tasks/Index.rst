.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../Includes.txt

.. _task:

Task
^^^^

.. note::
   This is a step by step instruction like a cooking recipe. It must be a logical thread from start to end divided steps. It gives additional information (but not to much!) and warns for difficult situation (e.g. data loss). After several steps a result may be well. The task end must be identifiable by a result.

In this tutorial we use the most common approach for building a website with TYPO3: We take one HTML file, which we call our HTML template. It will be used as a basis for the website. TYPO3 will use this file as a basis, but certain parts of this file will be replaced with the content, which you have in your TYPO3 installation. To tell TYPO3, which parts it should replace, we will modify the HTML template now. Inside the HTML template we will add so called markers and subparts. 

In a later chapter we will configure TYPO3 to replace these markers and subparts with the content, which has been inserted in TYPO3.

.. _working-template

Working with the HTML template
""""""""""""""""""""""""""""""

.. _shortinformation

Short information about markers and subparts
********************************************

This section will tell you what markers and subparts are, how they look like and what they are used for.

A marker is a word in your HTML template, which is wrapped by "###" on both sides. The marker "TITLE" would for example look like this: 

::

  <h1>###TITLE###</h1>

(Note that you may not insert markers inside HTML-comment-tags. They would not be replaced.)

TYPO3 will later replace the marker (that is the part "###TITLE###") with what you configured TYPO3 to put there. Everything around the marker will remain as it is.

In contrast a subpart is a pair of two markers in your HTML template, which have the same name. Between these two markers there may be some HTML code.

Example:

::

  ###METANAV###
  <p>
    This is HTML code.
    It will be replaced by TYPO3, when we configure the subpart "METANAV".
  </p>
  ###METANAV###

Opposite to single markers (like "###TITLE###" from above) you may insert the subpart-markers inside HTML-comment-tags. That way they do not show up, when you open your template file in the browser. Inside the comment tag, you can also add other notes. In this tutorial we add the information, if it is the beginning or the end of the subpart like done in the next example.

Example:

::

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

.. _open-template
   
Open the HTML template
**********************

.. note::
   You can open and edit HTML files with any text editor. However, you will make your life much easier, if you use an editor, which supports syntax highlighting. With syntax highlighting you will see directly where a certain tag begins, where it ends, where there are attributes and so on. A very good editor with syntax highlighting is Notepad++, but there also are many others. Choose the one you like!

* In one of the last chapters you have copied the template files to the folder fileadmin/template/.
* Our HTML template is the file fileadmin/template/index.html. You will notice that this is just a normal HTML document. You can open it with your webbrowser and you will see the design.
* Open the HTML template with your text editor.

.. _add-marker-subparts

Add markers/subparts
********************

We will now modify the HTML template by adding markers and subparts. Later we will configure TYPO3 to replace each of them with the content we want (see the next chapter).

.. _add-subpart-document

Add the subpart "DOCUMENT"
~~~~~~~~~~~~~~~~~~~~~~~~~~

Add a subpart called "DOCUMENT" inside the body tag. The first marker of this subpart should be directly behind the opening body tag and the second one directly in front of the closing body tag so that everything in the body tag is inside that subpart. TYPO3 will later create its own HTML structure for us and we will configure TYPO3 to only put the HTML code inside that structure, which is inside this subpart (and not also the head tag or the html tags or so). That is the reason, why we need it here.

::

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

.. _subpart-metanav

Add the subpart "METANAV"
~~~~~~~~~~~~~~~~~~~~~~~~~

* Inside the div box with the id "metanav" there is our metanavigation. Add a subpart called "METANAV", so that the whole content of that box is inside the subpart.

::
 
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

.. _marker-title

Add the marker "HEADERTITLE"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Below the metanavigation there is a div with the id "headertitle". Replace its content with the marker "HEADERTITLE".

:: 

  <div id="headertitle">###HEADERTITLE###</div>

.. _subpart-topnav
  
Add the subpart "TOPNAV"
~~~~~~~~~~~~~~~~~~~~~~~~

* Inside the div, which has the id "nav", we have our mainnavigation. Do the same as for "metanav" but call that subpart "TOPNAV".

::

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

.. _col1-subpart

Column 1: Add the subpart "SUBNAV"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As you might already have seen the template has three columns.
* Let's begin with the left column, column 1, which has the id "col1".
** Inside of column 1 there is the div with the id "col1_content". It will hold the sub menu. Wrap the whole content of that div in the subpart "SUBNAV".

::  

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

.. _col2-subpart

Column 2: Add the subpart "CONTENTRIGHT"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Column 2, the div with the id "col2" is the right column of our layout.
** In the div below there will be the content of that column. Wrap the content of that div into the subpart "CONTENTRIGHT".

A screenshot follows after we added the markers and subparts of column 3.

.. _col3-markers

Column 3: Add the markers "DATE", "BREADCRUMB" and "TITLE" and the subpart "CONTENTMIDDLE"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Column 3, the div with the id "col3" is the column, which will be displayed in the middle. In our layout it is the main content area.
** Inside the div with the id "breadcrumb" replace the date with a marker called "DATE" and the rootline with a marker called "BREADCRUMB".
** Next there is the page title. Replace the content of the h1 tag with the marker "TITLE".
** In the div below there will be the content of that column. Wrap the content of that div into the subpart "CONTENTMIDDLE".

::
 
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

.. _desired-task

The desired task result
~~~~~~~~~~~~~~~~~~~~~~~

This is how our HTML template now looks like:

:: 

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

.. _working-with-typoscript

Working with the TypoScript template record
"""""""""""""""""""""""""""""""""""""""""""

In the last steps, we have worked in the HTML template. Now we will work at another place. We will now work in the TYPO3 Backend. There we will create a TypoScript template and configure it as we need it.

.. _typoscript-template

TypoScript template records - a brief introduction
**************************************************

A TypoScript template is a record that contains the configuration information used to display content in a website; the frontend. It is written using the TypoScript scripting language. The templates are edited in the "Web" section of the TYPO3 backend and are stored in the database in the sys_template table.

Typoscript can be used to control nearly everything in the frontend, for example the doctype, the meta data in the header element of your website, the display of content inside the body tag and even each single rendering instruction, which TYPO3 uses internally to display your content elements.

For more information on the options available in TypoScript template records see the TypoScript reference, TSref.

.. _create-ts-template

Create a new TypoScript template
********************************

Let's start building our TypoScript template. Go to the Template module by opening the section "Web" and clicking on "Template":


.. figure:: ../Images/Images/Image:TBT-template-module.jpg
   :alt:

You cannot see the Template module?
The Template module is only accessible for administrators in TYPO3. Login with an administrator account and you will be able to see and use it.

In the page tree activate the "Root" page, which you have created before you worked in the HTML template file. You will see this screen:

.. figure:: ../Images/Images/Image:TBT-template-new.jpg
   :alt:

As you can see, there currently is no TypoScript record on our root page. So we have to create one, so that TYPO3 knows, how it should dispay our root page - and also all its subpages - in our website. Note that the template record is inherited to all subpages. That means that the configuration, which we insert in the template record of our root page, will automatically be used for all subpages as well.
To create a new template record click on "Create template for a new site".

.. figure:: ../Images/Images/Image:TBT-template-new2.jpg
   :alt:

After you have done so, you will come to the same screen, but there will additionally be the information, that there now is a template record on the page "Root" (with the id, which this page has in your system. In my case it is 75, but the ID does not matter now.). Click the link "Click here to go."

.. figure:: ../Images/Images/Image:TBT-template-new3.jpg
   :alt:

Now you see the "Info/Modify" screen. From here you can edit the whole template record or choose one single field of the record, which you want to view or change.

.. figure:: ../Images/Images/Image:TBT-template-new4.jpg
   :alt:

First there is one important step, which we need to do: There is a so called "static template", which comes with TYPO3. This static template already contains some TypoScript code. If we include this static template in our template record, it will help us, as we do not have to write each line of the code we need ourselves. Instead we can use a short one-liner to copy parts from this static template. (This is done when we insert the actual content for the markers CONTENTRIGHT and CONTENTMIDDLE).

Click the button "Edit whole template record".

.. figure:: ../Images/Images/Image:TBT-template-include-static1.jpg
   :alt:

Click the tab "Includes" and in the palette "Include static (from extensions)" click the item "CSS Styled Content (css_styled_content)" as marked in the screenshot. Then it will be added to the list on the left. When that is done click the icon "Save and close document" at the top.

.. figure:: ../Images/Images/Image:TBT-template-include-static2.jpg
   :alt:

You do not see the entry "CSS Styled Content (css_styled_content)" in the right list? Then you most probably have not installed the TYPO3 system extension "css_styled_content". Go to the Extension Manager, open the tab "Available extensions", watch out for the extension key "css_styled_content" and install the extension. Now include the static template as explained above.

You now are back in the Info/Modify screen. Here you can see some sections of the TypoScript template. The most important sections in a TypoScript template are the ones called "Constants" and "Setup". 

.. figure:: ../Images/Images/Image:TBT-template-new4a.jpg
   :alt:

In the section "Constants" you can - you guess it - define constants. These constants can then be used in the setup field of the template. Doing so is a bit more advanced and we will not do that in this tutorial.
The field labeled "Setup" is the one, in which we will enter all the TypoScript configuration. As you can see in the screenshot above, it already contains six lines of code. Click the small pencil next to the word "Setup".

.. figure:: ../Images/Images/Image:TBT-template-new4b.jpg
   :alt:

Now you can have a look at the content of the setup field. This is what you will see:

.. figure:: ../Images/Images/Image:TBT-template-new5.jpg
   :alt:

You don't see the code in different colors, but just as black text? Then you most probably have not installed the TYPO3 system extension "t3editor". You can install this extension by going to the Extension Manager, having a look at the tab "Available extensions" and by clicking the small icon in front of the row where it says "t3editor". Afterwards you should be able to see the code colored as in the screenshot above. If you still do not see the code colored, make sure that you have not checked the checkbox "Deactivate t3editor", which you see at the bottom of the above screenshot.

.. note::
   The t3editor helps with syntax-highlighting, but keep in mind, that if you use extensions, the t3editor does not know about valid properties. So, if something is not highlighted it does not mean that it is wrong - if something is highlighted, it does not mean, that it is right. If something does not work like expected read the relevant manuals.}}

.. _how-to-use

How to use TSref
****************

Before we continue to write our own TypoScript, let us have a look at the lines, which already are there.

::

    # Default PAGE object:
    page = PAGE
    page.10 = TEXT
    page.10.value = HELLO WORLD!

Did you read the Tutorial TypoScript in 45 Minutes? If you did, you should already know, what these lines are doing.
To remind you, here is a short explanation. We will also use this explanation to repeat (or to learn) how to use TSref!

You do not have a copy of TSref currently? TSref, the TypoScript reference, is available from TYPO3 TER, which is here: http://typo3.org/extensions/repository/ Search for the keyword "doc_core_tsref". This is the "extension key", under which the documentation is published. The extension doc_core_tsref contains a PDF file, which you can download from TER. Use it to conveniently look things up.

* Lines starting with "#" are comments. You can use them to comment your code. They are not parsed, when TYPO3 reads the template to render the website.
* In the next line the object "page" is defined and set to the value "PAGE". This value refers to a "page object". Have a look at the section "Setup" in TSref (remember that we are editing the "Setup" field). In the table with the headline "Top-level objects" you will find information about the objects, which can be set on the first level of TypoScript templates. One of them is called "PAGE". The definition of this PAGE object tells TYPO3 that it should start the output of a new page. As you see in TSref, the data type of this object is "->PAGE". This tells you that you should look into the table with the headline "PAGE", to see the configuration options for the PAGE object. This table follows some pages later in TSref.
* When you look into the table with the options for the "PAGE" object in TSref, you will see that there are several properties, which you can set inside a PAGE object, e.g. "typeNum", "wrap", "stdWrap", numbers (like "1", "2", "3") and so on. The next line in the code above defines the object "page.10", which is one of those "number objects". It could also be called for example "page.5" or "page.20". TSref does not say much about the meaning of these numbers except the data type, which is "cObject". Have a look at the section "Data types" at the beginning of TSref. In the subsection "Data types: Object types" you will find the description of the data type "cObject". It means that you can set the value to any "content object". <br/><br/>*Note* that a "cObject" or "content object" is not a "content element". A "content element" is an element, which is displayed on a single page in the website. Content elements can be edited in the Page module.<br/><br/>To get an overview of the available content objects have a look at the table of contents in TSref. There is a section called "Content Objects" which lists all available content objects. There you see that e.g. TEXT, IMAGE, USER, COA... are possible values. Depending on what you want to display, you can pick the one you like. You then find the options for the one you have chosen in the according section in TSref. <br/>Now you know that in line 3 of the listing above, a content object of the type TEXT is defined and why that is possible.
* Finally there is a subproperty under "page.10". Since "page.10" is a TEXT content object, we have a look at the properties of this content object in TSref. There we see that the cObject TEXT has the subproperty "value" (and some other subproperties, which can be found in the section "stdWrap", but are not important here). In our listing the subproperty "value" is set and as TSref tells us, it basically contains text. Here it is set to "HELLO WORLD!"

What you should have learnt from this chapter is, how properties can be set in TypoScript. Now you should understand, how you can use TSref to look up the available properties for each object and how to use them to create your own TypoScript.

By the way: Did you know, that these four lines already create an output? It is not much, but more than nothing.
Click on the  "View webpage" icon at the top of the screen. 

.. figure:: ../Images/Images/Image:TBT-template-new6.jpg
   :alt:

What you see is this:

.. figure:: ../Images/Images/Image:TBT-template-new7.jpg
   :alt:

.. _load-html-template

Load the HTML template in the TypoScript template
*************************************************

As you could see from the output of the few lines of TypoScript, which we have above, they only produce the words "HELLO WORLD!".

But that is not, what we want to have. We don't only want to output some words, but we want to output 
* first of all our complete template file
* and inside we want to replace our markers and subparts.

So where a TEXT object was defined above, we need to define an object, which outputs a template file. This can be done using the cObject "TEMPLATE". Look it up in TSref!

So instead of the code above we write

:: 

  # Default PAGE object:
  page = PAGE

  # Define the template
  page.10 = TEMPLATE

By the way: When you are working with t3editor to edit the Setup field of your TypoScript template, you can press Ctrl+S to save what currently is in the Setup field. This can make your work noticeably faster.

As TSref tells us, the TEMPLATE cObject has the property "template", in which we can define a cObject, which must be loaded with the template code. This is exactly what we want to do! Since our template is a file, an HTML file, we choose the cObject FILE and add:

::

  # Our template is a file
  page.10.template = FILE

Did you look up the content object FILE in TSref? If not, do so now! 
You will see that for this cObject there is the property "file". The cObject FILE returns the content of the file, which is set in this property. But how exactly do you have to link your file now? This is also answered in TSref. The data type of the property "file" is "resource". You find it in the "Data types reference". There you also find the information that you can link to a file in your TYPO3 installation using a relative path. See the example in TSref. So we add to our template:

:: 

  # Our template file is fileadmin/template/index.html
  page.10.template.file = fileadmin/template/index.html

This loads our template file. If you now view your website (the frontend), you will notice that our template file is used, but that in fact the CSS styles are still missing. 

So obviously we still have to add a reference to our CSS file to our PAGE object somehow.

The section on the "PAGE object" in TSref tells us how we can add tags to the head tag of the HTML output. There are the properties "stylesheet" and "shortcutIcon", which we want to use to include our stylesheet and our icon:

:: 

  # Insert shortcut icon in the head of the website
  page.shortcutIcon = fileadmin/template/favicon.ico
  # Insert stylesheet in the head of the website
  page.stylesheet = fileadmin/template/style.css

Now our Frontend output already has the styles included. 

However, if you view the sourcecode of the output, you will notice that TYPO3 created an own HTML structure and inside the body tags of this structure, there is our complete template, with *its* own html, head and body tags and all the content. This is syntactically wrong HTML or in other words: It is no valid HTML page currently.

We will fix this in the next step.

.. _work-subpart-document

Work with the subpart DOCUMENT
******************************

Currently TYPO3 puts our whole HTML template file between body tags. To get a valid HTML page, we should only put *that* part of our template inside these body tags, which really belongs between body tags. Again having a look at the TEMPLATE cObject in TSref there is the property "workOnSubpart" which does exactly this. In this property you can name a subpart, which you want the TEMPLATE cObject to return. That way this subpart gets extracted from our HTML template file and is the only thing returned. Do you remember how we wrapped the whole content of the body tags of our HTML template in the subpart DOCUMENT? This was the reason to do that; here we use it.
So we add to our template:

::

  # Work with the subpart "DOCUMENT"
  page.10.workOnSubpart = DOCUMENT

The resulting HTML output is a syntactically correct HTML page now. While the *"outer part"* of the output (like the html tag itself, the head tag and its content and the body tag itself) is created by TYPO3, the *contents of the body tag* are taken from our HTML template.

.. _configure-marker-subparts

Configure markers/subparts
**************************

The names of the markers and subparts are now used in the TypoScript template to insert dynamic content into the HTML template at those places, where the markers respectively subparts are.

Having a look at the section on the cObject TEMPLATE you will notice that there are two properties, which hold the configuration for subparts and markers: 

Inside the property "subparts" we can define the rendering instructions for our subparts and inside the property "marks" we can define the rendering instructions for the markers.

Let us add them to the setup of our TEMPLATE object:

::

    ######################################################
    #
    # Configuration of SUBPARTS
    #
    ######################################################

    # Define the subparts, which are inside the subpart DOCUMENT
    page.10.subparts {

    }

    ######################################################
    #
    # Configuration of MARKERS
    #
    ######################################################
    
    # Define the markers inside the subpart DOCUMENT
    page.10.marks {
    
    }

Our subparts are subproperties of "page.10.subparts" and our markers are subproperties of "page.10.marks". When we define the markers and subparts in the next sections, it is important not to mix up page.10.subparts and page.10.marks! If you put the definition of a *marker* into page.10.*subparts*, the marker will not be replaced and vice versa.

For each marker and for each subpart we will define which content object we want to use. Then we configure this content object to produce the output we want. You already know that the list of available content objects can be seen in the table of contents of TSref.

For each of the markers and subparts we will rebuild the structure of the HTML code, which we had in our template. After that we will have the same structure again, but the actual content in it will then be generated by TYPO3 based on the pages and on the page content, which you have created in your TYPO3 installation.

Note: To keep the TypoScript code arranged clearly during the following sections, we do not show the whole code again, when we e.g. add one line to it. Instead we will only show parts of it repeatedly during the setup of a marker or subpart. At the end of each section you will again find the result, which shows the complete code for the according marker or subpart.

.. _configure-metanav

Configure the subpart METANAV
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before we begin defining the first subpart for our meta navigation, let us have a look at where we are: First we have created a page structure in the TYPO3 Backend. TYPO3 will later display these pages. We have modified an HTML template file by adding subparts and markers for everything, which should be output dynamically by TYPO3. Again in the TYPO3 Backend we have created a template record in the root page. Inside that template record we have instructed TYPO3 to load our HTML template and to work with the part between the body tags.

In the next steps we will use the cObjects, which are offered by TYPO3, to configure the output for each of our markers and subparts.

Now we will start with the first subpart. The meta navigation, which will be displayed at the top right corner of the screen, should hold a menu with some pages. We always want the same pages to be at that place (no matter on which page the user of our website currently is). We will put the pages "Contact" and "Imprint" there.

Since we basically want to output a menu, we define the subpart METANAV as

:: 

  page.10.subparts {
  METANAV = HMENU

Now we can use the properties of the cObject HMENU. With these properties you can output all kinds of *hierarchical menus*.

Just for you to remember here again is the HTML code, which was in our template and which we have to replace:

:: 

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

As you can see, we first have a ul tag, which stands for an unordered list. Inside that list each menu item is inside an li tag.

Since the HMENU cObject has the property "wrap", we can create a ul tag around our menu by adding

:: 

  METANAV.wrap = <ul>|</ul>

Now we only want to have some special pages to be displayed in our menu. This can be done with the "special" property. As you see in TSref, this property supports several different values. We choose 

::

  METANAV.special = list

to create a list of selected pages.

For the type "special = list" there again are some subproperties available, the most important one being "special.value". Inside that property you have to define the page IDs, which should be part of the menu. In my case the pages "Imprint" and "Contact" have the page IDs 80 and 81, so to get them displayed I have to add:

::

  METANAV.special.value = 80, 81

However, *you will have to adjust this list* so that the IDs of your pages are used there.

The cObject HMENU can render menus. Since menus can have different levels of pages, HMENU offers "number properties", inside which you can define the rendering instructions for each page level seperately.
E.g. with "METANAV.1" we can define how pages on the first level of our menu should be rendered. "METANAV.2" would define the rendering of pages on level two and so on. (In fact it only makes sense to have one level of pages and not multiple levels for our meta navigation, but if you think of our subnavigation, you will notice that there we will have to define multiple levels.)

Have a look at the table of contents in TSref and look at the section "MENU Objects". These objects can be selected for each page level (e.g. for "METANAV.1"). The most important ones are TMENU and GMENU. TMENU creates a textual menu and GMENU creates a graphical menu.

For METANAV.1 we want to have simple text and no graphics. So we define

::

  METANAV.1 = TMENU

Note that TMENU and GMENU are *no* content objects (although their name looks similar to HMENU, which *is* a content object). So you cannot use them to replace a marker or a subpart (which you *can* use HMENU for)! TMENU and GMENU can only be used inside a menu (like inside an HMENU)!

Inside of the object TMENU we can now define the rendering of one single menu item (that is one single link to a page). 

The object TMENU has several properties. The most important ones are the so called "Common Item States". In the table "Common item states for TMENU, GMENU and IMGMENU series" you find these properties, which are available for TMENUs, GMENUs and IMGMENUs. Additional properties for TMENUs are listed in the table "TMENUITEM". 

We only need the table with the common properties now. This table lists the menu item states. With these states you can define the rendering of each menu item based on its current state. The state "NO" stands for "normal", that is the state in which a menu item is by default. If you do not define another more special state, which applies for a menu item, the state NO will be used to render it. The state "ACT" is used for menu items which are in the rootline currently (and so kind of "active"). The definition of "CUR" is used for the "curent" page, that is exactly the one page which the user is currently on. That way you can display the links differently e.g. by adding different CSS classes. We will do that for the marker TOPNAV.

For our menu we will only use the default state NO. That way the links will always be rendered the same way, no matter if the user currently is on the linked page or not. Or with other words: If we only define this state and no other states here, TYPO3 will use these rendering instructions for all items on page level one in that menu.

Before you use an item state, you should always activate it by setting it to 1:

::

  METANAV.1 {
    NO = 1
  }

While activating the item state is *not* needed for the item state NO, it *is* needed for all other item states. If you forget it there, the rendering, which you supplied for that state just will not be used. To not make this mistake it is better to always activate all item states explicitly before you use them.

Now we want the pages in our menu to be each wrapped in li tags. Have a look at the table "TMENUITEM" now. There you find the property "allWrap", which wraps the whole item. Exactly what we want, isn't it?

::

  METANAV.1 {
    NO = 1
    NO {
      # Each entry is wrapped by
      # <li> </li>
      allWrap = <li>|</li>
    }
  }

This completes the code we need for our meta navigation. I have rewritten it with brakets now and I have slightly restructured the properties.
Here it is again:

::

    ######################################################
    #
    # Configuration of SUBPARTS
    #
    ######################################################
    
    # Define the subparts, which are inside the subpart DOCUMENT
    page.10.subparts {
    
      ##############################################
      #
      # Subpart METANAV
      #
      ##############################################
    
      # The subpart METANAV outputs the meta navigation
      # at the top right corner of the page
      METANAV = HMENU
      METANAV.wrap = <ul>|</ul>
    
      # Only display special pages here: Contact and Imprint
      METANAV.special = list
      # LIST NEEDS MODIFICATION:
      # Take your page IDs!
      # Change the values in the following list!
      METANAV.special.value = 80, 81
    
      METANAV.1 = TMENU
      METANAV.1 {
    
        # NO: default formatting
        NO = 1
        NO {
          # Each entry is wrapped by
          # <li> </li>
          allWrap = <li>|</li>
        }
      }
    }
    
    ######################################################
    #
    # Configuration of MARKERS
    #

And here is a screenshot of the HTML source code of the resulting output:

.. figure:: ../Images/Images/Image:TBT-Conf_METANAV.jpg
   :alt:

.. _configure_headertitle
   
Configure the marker HEADERTITLE
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The marker HEADERTITLE should output something like a "site title". It is the title of your whole website. So what we want to output there basically are only some words of text. You already know how that is working; you removed such a definition when we started with the TEMPLATE cObject. There was a TEXT cObject, do you remember? This is how we can use a TEXT object to output our site title there:

::

    HEADERTITLE = TEXT
    HEADERTITLE.value = TYPO3

This is all it takes to put our header title in place. Btw this is the easiest way to output a string with a cObject.

Have you noted that we just have defined a marker (and no subpart)? Check that you have put the definition into page.10.marks, not into page.10.subparts! I have added some comments (all lines starting with "#") to the code so that it is easily understandable. Remember that these comments don't do anything and could also be left out which would not change the functionality of the TypoScript template. The code in that section should now look like this:

::
    
    ######################################################
    #
    # Configuration of MARKERS
    #
    ######################################################
    
    # Define the markers inside the subpart DOCUMENT
    page.10.marks {
    
      ##############################################
      #
      # Marker HEADERTITLE
      #
      ##############################################
    
      # The marker HEADERTITLE outputs the site title
      HEADERTITLE = TEXT
      HEADERTITLE.value = TYPO3
    
    }

In the next sections the code in this manual (like the part directly above) will no longer show a big comment above showing into which property you have to put a definition, because now you know where they belong. By the way: The order in which you define the markers and the subparts inside page.10.marks and page.10.subparts basically does not matter. (This is only different in a few cases: You can for instance create a copy of an object using the "<" operator. If you defined "DATE < page.10.marks.HEADERTITLE" below the definition of HEADERTITLE which we added above, you got the same output, which you get for the marker HEADERTITLE, also for the marker DATE. When you create a copy, the definition which you want to copy must be noted above the one in which you create the copy. However, we do not create copies of our own TypoScript code in this tutorial, so that we do not have to care about in which order we define our subparts or markers inside the respective properties.)

.. _configure-topnav

Configure the subpart TOPNAV
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The subpart TOPNAV displays our main menu, which is located inside the orange bar at the top of the page. Here again is the structure of the HTML code, which we need to create:

::

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

Since we want to display a menu we again begin defining an HMENU

::

   TOPNAV = HMENU

This time we have to wrap the menu in a div tag and - inside the div tag - into ul tags. We could put both into the same property now, like

::

   TOPNAV.wrap = <div id="nav_main"><ul>|</ul></div>

, but there also is a way, which makes our definitions look nicer to the eye: We define both wraps seperately. Like every cObject HMENU also provides a property named "stdWrap". TYPO3 applies this property after all other properties of the object have been computed. Behind stdWrap there is a very powerful function; it is a kind of "Swiss knife", which offers a big number of functionalities. This property has many subproperties (just look at the section "stdWrap" in TSref) with which you can do lots of different things: You can for example format the content of a cObject, you can change the case of the content, you can output the content based on a condition or you can add data from the database. However, this is just to give you a quick overview of what stdWrap can do for you. Here we only use the "wrap" property of stdWrap to add a normal wrap. Basically you already know how that is working. So we add this to our template:

::

    TOPNAV.wrap = <ul>|</ul>
    TOPNAV.stdWrap.wrap = <div id="nav_main">|</div>

Note that the order in which we define TOPNAV.wrap and TOPNAV.stdWrap.wrap does not matter. TYPO3 always applies different properties of an object based on the order, which is coded inside TYPO3. (And in this case "wrap" is computed before "stdWrap.wrap".)

When you had a look at our HTML template you might have noticed that there in fact are two menus: One in the orange bar at the top and one in the left column below the orange bar. The menu at the top (TOPNAV) should only display the first level of pages. The menu in the left column (SUBNAV) should display the subpages for that one page, which is currently selected from the top menu. We will configure SUBNAV later; now we are only interested in TOPNAV.

So what we want to output in the menu is a list of the pages, which we have on level 1 of our page tree in TYPO3. Again we use a textual menu. So we need to define 

::

    TOPNAV.1 = TMENU
    TOPNAV.1 {
    
    }

As the normal rendering (the default rendering) we again need li tags:

::

    TOPNAV.1 {
    
      # Definitions per page
      # NO: default formatting
      NO = 1
      NO {
        allWrap = <li>|</li>
      }
    }

But did you see that there is one page in the main menu, which has the CSS ID "current" in the li tag? This ID should be used for the page, which is somehow active currently: Either because the user currently is *on* that page or because he is *below* that page. The CSS ID is used in our CSS stylesheet to render that one link differently.

So this time we also have to define another item state besides "NO". You have already learnt that for our case we need to configure the state "ACT". This state offers the same properties as the state NO does. So we add this to the definition of our TMENU:

::
    
    TOPNAV.1 {
    
      # ACT: User is on this or below this page
      # Activate this state for this menu
      ACT = 1
      ACT {
        allWrap = <li id="current">|</li>
      }

That way a page, which is active (because the user is on that page or on a subpage below that page), is wrapped with this wrap instead of the one coming from NO.

This completes our TypoScript code for the subpart TOPNAV. Here is the complete code for that subpart. The order of the properties again is slightly restructured and the code is indented:

::

    ##############################################
    #
    # Subpart TOPNAV
    #
    ##############################################
    # The subpart TOPNAV outputs the main navigation
    TOPNAV = HMENU
    TOPNAV.wrap = <ul>|</ul>
    # "stdWrap" properties are applied after "wrap".
    TOPNAV.stdWrap.wrap = <div id="nav_main">|</div>
    
    # Definition for pages on the first level of the menu
    TOPNAV.1 = TMENU
    TOPNAV.1 {
    
      # Definitions per page
      # NO: default formatting
      NO = 1
      NO {
        # Each entry is wrapped by
        # <li> </li>
        allWrap = <li>|</li>
      }
    
      # ACT: User is on this or below this page
      # Activate this state for this menu
      ACT = 1
      ACT {
        # Use another wrap
        allWrap = <li id="current">|</li>
      }
    }

With this code added to our TypoScript template, the main navigation in the orange bar is already working. If you now view the Frontend (that is the website, which is produced by TYPO3), you will see that inside the orange bar we already see the titles of the pages, which we have created on the first level of the page tree inside the TYPO3 Backend some steps before. If you click one of these pages in the Frontend (inside the orange bar), you will also notice how the active page is displayed differently. A look at the source code of the frontend output shows us that for this page TYPO3 uses the wrap, which we have defined for the state ACT.

.. _configure-subnav

Configure the subpart SUBNAV
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Next we will configure the subpart SUBNAV. This subpart should render the sub navigation, which will be displayed in the left column of the Frontend output.

Basically this again is a normal menu, but it has some specifics: It should not show the pages, which are on level 1 of the page tree, but instead it shows the pages, which are *below* the page on level 1, which is currently *active*. So the first level of pages, which should appear in this menu are the pages on level 2 of the page tree.
Furthermore the sub navigation should also show pages on deeper levels like on level 3. So we also have to configure this level.

Here again is the structure of the HTML code, which we need to replace:

::

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

We again define an HMENU:

::

   SUBNAV = HMENU

Now we have to set the level of pages of the page tree, with which the menu should begin. This can be done with the property "entryLevel", which is provided by the object HMENU. If it is set to "0", the menu begins with the first level of pages below the root page. That is what is used in the top menu TOPNAV. (In fact we did not have to set entryLevel to "0" explicitly there, because "0" is the default value.) But here we want the menu not to start with the pages, which are directly below the root page, but with the ones, which are one level deeper. So we add:

::

    SUBNAV = HMENU
    SUBNAV.entryLevel = 1

Now independently from the question of the entryLevel: When you have a look at the above screenshot you will see that the HTML code of the menu basically has the same structure for the pages on level 1 as for the pages on level 2. Here is what the structure looks like:

* We need one ul tag around the whole menu and each item on the first level must be wrapped in li tags.
* Where a menu item has subpages, there inside the li tag we need a ul tag and inside that ul tag the next level of pages should be rendered. Have a look at the screenshot above. There "Submenu Item 3" shows this situation.

Since the structure of both levels of the menu basically is the same we will now define the structure for the pages on level one, will then copy that structure for the pages on level two and only make the few changes there, which are needed.

To have things structured logically, I add the outer ul tags not to the wrap of the HMENU like we did e.g. for TOPNAV, but to the wrap of the first level of pages of the TMENU. In the end this does not make a difference in the rendering, the wrap in both cases appears at the same place. But having it inside the first level of the TMENU I can also copy that wrap, when I create the instructions for pages on level 2.

::

    SUBNAV {
    
        # Definition for pages on the first level of the menu
        1 = TMENU
        1 {
          wrap = <ul id="submenu">|</ul>
    
Something else which is important when you can have multiple levels of pages in a menu is the question, if you always want to see all subpages. By default TYPO3 only shows the subpages of *the* page, which currently is active. In contrast I want TYPO3 to always show all subpages, also the ones of pages, which the user is not on currently. This can be done with the property expAll:

::

    1 = TMENU
    1 {
      wrap = <ul id="submenu">|</ul>
      expAll = 1
 
Now let's have a look at the rendering definition for a single item on level 1, when it is in normal state. We want to wrap each item on level 1 in an li tag. In the menus METANAV and TOPNAV we always used the property "allWrap" to do this kind of task. However, this property only wraps the item itself. But when we have an item with subpages, these subpages would not be included in the wrap, but would follow after it. With other words: allWrap would insert the closing li tag, before the tags for the subpages start (that is the ul tag and the li tags inside it). This would lead to invalid HTML; the nesting of the different tags would no longer be valid. So what we need here is a property, which does not only wrap the menu item, which we have currently, but also all subitems. The result should be that the closing li tag is inserted *after* the subpages. This can be done with "wrapItemAndSub". So we add this to our template:

::

    SUBNAV.1 {
      # Definition per page
      # NO: default formatting
      NO = 1
      NO {
        wrapItemAndSub = <li>|</li>
      }
    }

As you see in the HTML template there also is the CSS ID "active", which should be added to that one menu item, which currently is active. So again it is not enough to just define NO as normal default state and to always use that state, but we also have to add a special definition for the case of a page being active. So we need to define this different wrap in the property "wrapItemAndSub" of the object "ACT", so that it overwrites our normal default wrap:

::

    SUBNAV.1 {
      ACT = 1
      ACT {
        # Use another wrap
        wrapItemAndSub = <li id="active">|</li>
      }
    }
Now we have the definitions for the pages in the first level of our menu complete.

The next thing to do is to add the defintions for pages, which are displayed in the second level of our menu. You already know that - while the rendering of the pages for the first level of our menu is defined in "SUBNAV.1" - the rendering for the pages on level 2 will be done in "SUBNAV.2". As I explained above, we will not define each of these lines again for level 2, because they are nearly identical. Instead you will now learn how to copy objects in TypoScript.

Until now we always used the operator "=" to assign a value to a property. Copying an object works with the operator "<".

Before we continue with our template it makes sense to explain this with an example. I have the object HEADERTITLE. Now I can create a copy of it and call the copy ANOTHEROBJECT:

::

    page.10.marks {
      HEADERTITLE = TEXT
      HEADERTITLE.value = TYPO3
    
      # Create a copy of HEADERTITLE in ANOTHEROBJECT
      ANOTHEROBJECT < page.10.marks.HEADERTITLE
    }

With this definition we define the object ANOTHEROBJECT and set its content to a copy of the object HEADERTITLE. Copying also includes all subproperties and their values. The example above also sets ANOTHEROBJECT.value to the value "TYPO3".

When copying on the same level, you can just refer to the name of the copied object, prepended by a dot. See the following code:

::

    page.10.marks {
      HEADERTITLE = TEXT
      HEADERTITLE.value = TYPO3
    
      # Create a copy of HEADERTITLE in ANOTHEROBJECT
      ANOTHEROBJECT < .HEADERTITLE
    }

This produces the same result as the example above, but it is even more readable. This also is the reason why we will use this "short notation" when we now copy level 1 of our menu to level 2.

So now let us come back to our template record. Here again is our current TypoScript, reduced to the part, which is important now. (You will again find the complete TypoScript for this subpart at the end of this section.) The copying takes place in the last line:

::

    SUBNAV = HMENU
    SUBNAV {
    
      # Definition for pages on level 1
      1 = TMENU
      1 {
        NO = 1
    
        ACT = 1
      }
    
      # Definition for pages on level 2
      # Copy the definitions from level 1
      2 < .1
    }

The line "2 < .1" is all it takes to create a complete copy of all the definitions, which we set up for the pages on level 1. With these few signs we have copied all the definitions, which we have in SUBNAV.1 to SUBNAV.2. Easy, isn't it? The only thing you must be aware of is the dot in front of the copied object. Remember that it means that you point to an object on the same level. And do not forget it!

Now when we have a look at our HTML template again we see that there is one small difference in the output of the pages on level 2 compared to the output of the pages on level 1: The wrap at the ul tag (that is the wrap for the whole page level) is different. While the ul tag had the CSS ID "submenu" attached on level 1, our HTML template shows us that there does not belong a CSS ID on level 2. So let's overwrite the wrap for level 2. We can do so after we copied the whole object to SUBNAV.2 by defining another value for SUBNAV.2.wrap:

::
    
    SUBNAV = HMENU
    SUBNAV {
    
      # Definition for pages on level 2
      # Copy the definitions from level 1,
      # but use another wrap.
      2 < .1
      2.wrap = <ul>|</ul>

That's it! Our submenu now can display up to two levels of pages. This should be enough for most websites.

Again here is the whole TypoScript code of that subpart, slightly restructured and nicely indented:

::

  SUBNAV = HMENU
  SUBNAV {
    # Only display subpages of the page from the main
    # navigation, which is in the current rootline.
    # Default value of entryLevel is 0, which are the
    # pages on the first level.
    # We want to begin with those subpages on level 2.
    entryLevel = 1

    # Definition for pages on level 1
    1 = TMENU
    1 {
      wrap = <ul id="submenu">|</ul>
      # Always expand all subpages.
      expAll = 1

      # Definition per page
      # NO: default formatting
      NO = 1
      NO {
        # Each entry is wrapped by
        # <li> </li>
        wrapItemAndSub = <li>|</li>
      }

      # ACT: User is on this or below this page
      # Activate this state for this menu
      ACT = 1
      ACT {
        # Use another wrap
        wrapItemAndSub = <li id="active">|</li>
      }
    }

    # Definition for pages on level 2
    # Copy the definitions from level 1,
    # but use another wrap.
    2 < .1
    2.wrap = <ul>|</ul>
  }

Now we have defined the meta navigation, the top navigation and the sub navigation. So all menus in our site are configured now and should display links to the pages, which you have created inside the TYPO3 Backend. However, until now all pages only display the blind text, which comes from the HTML template. We will change this in the next sections.

.. _configure-contentright

Configure the subpart CONTENTRIGHT
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Using the menus you can now navigate through your website. To check if that works, have a look at the URL bar of your web browser. There you should see a URL ending with something like "index.php?id=75". When you click on a link to another page that id parameter (here the "75") should change. 

So in fact we can already visit the according pages that way. You will say "Well, that is nice, but all pages are still showing this "Lorem ipsum" dummy text, which comes from the HTML template." That is true and we will now change this. We will now configure the subpart CONTENTRIGHT.

The subpart CONTENTRIGHT is a special subpart: With this subpart we instruct TYPO3 to get the content of the current page, that is the content of the page which the user has clicked in the menus. We will configure CONTENTRIGHT to get the content for the *right* column of our web pages (and not for the left or middle column) from the database. TYPO3 offers the cObject CONTENT to do that job so we define:

::

   CONTENTRIGHT = CONTENT

As you can see in TSref the cObject CONTENT has a number of subproperties, which would allow us to define in detail, which records should be selected (and finally displayed). However, there is good news: Do you still remember that I told you to include a static template in your template record? You had to include the static template from the TYPO3 system extension "CSS Styled Content". This static template offers objects, which contain all the lines needed to get the correct contents from the database. In the page module in the TYPO3 Backend you by default see four columns. For each of these columns the static template from CSS Styled Content contains an object, which reads out the contents of that column. These objects have the following names:

::

    # Middle column (labeled "normal")
    styles.content.get
    # Left column
    styles.content.getLeft
    # Right column
    styles.content.getRight
    # Border column
    styles.content.getBorder

Since we have included the static template before, we can now simply fill our subpart CONTENTRIGHT by copying the object, which is available as "styles.content.getRight". So we add this to our template:

::

    CONTENTRIGHT = CONTENT
    CONTENTRIGHT < styles.content.getRight

In fact the line "CONTENTRIGHT = CONTENT" is not even needed, because it is directly overwritten again by the definition of styles.content.getRight when we copy this object in the next line. I only included it to make it more obvious what is happening here.

Just for fun we now have a look at the definitions, which we had to write, if the static template was not included:

::

    # get content, right
    CONTENTRIGHT = CONTENT
    CONTENTRIGHT {
      table = tt_content
      select.orderBy = sorting
      select.where = colPos=2
      select.languageField = sys_language_uid
    }

Thanks to the static template from CSS Styled Content we do not have to think about how all these properties work together and how to configure them. By copying styles.content.getRight we already get exactly these definitions for CONTENTRIGHT.

And that is already it! Here you have again the complete TypoScript code for this subpart:

::

  ##############################################
  #
  # Subpart CONTENTRIGHT
  #
  ##############################################

  # The subpart CONTENTRIGHT outputs the content,
  # which is saved in TYPO3 in the right column of a page
  CONTENTRIGHT = CONTENT
  # Needs the static template from css_styled_content
  # to be included in this template record.
  CONTENTRIGHT < styles.content.getRight

Considering how important this subpart is for our website (after all it outputs the content), it is surprisingly easy to set up. You might wonder that we did not define rendering instructions for the different content elements, which you have entered on a page in the TYPO3 Backend and which should be output in the Frontend. After all these elements can have a header in top of them or can display images just to name the most common examples. However, TYPO3 already comes with the needed rendering instructions so that we don't have to write them ourselves. If we wanted to we could change them somehow, but for now we will just leave everything as it is.

Now that you have defined the subpart CONTENTRIGHT, you can guess already, how we will define CONTENTMIDDLE. But let us stick to the order of the markers and subparts as we have it in our HTML template. So we will continue with the marker DATE.

Configure the marker DATE
~~~~~~~~~~~~~~~~~~~~~~~~~

The marker DATE is displayed above the middle column of our website. It should display the current date.

So basically we only want to output a short string, like a text, but it should get its content dynamically. This kind of magic is possible with the function stdWrap. stdWrap is available for many properties and also for some objects.

Let us define DATE as a TEXT object:

::

    DATE = TEXT

Did you put this line into page.10.marks? Remember that DATE is no subpart.

When you read the introduction of the cObject TEXT in TSref carefully you will notice that on the rootlevel of the TEXT object stdWrap properties are available. This only is the case for the cObject TEXT! All other cObjects have a property called "stdWrap", in which stdWrap properties are available.

When we have a look at the function stdWrap in TSref you will see that there is a property called "data", which has the data type TSref/getText|getText. Looking at the "Data types reference" you will see that using getText it is possible to get several information from somewhere in PHP. One of this information is the current date (see the example!). TSref shows us that in that case the syntax of our value is something like "date : d-m-y". The part "date :" must not be changed. The part behind is used for the date format, which we want to get. For the possible values you can have a look at the PHP manual on the date function: http://php.net/manual/en/function.date.php

We will use: Day with two digits, then a dot, then month with two digits, then another dot and finally the year with four digits. So the format of our date string must look like this: "d.m.Y".

So we add to our TypoScript:

::

    DATE = TEXT
    DATE.data = date : d.m.Y

Codewise this is the complete setup code, which we need for this marker. As usual I print it here with comments again:

::

    ##############################################
    #
    # Marker DATE
    #
    ##############################################
    
    # Outputs the current date in the defined format
    DATE = TEXT
    DATE.data = date : d.m.Y

With this marker you could again see how much you sometimes have to jump from chapter to chapter when you read TSref. But don't be worried: The syntax of the resulting TypoScript code mostly is - like in our case - rather simple.

.. note::
   Usually, the pages are cached for 24 hours. So it will happen, that a page gets cached at 31.12.2012. The date is filled then with 31.12.2012. But if someone request that page early at 1.1.2013 it will still state 31.12.2012. If you configure config.cache_clearAtMidnight the cache will be cleared at midnight and you have allways the correct date.

.. _configure-breadcrumb

Configure the marker BREADCRUMB
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The marker BREADCRUMB should show a breadcrumb menu. This is a menu, which shows the hierarchical click path, which the user has taken to come to the page on which he currently is.

As it helps the user navigating through the website this also is a kind of menu. As you know we always use the cObject HMENU, when we want to create a menu. So we ammend to our template:

::

    BREADCRUMB = HMENU

TYPO3 offers a special functionality to create a breadcrumb menu; maybe you have already seen it when we created our meta navigation (the menu with the few pages, which are always displayed at the top, no matter on which page the user currently is). The cObject HMENU has a property called "special", which has some values. With each of them you can create a special kind of menu. One of these values is called "rootline" and this basically is just another term for the pages, which we want to see in our menu. So let us add that:

::

    BREADCRUMB = HMENU
    BREADCRUMB {
      special = rootline

Now there also are some options for the rootline menu. The most important property is the one called "special.range". 

This property is a bit more complex, but you will get it. "special.range" takes two integers as values, seperated by a pipe. For example "special.range = 0|5". With this property we can define the range of our menu. Or in other words we can set the level of the first page in our menu and the level of the last page in our menu. The number in front of the pipe (in our example the "0") defines the level of the first page in our menu. The number behind the pipe (in our example the "5") defines the last level, which should be shown in the menu. All pages in the click path between and including these two levels will be included in the menu.

Now let's have a look at the meaning of the numbers: The root page is on level 0. Positive values stand for page levels further outwards. So with our example "special.range = 0|5" we would get a rootline menu which starts with the root page (level 0) and then shows the active pages on each level for up to 5 levels below the root page. (This all provided that the user currently is that deep into the structure of the website. If the user is for instance on level 2 currently, the rootline ends on level 2 and so will the output of our rootline menu.)

We want to create a special rootline: Our menu should not begin with the rootpage, because this page only is a redirect to the page "Home" on level 1. So we want our menu to start one level below the rootpage, which makes the first part of the value of special.range a "1". 

Then the menu should show all pages up to the current page. But how can we do that? The problem is that right now, where we are writing this code, we do not know on which page level the user is when he clicks a page. We do not know, how deep our website will be and basically the user could be on any page level. For this dilemma there is a solution: We can also define negative numbers for each of the values in special.range. Negative values begin with the outermost level of the current rootline and go inwards. For example -1 stands for the page on the outermost level of the current rootline. (This must not necessarily be the page, which is on the outermost level in the *page tree*!) So the value we want is "-1".

With this knowledge we can now define the value of special.range as we need it:

::

    BREADCRUMB = HMENU  
    BREADCRUMB {
      special = rootline
      special.range = 1|-1

Inside our HMENU we again define a TMENU 

::

    1 = TMENU
    1 {

When you have a look at our HTML template again you will see that in the rootline menu there are links to the pages and between the links we have greater-than signs. In the other menus we have always differentiated the items by their item state. That way e.g. the current page could be rendered differently. This is also what we could do here. We could add:

::

    NO = 1
    NO.allWrap = |&nbsp;>&nbsp; 
    
    CUR = 1
    CUR.allWrap = |

This shows a greater-than sign after each page, except behind the current page (which always is the last page in the rootline). But we already know that this is possible, the code looks ugly and using the same definitions again and again is boring. We will immediately forget these definitions and do it in a far more interesting way.

We will now have a look at something more complex.
There is a function called optionSplit, which is run over the whole configuration of TMENU, GMENU and IMGMENU. With this function we can produce the same result as with the ugly way above, but with short and nice code. Let's go:
Using the function "optionSplit" you can instruct TYPO3 to render each menu item differently depending on its position in the menu. Having this option on the one hand provides you with big flexibility. But on the other hand it comes with big complexibility as well. We will now use this function to render the items in our breadcrumb menu.

We want greater-than signs between the menu items. optionSplit is available for properties of menu items of TMENUs (like for properties of NO). So optionsSplit can e.g. be used for wraps of these menu items.
To be applied, the value, which you assign to the wrap, must have the following syntax:

|*| splits the list of menu items into up to three parts. A part can include one or more menu items. The number of items per part is defined through "||".

||  splits the parts in subparts. You can freely choose the number of subparts inside each part. Each subpart is one item. That way you can define different instructions for the menu items depending on their position.

Abstractly:

::

   NO.allWrap = first|*|middle|*|last

"first" is prepended to the first item, "last" to the last one and "middle" to all others. The priority of the parts in fact is last, first, middle. This is important, if there e.g. are only two pages in the menu.

In our breadcrumb menu we only have two different cases: We want the ">" sign in front of all pages, but not in front of the first one.

The easiest way to do that is to split the first part into subparts:

::

   NO.allWrap = ||&nbsp;>&nbsp;

Since there was no |*|, both subparts belong to part one. The first subpart of part one is empty, so there will be nothing in front of the first menu item. The second subpart of part one contains the ">" sign, which will be used in front of item two. If our menu has more items, the second subpart is repeated for all other items prepending them with ">" as well.

After these goodies, here you again have the complete setup code for that marker:

::
    
    ##############################################
    #
    # Marker BREADCRUMB
    #
    ##############################################
    
    # Outputs a menu which shows a click path to
    # the current page.
    BREADCRUMB = HMENU
    
    BREADCRUMB {
      special = rootline
      # Range: Syntax is "Start level|End level"
      # Values for both:
      # 0 stands for the root page, positive values go outwards.
      # Negative values begin with the outermost level of the current
      # rootline and go inwards;
      # e.g. -1 stands for the page on the outermost level of the
      # current rootline.
      # Start level: 1 = The page one level below the root page.
      # End level: -1 = The current page.
      special.range = 1|-1
    
      1 = TMENU
      1 {
    
        NO = 1
        # We want greater-than signs between the menu items.
        # Inside allWrap we use optionSplit to prepend the menu items
        # with different values depending on their position in the menu:
        # "||" divides different items.
        # Nothing in front of "||" means the first menu item will be
        # prepended with nothing.
        # The second item will be prepended with ">".
        # If our menu has more than two items, the definition of the
        # second item is repeated for all following items prepending
        # them with ">" as well.
        NO.allWrap = ||&nbsp;>&nbsp;
      }
    }

After that many new things just for the marker BREADCRUMB, we will have a look at the marker TITLE. No fear, compared to the last marker it will be like a walk in the park.

.. _configure-title

Configure the marker TITLE
~~~~~~~~~~~~~~~~~~~~~~~~~~

We are nearly done. Let's again have a look at what we have done already: First we have created a page structure in the TYPO3 Backend. With our current definitions TYPO3 can already display parts of these pages (namely the menus and the content of the right column). We have modified an HTML template file by adding subparts and markers for everything, which should be output dynamically by TYPO3. Again in the TYPO3 Backend we have created a template record in the root page. Inside that template record we have loaded our HTML template and configured most of the markers and subparts. The markers and subparts, which we have configured, already show their content. Currently only the marker TITLE and the subpart CONTENTMIDDLE are missing, then we have basically finished setting up our site. Only a few small things should still be done then.

Now we will configure the marker TITLE. This marker is placed above the middle column and should output the page title of each page (meaning always the title of the current page). So we need a cObject, which can output a text and this text should come from the database. Maybe you already have a clue where the journey is going.

Let's start by defining a simple TEXT object:

::

   TITLE = TEXT

You should remember that each cObject has stdWrap available: Either there is a property "stdWrap" or - in case of the cObject TEXT - the stdWrap properties are available directly for the object itself. By the way: You should already know that TYPO3 uses a database to store your pages and your page content. Do you know how a database is structured? It contains several tables (e.g. the pages are stored in the table called "pages") and in each table there are fields (e.g. in the table "pages" there is the field "author", which can contain the name of the author of each page. But that just for your information.

So now let's look through the possibilities of stdWrap to check, how it can help us. You will find that stdWrap has the property "field". This property returns the contents of that field of the current page out of the database, which you set as value for the property. You don't have to look into the table "pages" of your database and view its structure to see where TYPO3 stores the page titles. I will tell you: They are in the field called "title".

So we can add to our TypoScript:

::

   TITLE = TEXT
   TITLE.field = title

And that is all. Now the marker TITLE gets replaced with the headline of the page. Again here is the commented and indented code:

::

    ##############################################
    #
    # Marker TITLE
    #
    ##############################################
    
    # The marker TITLE outputs the page headline
    TITLE = TEXT
    TITLE.field = title

Now let us define the subpart CONTENTMIDDLE.

.. _configure-contentmiddle

Configure the subpart CONTENTMIDDLE
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

I don't want to bore you. You already know how this is working, at least you have already configured the subpart CONTENTRIGHT.

There you have already learnt that it is a help, that you have included the static template of the extension CSS Styled Content. You know that you can define

::

   CONTENTMIDDLE = CONTENT

to use a content object and you might remember that this line was not needed at all, because it will just be overwritten, when we define the next line where we copy the according object from the static template. The four objects, which help us get the content for the according column were named

::

    # Middle column (labeled "normal")
    styles.content.get
    # Left column
    styles.content.getLeft
    # Right column
    styles.content.getRight
    # Border column
    styles.content.getBorder

Here we want to get the content, which is saved in the column called "normal" in the page module of the TYPO3 Backend. The object, which we copy to get the content from that column, is named styles.content.get. So we add

::

   CONTENTMIDDLE = CONTENT
   CONTENTMIDDLE < styles.content.get

Again we do not need more than these two lines. This is all to get our content out of the database and into our page!

Here you again have the complete code for the subpart CONTENTMIDDLE:

::

    ##############################################
    #
    # Subpart CONTENTMIDDLE
    #
    ##############################################
    
    # The subpart CONTENTMIDDLE outputs the content of the middle column
    CONTENTMIDDLE = CONTENT
    # Needs the static template from css_styled_content
    # to be included in this template record.
    CONTENTMIDDLE < styles.content.get

This was the last subpart, which we had to configure. All markers already are configured as well. So now all markers and subparts get replaced. When you viewed your website some steps before (when we created the menus), you could already navigate through the site (the URLs changed), but there was only that dummy text and no real content. This has changed now.

.. _desired-task-result

The desired task result
~~~~~~~~~~~~~~~~~~~~~~~

.. note::
   Enter some content to see the result completely.

.. _task-result

The task result
"""""""""""""""

(Show the result of it all.)

View your website now! 

You will notice that all markers and all subparts display the content they should display. Basically you can now use your TYPO3 installation and add your contents, that is: Add pages and fill them with content elements. Each page - as long as it is a subpage to the page "Root" - will be rendered using your template with all its definitions. You can add an unlimited number of pages without having to write a single line of template code for them. If you have editors who should put the content in the TYPO3 installation you should create them a normal account, that is an account, which is no administrator in TYPO3. That way these users do not see the template module at all and you can even define for all modules, if they should see them. But these things have nothing to do with templating so we won't discuss them in detail.

.. _next-steps

Next steps
**********

.. note::
   What might be the next task? E.g. adding a second level for the navigation. Create no text menu, but a graphical menu. Ensure that HTML-output is conform to W3C-standard etc.

In this tutorial we built the website by adding markers and subparts to a HTML file, which is a very common way to do the job. Mention that with TYPO3 websites can also be built in three other ways:
* Using the TYPO3 extension automaketemplate, which basically works the same way as we do in this tutorial, but which automatically wraps those sections of a HTML page, which have a certain class or id, in corresponding template subparts.
* Using a special TYPO3 extension called TemplaVoilá which uses a technique called "mapping" to allow to create more flexible page structures.
However, both are not part of the TYPO3 Core and need some additional configuration. For these reasons they are not used in this tutorial.
* you can do without any HTML Template and build the website complete inside of Typoscript with nested COAs and wraps 

Do you want to know more about how copying objects in TypoScript works? Do you know that you can also create so called "references" instead of copying an object? If you want to know more, have a look at the manual "TypoScript Syntax and In-depth Study"! The chapter "Syntax" tells you all about the syntax of TypoScript!