.. include:: ../../../../Includes.txt


.. _configure-date:

DATE mark
~~~~~~~~~

The DATE mark is located above the middle column of our website. It should display the current date.

So basically we only want to output a short string, like a text, but it should get its content dynamically.
This kind of magic is possible with the :ref:`stdWrap <t3tsref:stdwrap>` function.

Let us define DATE as a TEXT object:

.. code-block:: typoscript

	DATE = TEXT

Did you put this line into :code:`page.10.marks`? Remember that DATE is no subpart.

When you read the introduction to the :ref:`TEXT object in the TSref <t3tsref:cobj-text>`
carefully you will notice that the :code:`TEXT` object has :code:`stdWrap` properties
at "root level", i.e. you can apply them directly to the object.

Now the :ref:`stdWrap <t3tsref:stdwrap>` function has a property called :code:`data`,
which is of data type :ref:`getText <t3tsref:data-type-gettext>`. From this we can see
that this data type can call PHP's :code:`date()` function, using the same format options
(see http://php.net/manual/en/function.date.php).

We will use a :code:`d.m.Y` format. For those unfamiliar with PHP, this means having the
day on two digits (:code:`d`), the month on two digits too (:code:`m`) and the year
on four digits (:code:`Y`), each separated by dots.

So we add to our TypoScript:

.. code-block:: typoscript

	DATE = TEXT
	DATE.data = date : d.m.Y

As far as code is concerned, this is all we need for this mark. As usual here is the
full code with comments:

.. code-block:: typoscript

	////////////////////////////////////////////////////////////////////////////////////////////
	//
	// Mark DATE
	//
	////////////////////////////////////////////////////////////////////////////////////////////

	// Outputs the current date in the defined format
	DATE = TEXT
	DATE.stdWrap.data = date : d.m.Y

You may have the feeling that we keep jumping all over the TSref. This is true, but you should
not be worried. Most of the code is finally rather simple and you will remember those basics
quite quickly. However referring to the TSref is a daily routine for a TYPO3 CMS integrator.

.. note::

   By default pages are cached for 24 hours. So it may happen that a page gets cached on 31.12.2012.
   The DATE mark is then filled with "31.12.2012". But if someone requests that page early on 1.1.2013
   it will still state "31.12.2012". One way around this would be to use the
   :ref:`config.cache_clearAtMidnight <t3tsref:setup-config-cache-clearatmidnight>` property to have
   all caches flushed at midnight every day.
