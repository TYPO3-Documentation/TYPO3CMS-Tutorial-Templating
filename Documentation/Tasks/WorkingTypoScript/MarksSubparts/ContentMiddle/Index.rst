.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../../Includes.txt


.. _configure-contentmiddle:

CONTENTMIDDLE subpart
~~~~~~~~~~~~~~~~~~~~~

I don't want to bore you. You already know how this is working, at least you have already configured the subpart CONTENTRIGHT.

There you have already learnt that it is a help, that you have included the static template of the extension CSS Styled Content. You know that you can define

.. code-block:: typoscript

	CONTENTMIDDLE = CONTENT

to use a content object and you might remember that this line was not needed at all, because it will just be overwritten, when we define the next line where we copy the according object from the static template. The four objects, which help us get the content for the according column were named

.. code-block:: typoscript

	# Middle column (labeled "normal")
	styles.content.get
	# Left column
	styles.content.getLeft
	# Right column
	styles.content.getRight
	# Border column
	styles.content.getBorder

Here we want to get the content, which is saved in the column called "normal" in the page module of the TYPO3 Backend. The object, which we copy to get the content from that column, is named styles.content.get. So we add

.. code-block:: typoscript

	CONTENTMIDDLE = CONTENT
	CONTENTMIDDLE < styles.content.get

Again we do not need more than these two lines. This is all to get our content out of the database and into our page!

Here you again have the complete code for the subpart CONTENTMIDDLE:

.. code-block:: typoscript

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

This was the last subpart, which we had to configure.
All marks already are configured as well.
So now all marks and subparts get replaced.
When you viewed your website some steps before (when we
created the menus), you could already navigate through the
site (the URLs changed), but there was only that dummy text and no real content.
This has changed now.
