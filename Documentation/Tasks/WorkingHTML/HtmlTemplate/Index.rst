.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


.. _shortinformation:

A quick explanation on marks and subparts
*****************************************

This section explains what marks and subparts are, what they look like and what they are used for.
Both marks and subparts refere to a concept called "markers".
A marker is a word  wrapped in three hash tags (###) on either side.

Examples:

.. code-block:: text

	###TITLE###
	###METANAV###
	###DOCUMENT###

All of the above are valid markers. There's more on
:ref:`naming makers <shortinformation-naming>` later.

.. _shortinformation-marks:

Marks
~~~~~

A mark is a single marker placed in your HTML template.
Example:

.. code-block:: html

	<h1>###TITLE###</h1>

When the template is interpreted by TYPO3 CMS, the mark
(i.e. :code:`###TITLE###`) is replaced with what you configured TYPO3 CMS to put there.
Everything around the mark (above and below) remains untouched.

.. important::

   Marks may not be placed inside HTML comment tags. In such a case they do not get replaced.
   So the following is **wrong**:

   .. code-block:: html

   		<!--###TITLE###-->


.. _shortinformation-subparts:

Subparts
~~~~~~~~

Subparts use the same syntax, but use **pairs of markers**, with possibly some HTML code
in between.

Example:

.. code-block:: html

	###METANAV###
	<p>
		This is HTML code.
		It will be replaced by TYPO3, when we configure the subpart "METANAV".
	</p>
	###METANAV###

The subpart consists of both markers and everything in between.
When the template is interpreted by TYPO3 CMS the whole subpart
is replaced by whatever was configured to be placed there.
Everything around the subpart (above and below) remains untouched.

Contrary to marks, the subpart markers may be placed inside HTML comment tags.
That way they do not show up, when you open your template file in the browser,
but still do their work with TYPO3 CMS. Additional information may be placed
inside the comment tag. It is a current practice to indicate the beginning
and the end of the subpart by using the words "Start" and "End" in the opening
and closing markers respectively.

Example:

.. code-block:: html

	<!-- ###METANAV### Start -->
	<p>
		This is HTML code.
		It will be replaced by TYPO3, when we configure the subpart "METANAV".
	</p>
	<!-- ###METANAV### End -->


.. _shortinformation-naming:

Naming markers
~~~~~~~~~~~~~~

A question that often arises on marks and subparts is how to name them.
Just use any name that you see fit, TYPO3 CMS will know how to replace them
(more on this up ahead). There is going to be correspondance between the names
used in the markers and TYPO3 CMS configuration.

Marks and subparts have nothing to do with IDs or classes, which some HTML tags have,
or with CSS styles, which are associated with these IDs or classes.
However, you can use names for marks and subparts, which somehow fit the IDs or classes,
so that it is easier for you to remember the roles of the various marks and subparts.

In general create relevant, meaningful and short marker names in your templates.

.. important::

   The only rule is that the marker names must be single words
   with no space inside them. The following are **not** valid markers:

   .. code-block:: text

		###MAIN CONTENT###
		###SECONDARY HEADER###
