.. include:: /Includes.rst.txt


.. _use-html-template:

Use any HTML template
*********************

.. note::

   You can open and edit HTML files with any text editor. However, you will make your life much easier,
   if you use an editor, which supports syntax highlighting. With syntax highlighting you will see directly
   where a certain tag begins, where it ends, where there are attributes and so on.

   If you don't already have one of these, a quick search on Internet will turn up
   a lot of them and you should be able to find one which runs on your computer
   and with which you are comfortable.


Our HTML template is very simple, but has many parts we can later point to:

.. code-block:: html

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
			<div id="page_margins">
				<div id="page" class="hold_floats">
					<div id="header">
						<div id="logo">
							<img src="/path/to/logofile.svg" alt="Logo" />
						</div>
					</div>
					<nav id="mainnav">
						<ul>
							<li>Home</li>
							<li>About</li>
							<li>
								References
								<ul>
									<li>Category 1</li>
									<li>Category 2</li>
								</ul>
							</li>
							<li>Get in contact</li>
						</ul>
					</nav>
					<div id="content">
						...
					</div>
					<div id="footer">
						<nav id="footernav">
							<ul>
								<li><a href="#">Contact</a></li>
								<li><a href="#">Imprint</a></li>
							</ul>
						</nav>
					</div>
				</div>
			</div>
		</body>
	</html>

.. _prepare-html-template:

Prepare HTML template
*********************

.. hint::
   We suggest to copy the original HTML template to a place in your versioning
   system for further work. Best way is a so-called SitePackage which is a TYPO3
   extension which includes the Fluid templates (partials/layouts), CSS stylesheets
   and JavaScript.

After creating a copy of the HTML template we remove all parts but the HTML within the `<body>` part:

.. code-block:: html

	<div id="page_margins">
		<div id="page" class="hold_floats">
			<div id="header">
				<div id="logo">
					<img src="/path/to/logofile.svg" alt="Logo" />
				</div>
			</div>
			<nav id="mainnav">
				<ul>
					<li>Home</li>
					<li>About</li>
					<li>
						References
						<ul>
							<li>Category 1</li>
							<li>Category 2</li>
						</ul>
					</li>
					<li>Get in contact</li>
				</ul>
			</nav>
			<div id="content">
				...
			</div>
			<div id="footer">
				<nav id="footernav">
					<ul>
						<li><a href="#">Contact</a></li>
						<li><a href="#">Imprint</a></li>
					</ul>
				</nav>
			</div>
		</div>
	</div>


Build <head> in TypoScript
**************************

.. code-block:: typoscript

   # General page
   page = PAGE

   # Include CSS in any directory
   page.includeCSS.name = relative/path/to/file/based/on/document/root/file.css

   # Include CSS in extensions (site package)
   page.includeCSS.name = EXT:site_package/Resources/Public/Css/File.css

   # Include JS as library, loaded before the normal JS (header or footer)
   page.includeJSlibs.name = EXT:site_package/Resources/Public/JavaScript/File.js
   page.includeJSFooterlibs.name = EXT:site_package/Resources/Public/JavaScript/File.js

   # Include JS (header or footer)
   page.includeJS.name = EXT:site_package/Resources/Public/JavaScript/File.js
   page.includeJSFooter.name = EXT:site_package/Resources/Public/JavaScript/File.js

   # Class in <body> tag
   page.bodyTag = <body class="myclass">

   # META information
   # page.meta.<name> = <value>
   page.meta.description = My description




