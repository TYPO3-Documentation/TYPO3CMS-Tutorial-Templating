
.. include:: ../../../../Includes.txt


.. _configure-breadcrumb:

BREADCRUMB mark
~~~~~~~~~~~~~~~

The mark BREADCRUMB should show a breadcrumb trail, i.e. the path in the web site which leads
to the current page.

In TYPO3 CMS this also considered to be a kind of menu and - as such - we will be using
our old friend :code:`HMENU`. And so we start again:

.. code-block:: typoscript

	BREADCRUMB = HMENU

As we saw while creating the METANAV, TYPO3 CMS offers several "special" menus.
One such type is called "rootline" and corresponds exactly to the definition of a
breadcrumb trail. Hence:

.. code-block:: typoscript

	BREADCRUMB = HMENU
	BREADCRUMB {
		special = rootline

The "rootline" menu has its own options, the most important one being :code:`special.range`.

:code:`special.range` takes two integers as values, seperated by a pipe.
For example :code:`special.range = 0|5`. With this property we can define the range of our menu,
i.e. from which page tree level it should start (e.g. :code:`0`) and at which level it should stop
(e.g. :code:`5`). All pages along the trail between these two levels (and include those exactly
at the levels) will be included in the menu.

Let's have a look at the meaning of the numbers. The root page is on level 0.
Positive values stand for page levels deeper down. Our example corresponds to a
rootline menu starting with the root page (level 0) and including the active pages on each level
down to 5 levels below the root page. Obviously the menu does not display pages deeper
than the one is user is currently on.

It our case, we don't want the BREADCRUMB to start on the root level, because the root page
is just a redirection to the page called "Home". Hence we want our range to start with :code:`1`.

But how can we set the end of our range without knowing the depth the page tree may reach
when our web site finished. The solutions is to use negative numbers in the range. Negative values
begin with the deepest level of the current rootline and go upwards. As such :code:`-1`
stands for the page on the deepest level of the current rootline. And that's exactly the value
that we want.

Thus we can write:

.. code-block:: typoscript

	BREADCRUMB = HMENU
	BREADCRUMB {
		  special = rootline
		  special.range = 1|-1

Inside our :code:`HMENU` we again define a :code:`TMENU`:

.. code-block:: typoscript

	1 = TMENU
	1 {

Our HTML template says that in the rootline menu is comprised of links to the pages,
with "greater than" signs (:code:`>`) in between. We also want to differentiate the
current page from the others pages:

.. code-block:: typoscript

	NO = 1
	NO.allWrap = |&nbsp;>&nbsp;

	CUR = 1
	CUR.allWrap = |

This shows a "greater than" sign (:code:`>`) after each page, except after the current page
(which always is the last page in the rootline).

This could be written differently using a feature called :ref:`optionSplit <t3tsref:objects-optionsplit>`.
However this feature is quite complex and beyond the scope of this tutorial.
It is well documented in the TSref.

Here again is the complete setup code for that mark:

.. code-block:: typoscript

	////////////////////////////////////////////////////////////////////////////////////////////
	//
	// Mark BREADCRUMB
	//
	////////////////////////////////////////////////////////////////////////////////////////////

	// Outputs a menu which shows a click path to
	// the current page.
	BREADCRUMB = HMENU

	BREADCRUMB {
		special = rootline
		// Range: Syntax is "Start level|End level"
		// Values for both:
		// 0 stands for the root page, positive values go outwards.
		// Negative values begin with the outermost level of the current
		// rootline and go inwards;
		// e.g. -1 stands for the page on the outermost level of the
		// current rootline.
		// Start level: 1 = The page one level below the root page.
		// End level: -1 = The current page.
		special.range = 1|-1

		1 = TMENU
		1 {

			// We want greater-than signs between the menu items.
			// So each item should be wrapped with ">" except for the
			// last (= current) one.
			NO = 1
			NO.allWrap = |&nbsp;>&nbsp;
			CUR = 1
			CUR.allWrap = |
		}
	}

Let's move on to the TITLE mark.
