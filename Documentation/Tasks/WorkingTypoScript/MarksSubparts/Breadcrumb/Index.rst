.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../../Includes.txt


.. _configure-breadcrumb:

BREADCRUMB mark
~~~~~~~~~~~~~~~

The mark BREADCRUMB should show a breadcrumb menu. This is a menu, which shows the hierarchical click path, which the user has taken to come to the page on which he currently is.

As it helps the user navigating through the website this also is a kind of menu. As you know we always use the cObject HMENU, when we want to create a menu. So we ammend to our template:

.. code-block:: typoscript

	BREADCRUMB = HMENU

TYPO3 CMS offers a special functionality to create a breadcrumb menu; maybe you have already seen it when we created our meta navigation (the menu with the few pages, which are always displayed at the top, no matter on which page the user currently is). The cObject HMENU has a property called "special", which has some values. With each of them you can create a special kind of menu. One of these values is called "rootline" and this basically is just another term for the pages, which we want to see in our menu. So let us add that:

.. code-block:: typoscript

	BREADCRUMB = HMENU
	BREADCRUMB {
		special = rootline

Now there also are some options for the rootline menu. The most important property is the one called "special.range".

This property is a bit more complex, but you will get it. "special.range" takes two integers as values, seperated by a pipe. For example "special.range = 0|5". With this property we can define the range of our menu. Or in other words we can set the level of the first page in our menu and the level of the last page in our menu. The number in front of the pipe (in our example the "0") defines the level of the first page in our menu. The number behind the pipe (in our example the "5") defines the last level, which should be shown in the menu. All pages in the click path between and including these two levels will be included in the menu.

Now let's have a look at the meaning of the numbers: The root page is on level 0. Positive values stand for page levels further outwards. So with our example "special.range = 0|5" we would get a rootline menu which starts with the root page (level 0) and then shows the active pages on each level for up to 5 levels below the root page. (This all provided that the user currently is that deep into the structure of the website. If the user is for instance on level 2 currently, the rootline ends on level 2 and so will the output of our rootline menu.)

We want to create a special rootline: Our menu should not begin with the rootpage, because this page only is a redirect to the page "Home" on level 1. So we want our menu to start one level below the rootpage, which makes the first part of the value of special.range a "1".

Then the menu should show all pages up to the current page. But how can we do that? The problem is that right now, where we are writing this code, we do not know on which page level the user is when he clicks a page. We do not know, how deep our website will be and basically the user could be on any page level. For this dilemma there is a solution: We can also define negative numbers for each of the values in special.range. Negative values begin with the outermost level of the current rootline and go inwards. For example -1 stands for the page on the outermost level of the current rootline. (This must not necessarily be the page, which is on the outermost level in the *page tree*!) So the value we want is "-1".

With this knowledge we can now define the value of special.range as we need it:

.. code-block:: typoscript

	BREADCRUMB = HMENU
	BREADCRUMB {
		  special = rootline
		  special.range = 1|-1

Inside our HMENU we again define a TMENU

.. code-block:: typoscript

	1 = TMENU
	1 {

When you have a look at our HTML template again you will see that in the rootline menu there are links to the pages and between the links we have greater-than signs. In the other menus we have always differentiated the items by their item state. That way e.g. the current page could be rendered differently. This is also what we could do here. We could add:

.. code-block:: typoscript

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

- :code:`|*|` splits the list of menu items into up to three parts. A part can include one or more menu items.
  The number of items per part is defined through :code:`||`.

- :code:`||`  splits the parts in subparts. You can freely choose the number of subparts inside each part.
  Each subpart is one item. That way you can define different instructions for the menu items depending on
  their position.

Abstractly:

.. code-block:: typoscript

	NO.allWrap = first|*|middle|*|last

"first" is prepended to the first item, "last" to the last one and "middle" to all others.
The priority of the parts in fact is last, first, middle. This is important,
if there e.g. are only two pages in the menu.

In our breadcrumb menu we only have two different cases: We want the ">" sign in front of all pages,
but not in front of the first one.

The easiest way to do that is to split the first part into subparts:

.. code-block:: typoscript

	NO.allWrap = ||&nbsp;>&nbsp;

Since there was no :code:`|*|`, both subparts belong to part one. The first subpart of part one is empty,
so there will be nothing in front of the first menu item. The second subpart of part one contains the ">" sign,
which will be used in front of item two. If our menu has more items, the second subpart is repeated for
all other items prepending them with ">" as well.

After these goodies, here you again have the complete setup code for that mark:

.. code-block:: typoscript

	##############################################
	#
	# Mark BREADCRUMB
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

After that many new things just for the mark BREADCRUMB, we will have a look at the mark TITLE.
No fear, compared to the last mark it will be like a walk in the park.
