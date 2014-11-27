.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


.. _load-html-template:

Load the HTML template in the TypoScript template
*************************************************

As you could see from the output of the few lines of TypoScript, which we have above, they only produce the words "HELLO WORLD!".

But that is not, what we want to have. We don't only want to output some words, but we want to output

- first of all our complete template file
- and inside we want to replace our marks and subparts.

So where a TEXT object was defined above, we need to define an object, which outputs a template file. This can be done using the cObject "TEMPLATE". Look it up in TSref!

So instead of the code above we write

.. code-block:: typoscript

	# Default PAGE object:
	page = PAGE

	# Define the template
	page.10 = TEMPLATE


.. tip::

   When you are working with t3editor to edit the Setup field of your TypoScript template,
   you can press Ctrl+S to save what currently is in the Setup field.
   This can make your work noticeably faster.

As TSref tells us, the TEMPLATE cObject has the property "template", in which we can define a cObject, which must be loaded with the template code. This is exactly what we want to do! Since our template is a file, an HTML file, we choose the cObject FILE and add:

.. code-block:: typoscript

	# Our template is a file
	page.10.template = FILE

Did you look up the content object FILE in TSref? If not, do so now!
You will see that for this cObject there is the property "file". The cObject FILE returns the content of the file, which is set in this property. But how exactly do you have to link your file now? This is also answered in TSref. The data type of the property "file" is "resource". You find it in the "Data types reference". There you also find the information that you can link to a file in your TYPO3 installation using a relative path. See the example in TSref. So we add to our template:

.. code-block:: typoscript

	# Our template file is fileadmin/template/index.html
	page.10.template.file = fileadmin/template/index.html

This loads our template file. If you now view your website (the frontend), you will notice that our template file is used, but that in fact the CSS styles are still missing.

So obviously we still have to add a reference to our CSS file to our PAGE object somehow.

The section on the "PAGE object" in TSref tells us how we can add tags to the head tag of the HTML output. There are the properties "stylesheet" and "shortcutIcon", which we want to use to include our stylesheet and our icon:

.. code-block:: typoscript

	# Insert shortcut icon in the head of the website
	page.shortcutIcon = fileadmin/template/favicon.ico
	# Insert stylesheet in the head of the website
	page.stylesheet = fileadmin/template/style.css

Now our Frontend output already has the styles included.

However, if you view the sourcecode of the output, you will notice that TYPO3 created an own HTML structure and inside the body tags of this structure, there is our complete template, with *its* own html, head and body tags and all the content. This is syntactically wrong HTML or in other words: It is no valid HTML page currently.

We will fix this in the next step.
