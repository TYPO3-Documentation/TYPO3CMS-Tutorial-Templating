.. include:: ../../../../Includes.txt


.. _configure_headertitle:

HEADERTITLE mark
~~~~~~~~~~~~~~~~

The mark HEADERTITLE should output something like a "site title".
It is the title of your whole website. So what we want to output
there basically are only a few words of text. You already know
how that is working; you removed such a definition when we started
with the :code:`TEMPLATE` object. There was a :code:`TEXT` object,
do you remember? This is how we can use a :code:`TEXT` object
to output our site title there:

.. code-block:: typoscript

	HEADERTITLE = TEXT
	HEADERTITLE.value = TYPO3

This is all it takes to put our header title in place.
By the way, this is the easiest way to output a string with a
content object.

Have you noted that we just have defined a mark (and not a subpart)?
Check that you have put the definition into :code:`page.10.marks`,
not into :code:`page.10.subparts`!

Here is the same code within the context of comments, so that
you can see more clearly where it belongs:

.. code-block:: typoscript

	////////////////////////////////////////////////////////////////////////////////////////////////////////////
	//
	// Configuration of MARKS
	//
	////////////////////////////////////////////////////////////////////////////////////////////////////////////

	# Define the marks inside the subpart DOCUMENT
	page.10.marks {

		////////////////////////////////////////////////////////////////////////////////////////////
		//
		// Mark HEADERTITLE
		//
		////////////////////////////////////////////////////////////////////////////////////////////

		# The mark HEADERTITLE outputs the site title
		HEADERTITLE = TEXT
		HEADERTITLE.value = TYPO3

	}

.. note::

   By the way, the order in which you define the marks and the subparts inside
   :code:`page.10.marks` and :code:`page.10.subparts` basically does not matter,
   except if you use copies of objects. The original object must be defined
   before it is copied.
