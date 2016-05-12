
.. include:: ../../../../Includes.txt


.. _configure-contentmiddle:

CONTENTMIDDLE subpart
~~~~~~~~~~~~~~~~~~~~~

This will be very similar to what we did for :ref:`CONTENTRIGHT <configure-contentright>`.
We will use a :code:`CONTENT` object:

.. code-block:: typoscript

	CONTENTMIDDLE = CONTENT

and benefit from the objects already existing in the static template from
"CSS Styled Content", i.e.:

.. code-block:: typoscript

	// Middle column (labeled "normal")
	styles.content.get
	// Left column
	styles.content.getLeft
	// Right column
	styles.content.getRight
	// Border column
	styles.content.getBorder

For CONTENTMIDDLE we want to display the content which corresponds to the column called "normal"
in the page module of the TYPO3 CMS backend. Hence the object to copy is :code:`styles.content.get`:

.. code-block:: typoscript

	CONTENTMIDDLE = CONTENT
	CONTENTMIDDLE < styles.content.get

Again these two lines are enough. This is all that we need to get our content out of the database
and into our page!

Here you again have the complete code for the subpart CONTENTMIDDLE:

.. code-block:: typoscript

	////////////////////////////////////////////////////////////////////////////////////////////
	//
	// Subpart CONTENTMIDDLE
	//
	////////////////////////////////////////////////////////////////////////////////////////////

	// The subpart CONTENTMIDDLE outputs the content of the middle column
	CONTENTMIDDLE = CONTENT
	// Needs the static template from css_styled_content
	// to be included in this template record.
	CONTENTMIDDLE < styles.content.get

This was the last subpart, which we had to configure.
All marks already are configured as well.
So now all marks and subparts get replaced.
When you viewed your web site some steps earlier (when we
created the menus), you could already navigate through the
site (the URLs changed), but there was only dummy text and no real content.
This has changed now.

The tutorial distribution provides a file with the full TypoScript code, in case you
want to check it out. It is located in :file:`fileadmin/doc_tut_templating/TypoScript-code.txt`.
