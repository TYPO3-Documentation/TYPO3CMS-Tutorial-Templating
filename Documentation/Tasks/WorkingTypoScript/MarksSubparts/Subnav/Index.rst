.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../../Includes.txt


.. _configure-subnav:

SUBNAV subpart
~~~~~~~~~~~~~~

Next we will configure the subpart SUBNAV. This subpart should render the sub navigation, which will be displayed in the left column of the Frontend output.

Basically this again is a normal menu, but it has some specifics: It should not show the pages, which are on level 1 of the page tree, but instead it shows the pages, which are *below* the page on level 1, which is currently *active*. So the first level of pages, which should appear in this menu are the pages on level 2 of the page tree.
Furthermore the sub navigation should also show pages on deeper levels like on level 3. So we also have to configure this level.

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

We again define an HMENU:

.. code-block:: typoscript

	SUBNAV = HMENU

Now we have to set the level of pages of the page tree, with which the menu should begin. This can be done with the property "entryLevel", which is provided by the object HMENU. If it is set to "0", the menu begins with the first level of pages below the root page. That is what is used in the top menu TOPNAV. (In fact we did not have to set entryLevel to "0" explicitly there, because "0" is the default value.) But here we want the menu not to start with the pages, which are directly below the root page, but with the ones, which are one level deeper. So we add:

.. code-block:: typoscript

	SUBNAV = HMENU
	SUBNAV.entryLevel = 1

Now independently from the question of the entryLevel: When you have a look at the above screenshot you will see that the HTML code of the menu basically has the same structure for the pages on level 1 as for the pages on level 2. Here is what the structure looks like:

- We need one ul tag around the whole menu and each item on the first level must be wrapped in li tags.

- Where a menu item has subpages, there inside the li tag we need a ul tag and inside that ul tag the next level of pages should be rendered. Have a look at the screenshot above. There "Submenu Item 3" shows this situation.

Since the structure of both levels of the menu basically is the same we will now define the structure for the pages on level one, will then copy that structure for the pages on level two and only make the few changes there, which are needed.

To have things structured logically, I add the outer ul tags not to the wrap of the HMENU like we did e.g. for TOPNAV, but to the wrap of the first level of pages of the TMENU. In the end this does not make a difference in the rendering, the wrap in both cases appears at the same place. But having it inside the first level of the TMENU I can also copy that wrap, when I create the instructions for pages on level 2.

