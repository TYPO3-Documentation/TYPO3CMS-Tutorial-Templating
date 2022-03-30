.. include:: /Includes.rst.txt


.. _configure-contentright:

CONTENTRIGHT subpart
~~~~~~~~~~~~~~~~~~~~

Using the menus you can now navigate through your website. However since the content is always the same,
the only way to check if it really works is to look at the URLs in the address bar of your browser.

Now is the time to stop displaying the content of the HTML template and get the actual stuff
output in the frontend, starting with the subpart called CONTENTRIGHT.

We want to instruct this subpart to display the content of the current page,
more particularly the content which was entered in the "Right" column of the **WEB > Page**
module in the TYPO3 CMS backend. For this we use the :ref:`CONTENT <t3tsref:cobj-content>` object:

.. code-block:: typoscript

	CONTENTRIGHT = CONTENT

The TSref shows us that the :code:`CONTENT` object has a number of subproperties,
which would allow us to define in detail which records should be selected (and finally displayed).
However, there is good news: remember how we included a static template from system extension
"css\_styled\_content"? This static template offers objects which contain all the lines needed
to get the correct contents from the database.

The **WEB > Page** module of the TYPO3 CMS Backend contains four columns by default.
The static template from "CSS Styled Content" contains an object to render the content
for each of these columns. Here are their names:

.. code-block:: typoscript

	// Middle column (labeled "normal")
	styles.content.get
	// Left column
	styles.content.getLeft
	// Right column
	styles.content.getRight
	// Border column
	styles.content.getBorder

We can now simply fill our subpart CONTENTRIGHT by copying the object,
which is available as :code:`styles.content.getRight`:

.. code-block:: typoscript

	CONTENTRIGHT = CONTENT
	CONTENTRIGHT < styles.content.getRight

In fact the line :code:`CONTENTRIGHT = CONTENT` is not even needed,
because :code:`styles.content.getRight` itself contains an object definition.
It is only included here to make it more obvious what is happening.

Just for your information, this is the code which would have been needed if
we hadn't had a definition available for copy:

.. code-block:: typoscript

	// get content, right
	CONTENTRIGHT = CONTENT
	CONTENTRIGHT {
		table = tt_content
		select.orderBy = sorting
		select.where = colPos=2
		select.languageField = sys_language_uid
	}

And that is already it! Here you have again the complete TypoScript code for this subpart:

.. code-block:: typoscript

	////////////////////////////////////////////////////////////////////////////////////////////
	//
	// Subpart CONTENTRIGHT
	//
	////////////////////////////////////////////////////////////////////////////////////////////

	// The subpart CONTENTRIGHT outputs the content,
	// which is saved in TYPO3 in the right column of a page
	CONTENTRIGHT = CONTENT
	// Needs the static template from css_styled_content
	// to be included in this template record.
	CONTENTRIGHT < styles.content.getRight

Considering how important this subpart is for our website (after all it outputs the content),
it is surprisingly easy to set up. You might wonder that we did not define rendering instructions
for the different content elements, which you have entered on a page in the TYPO3 CMS backend
and which should be output in the frontend.

Such definitions are also all part of the "CSS Styled Content" static template.

Now that you have defined the CONTENTRIGHT subpart, you can guess already, how we will define CONTENTMIDDLE.
But let us stick to the order of the marks and subparts as we have it in our HTML template.
So we will continue with the DATE mark.
