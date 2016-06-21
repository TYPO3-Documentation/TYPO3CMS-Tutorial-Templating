.. include:: ../../../../Includes.txt


.. _configure-topnav:

TOPNAV subpart
~~~~~~~~~~~~~~

The subpart TOPNAV displays our main menu, which is located
inside the orange bar at the top of the page. Here again is
the structure of the HTML code, which we need to create:

.. code-block:: html

    <div id="nav">
        <!-- ###TOPNAV### Start -->
        <div id="nav_main">
            <ul>
                <li><a>Menu Item 1</a></li>
                <li><a>Menu Item 2</a></li>
                <li id="current"><a>Menu Item 3</a></li>
                <li><a>Menu Item 4</a></li>
            </ul>
        </div>
        <!-- ###TOPNAV### End -->
    </div>

Since we want to display a menu we again begin defining a :code:`HMENU` object:

.. code-block:: typoscript

	TOPNAV = HMENU

This time we have to wrap the menu in a :code:`<div>` tag and - inside that tag -
into :code:`<ul>` tags. We could put both into the same property now, like:

.. code-block:: typoscript

	TOPNAV.wrap = <div id="nav_main"><ul>|</ul></div>

but there also is a way, which makes our definitions look nicer to the eye:
we define both wraps seperately. Like every content object :code:`HMENU` also
provides a property named :code:`stdWrap`. TYPO3 CMS applies this property
after all other properties of the object have been computed.

.. tip::

   If you don't remember exactly what :code:`stdWrap` does, you may want
   to refresh your knowledge by returning to the :ref:`TypoScript in 45 Minutes Tutorial <t3ts45:using-stdwrap>`.

Here we only use the :code:`wrap` property of :code:`stdWrap` to add a normal wrap.
So we add this to our template:

.. code-block:: typoscript

	TOPNAV.wrap = <ul>|</ul>
	TOPNAV.stdWrap.wrap = <div id="nav_main">|</div>

Note that the order in which we define :code:`TOPNAV.wrap` and :code:`TOPNAV.stdWrap.wrap` does not matter.
TYPO3 CMS always applies different properties of an object based on the order,
which is coded inside TYPO3 CMS (and in this case :code:`wrap` is computed before :code:`stdWrap.wrap`).

When you had a look at our HTML template you might have noticed that there in fact are two menus:
one in the orange bar at the top and one in the left column below the orange bar.
The menu at the top (TOPNAV) should only display the first level of pages.
The menu in the left column (SUBNAV) should display the subpages for the current page.
We will configure SUBNAV later; now we are only interested in TOPNAV.

So what we want to output in the menu is a list of the pages, which we have on level 1 of our page tree in TYPO3 CMS.
Again we use a textual menu. So we need to define

.. code-block:: typoscript

	TOPNAV.1 = TMENU
	TOPNAV.1 {

	}

For the normal rendering (the default rendering) we again need :code:`<li>` tags:

.. code-block:: typoscript

	TOPNAV.1 {

		// Definitions per page
		// NO: default formatting
		NO = 1
		NO {
			allWrap = <li>|</li>
		}
	}

We also want to apply a different style in the menu to the page that either matches
the current page or is part of the navigation leading to the current page.
So this time we also have to define another item state besides :code:`NO`.
In our case we need to configure the state :code:`ACT`, which has the same properties
as the state :code:`NO` does. So we add this to the definition of our :code:`TMENU`:

.. code-block:: typoscript

	TOPNAV.1 {

		// ACT: User is on this or below this page
		// Activate this state for this menu
		ACT = 1
		ACT {
			allWrap = <li id="current">|</li>
		}

This completes our TypoScript code for the subpart TOPNAV. Here is the complete code for that subpart.
The order of the properties again is slightly restructured and the code is indented:

.. code-block:: typoscript

	////////////////////////////////////////////////////////////////////////////////////////////
	//
	// Subpart TOPNAV
	//
	////////////////////////////////////////////////////////////////////////////////////////////

	// The subpart TOPNAV outputs the main navigation
	TOPNAV = HMENU
	TOPNAV.wrap = <ul>|</ul>
	// "stdWrap" properties are applied after "wrap".
	TOPNAV.stdWrap.wrap = <div id="nav_main">|</div>

	// Definition for pages on the first level of the menu
	TOPNAV.1 = TMENU
	TOPNAV.1 {

		// Definitions per page
		// NO: default formatting
		NO = 1
		NO {
			// Each entry is wrapped by
			// <li> </li>
			allWrap = <li>|</li>
		}

		// ACT: User is on this or below this page
		// Activate this state for this menu
		ACT = 1
		ACT {
			// Use another wrap
			allWrap = <li id="current">|</li>
		}
	}

With this code added to our TypoScript template, the main navigation in the orange bar is already working.
If you now view the frontend, you will see that the pages created in the TYPO3 CMS backend appear inside
the orange bar. Click around the menu and see how the active page updates automatically, as per our
definition of the :code:`ACT` state.
