.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../../Includes.txt


.. _configure-contentright:

CONTENTRIGHT subpart
~~~~~~~~~~~~~~~~~~~~

Using the menus you can now navigate through your website. To check if that works, have a look at the URL bar of your web browser. There you should see a URL ending with something like "index.php?id=75". When you click on a link to another page that id parameter (here the "75") should change.

So in fact we can already visit the according pages that way. You will say "Well, that is nice, but all pages are still showing this "Lorem ipsum" dummy text, which comes from the HTML template." That is true and we will now change this. We will now configure the subpart CONTENTRIGHT.

The subpart CONTENTRIGHT is a special subpart: With this subpart we instruct TYPO3 to get the content of the current page, that is the content of the page which the user has clicked in the menus. We will configure CONTENTRIGHT to get the content for the *right* column of our web pages (and not for the left or middle column) from the database. TYPO3 offers the cObject CONTENT to do that job so we define:

.. code-block:: typoscript

	CONTENTRIGHT = CONTENT

As you can see in TSref the cObject CONTENT has a number of subproperties, which would allow us to define in detail, which records should be selected (and finally displayed). However, there is good news: Do you still remember that I told you to include a static template in your template record? You had to include the static template from the TYPO3 system extension "CSS Styled Content". This static template offers objects, which contain all the lines needed to get the correct contents from the database. In the page module in the TYPO3 Backend you by default see four columns. For each of these columns the static template from CSS Styled Content contains an object, which reads out the contents of that column. These objects have the following names:

.. code-block:: typoscript

	# Middle column (labeled "normal")
	styles.content.get
	# Left column
	styles.content.getLeft
	# Right column
	styles.content.getRight
	# Border column
	styles.content.getBorder

Since we have included the static template before, we can now simply fill our subpart CONTENTRIGHT by copying the object, which is available as "styles.content.getRight". So we add this to our template:

.. code-block:: typoscript

	CONTENTRIGHT = CONTENT
	CONTENTRIGHT < styles.content.getRight

In fact the line "CONTENTRIGHT = CONTENT" is not even needed, because it is directly overwritten again by the definition of styles.content.getRight when we copy this object in the next line. I only included it to make it more obvious what is happening here.

Just for fun we now have a look at the definitions, which we had to write, if the static template was not included:

.. code-block:: typoscript

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

.. code-block:: typoscript

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

Now that you have defined the subpart CONTENTRIGHT, you can guess already, how we will define CONTENTMIDDLE.
But let us stick to the order of the marks and subparts as we have it in our HTML template.
So we will continue with the mark DATE.
