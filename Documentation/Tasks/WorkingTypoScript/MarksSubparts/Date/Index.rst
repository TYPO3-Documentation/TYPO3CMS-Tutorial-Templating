.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../../Includes.txt


.. _configure-date:

DATE mark
~~~~~~~~~

The mark DATE is displayed above the middle column of our website. It should display the current date.

So basically we only want to output a short string, like a text, but it should get its content dynamically. This kind of magic is possible with the function stdWrap. stdWrap is available for many properties and also for some objects.

Let us define DATE as a TEXT object:

.. code-block:: typoscript

	DATE = TEXT

Did you put this line into page.10.marks? Remember that DATE is no subpart.

When you read the introduction of the cObject TEXT in TSref carefully you will notice that the TEXT object has a property called "stdWrap", in which stdWrap properties are available.

When we have a look at the function stdWrap in TSref you will see that there is a property called "data", which has the data type TSref/getText|getText. Looking at the "Data types reference" you will see that using getText it is possible to get several information from somewhere in PHP. One of this information is the current date (see the example!). TSref shows us that in that case the syntax of our value is something like "date : d-m-y". The part "date :" must not be changed. The part behind is used for the date format, which we want to get. For the possible values you can have a look at the PHP manual on the date function: http://php.net/manual/en/function.date.php

We will use: Day with two digits, then a dot, then month with two digits, then another dot and finally the year with four digits. So the format of our date string must look like this: :code:`d.m.Y`.

So we add to our TypoScript:

.. code-block:: typoscript

	DATE = TEXT
	DATE.stdWrap.data = date : d.m.Y

Codewise this is the complete setup code, which we need for this mark. As usual I print it here with comments again:

.. code-block:: typoscript

	##############################################
	#
	# Mark DATE
	#
	##############################################

	# Outputs the current date in the defined format
	DATE = TEXT
	DATE.stdWrap.data = date : d.m.Y

With this mark you could again see how much you sometimes have to jump from chapter to chapter when you read TSref.
But don't be worried: The syntax of the resulting TypoScript code mostly is - like in our case - rather simple.

.. note::

   Usually, the pages are cached for 24 hours. So it will happen, that a page gets cached at 31.12.2012.
   The date is filled then with 31.12.2012. But if someone request that page early at 1.1.2013
   it will still state 31.12.2012. If you configure config.cache_clearAtMidnight
   the cache will be cleared at midnight and you have allways the correct date.
