.. include:: ../../../../Includes.txt


.. _configure-subnav:

SUBNAV subpart
~~~~~~~~~~~~~~

Next we will configure the subpart SUBNAV. This subpart should render the sub navigation,
which will be displayed in the left column of the Frontend output.

Basically this again is a normal menu, but with a couple of twists. First of all,
it should not show the pages which are on the first level of the page tree, but instead
those which are below the active page on level 1. Furthermore the sub navigation
should also show pages on deeper levels like on level 3. So we also have to configure this level.

Here again is the structure of the HTML code, which we need to replace:

.. code-block:: html

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

We again define a :code:`HMENU`:

.. code-block:: typoscript

	SUBNAV = HMENU

Now we have to set the level of the page tree on which the menu should begin.
This can be done with the property :code:`entryLevel`, which is provided
by the :code:`HMENU` object. If it is set to :code:`0`, the menu begins with
the first level of pages below the root page. That is what is used in
the top menu TOPNAV by default Here we want to start one level deeper,
so we et:

.. code-block:: typoscript

	SUBNAV = HMENU
	SUBNAV.entryLevel = 1

.. note::

   Setting an :code:`entryLevel` does not change le numbers used for
   levels inside the menu object. The first level is still "1", the next
   one "2", etc.

Given the HTML code above we can see that we have the same structure on level 1 as on level 2,
i.e.:

- we need one :code:`<ul>` tag around the whole menu and each item on the first level
  must be wrapped in :code:`<li>` tags.

- where a menu item has subpages, we need a :code:`<ul>` tag inside the :code:`<li>` tag.
  Inside that :code:`<ul>` tag, the next level of pages should be rendered.
  :code:`<ul>` tags will end up nested, as in the HTML code above.

Since the structure of both levels of the menu are nearly the same, we will now
define the structure for the first level and then copy that structure for the second level,
with just a few changes.

In the TOPNAV, the :code:`wrap` could be placed on the :code:`HMENU` object because the
menu only had a single level. In the case of the SUBNAV, we want to place the :code:`wrap`
on the :code:`TMENU` object instead. In a way this is also more logical, even if there
was a single menu level.

.. code-block:: typoscript

	SUBNAV {

		// Definition for pages on the first level of the menu
		1 = TMENU
		1 {
			wrap = <ul id="submenu">|</ul>

There's another important consideration for multiple-level menus: do you want to see all child
pages of the current page or also children of the sibling pages? The latter is more often the case.
This behaviour can be toggled on and off with the :code:`expAll` property.

.. code-block:: typoscript

	1 = TMENU
	1 {
		wrap = <ul id="submenu">|</ul>
		expAll = 1

Now let's have a look at the rendering definition for a single item on level 1, when it is in normal state.
We want to wrap each item on level 1 in an :code:`<li>` tag, but that tag should be wrapped around the
:code:`<ul>` structure of its child pages. In that case the :code:`allWrap` property which we have used
so far in the METANAV and TOPNAV menus is not appropriate, because it wil wrap only around the menu item
itself and not around the child structure, thus generating invalid HTML. Luckily there is a specific
property just for this case, called :code:`wrapItemAndSub`:

.. code-block:: typoscript

	SUBNAV.1 {
		// Definition per page
		// NO: default formatting
		NO = 1
		NO {
			wrapItemAndSub = <li>|</li>
		}
	}

This menu also has an active state, which we need to define. We also need to use the :code:`wrapItemAndSub`
property for the :code:`ACT` state:

.. code-block:: typoscript

	SUBNAV.1 {
		ACT = 1
		ACT {
			// Use another wrap
			wrapItemAndSub = <li id="active">|</li>
		}
	}


With that, the definition of our first menu level is complete.

As we discussed earlier, the structure for the second level is basically the same. It would be a shame
writing the same TypoScript code again. Instead we want to use the possiblity to copy TypoScript
objects, so that :code:`SUBNAV.2` starts out the same as :code:`SUBNAV.1`.

Until now we always used the :code:`=` operator to assign a value to a property.
Copying an object works with the :code:`<` operator.

Let's first look at a simple example, where we copy an object called HEADERTITLE
to ANOTHEROBJECT.

.. code-block:: typoscript

	page.10.marks {
		HEADERTITLE = TEXT
		HEADERTITLE.value = TYPO3

		// Create a copy of HEADERTITLE in ANOTHEROBJECT
		ANOTHEROBJECT < page.10.marks.HEADERTITLE
	}

With this code we define the object ANOTHEROBJECT and set its content to be a copy of object HEADERTITLE.
Copying also includes all subproperties and their values. Which means that the example above also sets
:code:`ANOTHEROBJECT.value` to the value "TYPO3".

When copying on the same level, you can just refer to the name of the copied object, prepended by a dot:

.. code-block:: typoscript

	page.10.marks {
		HEADERTITLE = TEXT
		HEADERTITLE.value = TYPO3

		// Create a copy of HEADERTITLE in ANOTHEROBJECT
		ANOTHEROBJECT < .HEADERTITLE
	}

This produces the same result as the example above, but it is even more readable. We will
use this "short notation" for our menu level copy.

Back to our template record. Here is our TypoScript code so far, with the copy of the first
level to the second level:

.. code-block:: typoscript

	SUBNAV = HMENU
	SUBNAV {

		// Definition for pages on level 1
		1 = TMENU
		1 {
			NO = 1

			ACT = 1
		}

		// Definition for pages on level 2
		// Copy the definitions from level 1
		2 < .1
	}

The line :code:`2 < .1` is all it takes to create a complete copy of all the definitions.

.. important::

   Do not forget the dot in front of the copied object. Remember that it means that you point to an object on the same level,
   i.e. a child of the same parent object.

Looking at our HTML template again we see that there is one small difference in the output of the pages on level 2:
the :code:`<ul>` tag on the second level is different. It does not have an :code:`id="submenu"` attribute
as there exists on level 1. So we need overwrite the :code:`wrap` on level 2
**after** the copy operation:

.. code-block:: typoscript

	SUBNAV = HMENU
	SUBNAV {

		// Definition for pages on level 2
		// Copy the definitions from level 1,
		// but use another wrap.
		2 < .1
		2.wrap = <ul>|</ul>

That's it! Our submenu now can display up to two levels of pages. This should be enough for most web sites.

Again here is the whole TypoScript code of that subpart, slightly restructured and nicely indented:

.. code-block:: typoscript

	SUBNAV = HMENU
	SUBNAV {
		// Only display subpages of the page from the main
		// navigation, which is in the current rootline.
		// Default value of entryLevel is 0, which are the
		// pages on the first level.
		// We want to begin with those subpages on level 2.
		entryLevel = 1

		// Definition for pages on level 1
		1 = TMENU
		1 {
			wrap = <ul id="submenu">|</ul>
			// Always expand all subpages.
			expAll = 1

			// Definition per page
			// NO: default formatting
			NO = 1
			NO {
				// Each entry is wrapped by
				// <li> </li>
				wrapItemAndSub = <li>|</li>
			}

			// ACT: User is on this or below this page
			// Activate this state for this menu
			ACT = 1
			ACT {
				// Use another wrap
				wrapItemAndSub = <li id="active">|</li>
			}
		}

		// Definition for pages on level 2
		// Copy the definitions from level 1,
		// but use another wrap.
		2 < .1
		2.wrap = <ul>|</ul>
	}

Now we have defined the meta navigation, the top navigation and the sub navigation.
All menus in our site are configured now and should display links to TYPO3 CMS pages.
However all pages still display the same dummy text and the content from the TYPO3 CMS.
We will change this in the next chapters.