.. code-block:: typoscript

	SUBNAV {

		# Definition for pages on the first level of the menu
		1 = TMENU
		1 {
			wrap = <ul id="submenu">|</ul>

Something else which is important when you can have multiple levels of pages in a menu is the question, if you always want to see all subpages. By default TYPO3 only shows the subpages of *the* page, which currently is active. In contrast I want TYPO3 to always show all subpages, also the ones of pages, which the user is not on currently. This can be done with the property expAll:

.. code-block:: typoscript

	1 = TMENU
	1 {
		wrap = <ul id="submenu">|</ul>
		expAll = 1

Now let's have a look at the rendering definition for a single item on level 1, when it is in normal state. We want to wrap each item on level 1 in an li tag. In the menus METANAV and TOPNAV we always used the property "allWrap" to do this kind of task. However, this property only wraps the item itself. But when we have an item with subpages, these subpages would not be included in the wrap, but would follow after it. With other words: allWrap would insert the closing li tag, before the tags for the subpages start (that is the ul tag and the li tags inside it). This would lead to invalid HTML; the nesting of the different tags would no longer be valid. So what we need here is a property, which does not only wrap the menu item, which we have currently, but also all subitems. The result should be that the closing li tag is inserted *after* the subpages. This can be done with "wrapItemAndSub". So we add this to our template:

.. code-block:: typoscript

	SUBNAV.1 {
		# Definition per page
		# NO: default formatting
		NO = 1
		NO {
			wrapItemAndSub = <li>|</li>
		}
	}

As you see in the HTML template there also is the CSS ID "active", which should be added to that one menu item, which currently is active. So again it is not enough to just define NO as normal default state and to always use that state, but we also have to add a special definition for the case of a page being active. So we need to define this different wrap in the property "wrapItemAndSub" of the object "ACT", so that it overwrites our normal default wrap:

.. code-block:: typoscript

	SUBNAV.1 {
		ACT = 1
		ACT {
			# Use another wrap
			wrapItemAndSub = <li id="active">|</li>
		}
	}


Now we have the definitions for the pages in the first level of our menu complete.

The next thing to do is to add the defintions for pages, which are displayed in the second level of our menu. You already know that - while the rendering of the pages for the first level of our menu is defined in "SUBNAV.1" - the rendering for the pages on level 2 will be done in "SUBNAV.2". As I explained above, we will not define each of these lines again for level 2, because they are nearly identical. Instead you will now learn how to copy objects in TypoScript.

Until now we always used the operator "=" to assign a value to a property. Copying an object works with the operator "<".

Before we continue with our template it makes sense to explain this with an example. I have the object HEADERTITLE. Now I can create a copy of it and call the copy ANOTHEROBJECT:

.. code-block:: typoscript

	page.10.marks {
		HEADERTITLE = TEXT
		HEADERTITLE.value = TYPO3

		# Create a copy of HEADERTITLE in ANOTHEROBJECT
		ANOTHEROBJECT < page.10.marks.HEADERTITLE
	}

With this definition we define the object ANOTHEROBJECT and set its content to a copy of the object HEADERTITLE. Copying also includes all subproperties and their values. The example above also sets ANOTHEROBJECT.value to the value "TYPO3".

When copying on the same level, you can just refer to the name of the copied object, prepended by a dot. See the following code:

.. code-block:: typoscript

	page.10.marks {
		HEADERTITLE = TEXT
		HEADERTITLE.value = TYPO3

		# Create a copy of HEADERTITLE in ANOTHEROBJECT
		ANOTHEROBJECT < .HEADERTITLE
	}

This produces the same result as the example above, but it is even more readable. This also is the reason why we will use this "short notation" when we now copy level 1 of our menu to level 2.

So now let us come back to our template record. Here again is our current TypoScript, reduced to the part, which is important now. (You will again find the complete TypoScript for this subpart at the end of this section.) The copying takes place in the last line:

.. code-block:: typoscript

	SUBNAV = HMENU
	SUBNAV {

		# Definition for pages on level 1
		1 = TMENU
		1 {
			NO = 1

			ACT = 1
		}

		# Definition for pages on level 2
		# Copy the definitions from level 1
		2 < .1
	}

The line "2 < .1" is all it takes to create a complete copy of all the definitions, which we set up for the pages on level 1. With these few signs we have copied all the definitions, which we have in SUBNAV.1 to SUBNAV.2. Easy, isn't it? The only thing you must be aware of is the dot in front of the copied object. Remember that it means that you point to an object on the same level. And do not forget it!

Now when we have a look at our HTML template again we see that there is one small difference in the output of the pages on level 2 compared to the output of the pages on level 1: The wrap at the ul tag (that is the wrap for the whole page level) is different. While the ul tag had the CSS ID "submenu" attached on level 1, our HTML template shows us that there does not belong a CSS ID on level 2. So let's overwrite the wrap for level 2. We can do so after we copied the whole object to SUBNAV.2 by defining another value for SUBNAV.2.wrap:

.. code-block:: typoscript

	SUBNAV = HMENU
	SUBNAV {

		# Definition for pages on level 2
		# Copy the definitions from level 1,
		# but use another wrap.
		2 < .1
		2.wrap = <ul>|</ul>

That's it! Our submenu now can display up to two levels of pages. This should be enough for most websites.

Again here is the whole TypoScript code of that subpart, slightly restructured and nicely indented:

.. code-block:: typoscript

	SUBNAV = HMENU
	SUBNAV {
		# Only display subpages of the page from the main
		# navigation, which is in the current rootline.
		# Default value of entryLevel is 0, which are the
		# pages on the first level.
		# We want to begin with those subpages on level 2.
		entryLevel = 1

		# Definition for pages on level 1
		1 = TMENU
		1 {
			wrap = <ul id="submenu">|</ul>
			# Always expand all subpages.
			expAll = 1

			# Definition per page
			# NO: default formatting
			NO = 1
			NO {
				# Each entry is wrapped by
				# <li> </li>
				wrapItemAndSub = <li>|</li>
			}

			# ACT: User is on this or below this page
			# Activate this state for this menu
			ACT = 1
			ACT {
				# Use another wrap
				wrapItemAndSub = <li id="active">|</li>
			}
		}

		# Definition for pages on level 2
		# Copy the definitions from level 1,
		# but use another wrap.
		2 < .1
		2.wrap = <ul>|</ul>
	}

Now we have defined the meta navigation, the top navigation and the sub navigation. So all menus in our site are configured now and should display links to the pages, which you have created inside the TYPO3 Backend. However, until now all pages only display the blind text, which comes from the HTML template. We will change this in the next sections.
