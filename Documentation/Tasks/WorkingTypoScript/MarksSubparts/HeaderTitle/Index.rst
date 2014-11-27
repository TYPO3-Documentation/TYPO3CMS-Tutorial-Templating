.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../../Includes.txt


.. _configure_headertitle:

HEADERTITLE mark
~~~~~~~~~~~~~~~~

The mark HEADERTITLE should output something like a "site title".
It is the title of your whole website. So what we want to output
there basically are only some words of text. You already know
how that is working; you removed such a definition when we started with the TEMPLATE cObject.
There was a TEXT cObject, do you remember? This is how we can use a TEXT object to output our site title there:

.. code-block:: typoscript

	HEADERTITLE = TEXT
	HEADERTITLE.value = TYPO3

This is all it takes to put our header title in place. Btw this is the easiest way to output a string with a cObject.

Have you noted that we just have defined a mark (and no subpart)?
Check that you have put the definition into page.10.marks, not into page.10.subparts!
I have added some comments (all lines starting with "#") to the code so that it is easily understandable.
Remember that these comments don't do anything and could also be left out which would not change
the functionality of the TypoScript template. The code in that section should now look like this:

.. code-block:: typoscript

	######################################################
	#
	# Configuration of MARKS
	#
	######################################################

	# Define the marks inside the subpart DOCUMENT
	page.10.marks {

		##############################################
		#
		# Mark HEADERTITLE
		#
		##############################################

		# The mark HEADERTITLE outputs the site title
		HEADERTITLE = TEXT
		HEADERTITLE.value = TYPO3

	}

In the next sections the code in this manual (like the part directly above)
will no longer show a big comment above showing into which property you have to put a definition,
because now you know where they belong. By the way: The order in which you define
the marks and the subparts inside page.10.marks and page.10.subparts basically does not matter.
(This is only different in a few cases: You can for instance create a copy of an object
using the "<" operator. If you defined "DATE < page.10.marks.HEADERTITLE" below the definition of
HEADERTITLE which we added above, you got the same output, which you get for the mark HEADERTITLE,
also for the mark DATE. When you create a copy, the definition which you want to copy
must be noted above the one in which you create the copy.
However, we do not create copies of our own TypoScript code in this tutorial,
so that we do not have to care about in which order we define our subparts or marks inside the respective properties.)
