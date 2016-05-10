
.. include:: ../../../Includes.txt


.. _load-html-template:

Load the HTML template in the TypoScript template
*************************************************

As you could see above, our template does not currently produce an interesting
output. What we really want is to:

- use our complete HTML template file
- display actual content from TYPO3 CMS within that template.

To proceed with this, we first change the content of the :code:`PAGE`
object to use a :ref:`TEMPLATE object <t3tsref:cobj-template>`:

.. code-block:: typoscript

	# Default PAGE object:
	page = PAGE

	# Define the template
	page.10 = TEMPLATE


.. tip::

   When you are working with t3editor to edit the Setup field of your TypoScript template,
   you can press Ctrl+S to save what currently is in the Setup field.
   This can make your work noticeably faster.

The TEMPLATE cObject has a property called :code:`template`, in which we can define a cObject
which will be loaded with the template code. This is exactly what we want to do!
Since our template is a file, an HTML file, we choose the cObject
:ref:`FILE <t3tsref:cobj-file>` and add:

.. code-block:: typoscript

	# Our template is a file
	page.10.template = FILE

Do you know what the next step is? Did you look up the content object :ref:`FILE <t3tsref:cobj-file>` in TSref?
If not, do so now! You will see that for this object there is a property called :code:`file`.
The :code:`FILE` object returns the content of the file, which is set in this property.

But how exactly do you have to link your file now? This is also answered in the TSref.
The data type of the :code:`file` property is :ref:`resource <t3tsref:data-type-resource>`.
The TSref indicates that you can point to a file in your TYPO3 CMS installation using a relative path.
So we add to our template:

.. code-block:: typoscript

	# Our template file is fileadmin/doc_tut_templating/index.html
	page.10.template.file = fileadmin/doc_tut_templating/index.html

This loads our template file. If you now view your website (the frontend),
you will notice that our template file is used, but that the CSS styles is missing.

Something is missing...

Going through the TSref for the :code:`PAGE` we can find several ways to include
a reference to CSS file. The favored one is the property called :code:`includeCSS`,
which is an arrray making it possible to include several files.
While we are at it, let's also add a :code:`shortcutIcon`:

.. code-block:: typoscript

	# Insert shortcut icon in the head of the website
	page.shortcutIcon = fileadmin/doc_tut_templating/favicon.ico
	# Insert stylesheet in the head of the website
	page.includeCSS.base = fileadmin/doc_tut_templating/style.css

Now our frontend output already has the styles included.

However, if you view the sourcecode of the output, you will notice that TYPO3 CMS created its own HTML structure,
inside of which is our own HTML template, complete :code:`<html>`, :code:`<head>` and :code:`body` tags and all the content.
This is obviously not what we want and also not syntactically correct.

We will fix this in the next steps.
