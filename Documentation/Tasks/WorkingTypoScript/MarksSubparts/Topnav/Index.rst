.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../../Includes.txt


.. _configure-topnav:

TOPNAV subpart
~~~~~~~~~~~~~~

The subpart TOPNAV displays our main menu, which is located inside the orange bar at the top of the page. Here again is the structure of the HTML code, which we need to create:

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

Since we want to display a menu we again begin defining an HMENU

.. code-block:: typoscript

	TOPNAV = HMENU

This time we have to wrap the menu in a div tag and - inside the div tag - into ul tags. We could put both into the same property now, like

.. code-block:: typoscript

	TOPNAV.wrap = <div id="nav_main"><ul>|</ul></div>

but there also is a way, which makes our definitions look nicer to the eye: We define both wraps seperately. Like every cObject HMENU also provides a property named "stdWrap". TYPO3 applies this property after all other properties of the object have been computed. Behind stdWrap there is a very powerful function; it is a kind of "Swiss knife", which offers a big number of functionalities. This property has many subproperties (just look at the section "stdWrap" in TSref) with which you can do lots of different things: You can for example format the content of a cObject, you can change the case of the content, you can output the content based on a condition or you can add data from the database. However, this is just to give you a quick overview of what stdWrap can do for you. Here we only use the "wrap" property of stdWrap to add a normal wrap. Basically you already know how that is working. So we add this to our template:

.. code-block:: typoscript

	TOPNAV.wrap = <ul>|</ul>
	TOPNAV.stdWrap.wrap = <div id="nav_main">|</div>

Note that the order in which we define TOPNAV.wrap and TOPNAV.stdWrap.wrap does not matter. TYPO3 always applies different properties of an object based on the order, which is coded inside TYPO3. (And in this case "wrap" is computed before "stdWrap.wrap".)

When you had a look at our HTML template you might have noticed that there in fact are two menus: One in the orange bar at the top and one in the left column below the orange bar. The menu at the top (TOPNAV) should only display the first level of pages. The menu in the left column (SUBNAV) should display the subpages for that one page, which is currently selected from the top menu. We will configure SUBNAV later; now we are only interested in TOPNAV.

So what we want to output in the menu is a list of the pages, which we have on level 1 of our page tree in TYPO3. Again we use a textual menu. So we need to define

.. code-block:: typoscript

	TOPNAV.1 = TMENU
	TOPNAV.1 {

	}

As the normal rendering (the default rendering) we again need li tags:

.. code-block:: typoscript

	TOPNAV.1 {

		# Definitions per page
		# NO: default formatting
		NO = 1
		NO {
			allWrap = <li>|</li>
		}
	}

But did you see that there is one page in the main menu, which has the CSS ID "current" in the li tag? This ID should be used for the page, which is somehow active currently: Either because the user currently is *on* that page or because he is *below* that page. The CSS ID is used in our CSS stylesheet to render that one link differently.

So this time we also have to define another item state besides "NO". You have already learnt that for our case we need to configure the state "ACT". This state offers the same properties as the state NO does. So we add this to the definition of our TMENU:

.. code-block:: typoscript

	TOPNAV.1 {

		# ACT: User is on this or below this page
		# Activate this state for this menu
		ACT = 1
		ACT {
			allWrap = <li id="current">|</li>
		}

That way a page, which is active (because the user is on that page or on a subpage below that page), is wrapped with this wrap instead of the one coming from NO.

This completes our TypoScript code for the subpart TOPNAV. Here is the complete code for that subpart. The order of the properties again is slightly restructured and the code is indented:

.. code-block:: typoscript

	##############################################
	#
	# Subpart TOPNAV
	#
	##############################################
	# The subpart TOPNAV outputs the main navigation
	TOPNAV = HMENU
	TOPNAV.wrap = <ul>|</ul>
	# "stdWrap" properties are applied after "wrap".
	TOPNAV.stdWrap.wrap = <div id="nav_main">|</div>

	# Definition for pages on the first level of the menu
	TOPNAV.1 = TMENU
	TOPNAV.1 {

		# Definitions per page
		# NO: default formatting
		NO = 1
		NO {
			# Each entry is wrapped by
			# <li> </li>
			allWrap = <li>|</li>
		}

		# ACT: User is on this or below this page
		# Activate this state for this menu
		ACT = 1
		ACT {
			# Use another wrap
			allWrap = <li id="current">|</li>
		}
	}

With this code added to our TypoScript template, the main navigation in the orange bar is already working. If you now view the Frontend (that is the website, which is produced by TYPO3), you will see that inside the orange bar we already see the titles of the pages, which we have created on the first level of the page tree inside the TYPO3 Backend some steps before. If you click one of these pages in the Frontend (inside the orange bar), you will also notice how the active page is displayed differently. A look at the source code of the frontend output shows us that for this page TYPO3 uses the wrap, which we have defined for the state ACT.
