Welcome to django-composite-field's documentation!
==================================================

django-composite-field provides a :class:`CompositeField` that
encapsulates multiple fields and allows you to treat them as one.

``CompositeField``
------------------

.. class:: CompositeField(fields, [**options])

A :class:`CompositeField` acts as a proxy for one or more other
fields. It behaves like a single field, and can be used as a primary
key. Composite keys in Django, hooray!

.. attribute:: CompositeField.fields

    A tuple or list of fields to be included in the composite field.
    Fields will be used in the order they're specified.

Unpacking
~~~~~~~~~

:class:`CompositeField` can be unpacked. Say you have a model with
these fields::

    class Thing(models.Model):
        first = models.CharField(max_length=32)
        second = models.IntegerField()
        both = CompositeField(('first', 'second'))

You can then unpack the :class:`CompositeField` like so::

    >>> thing = Thing(first='newt', second=42)
    >>> first, second = thing.both

    # The values of the individual fields have been unpacked.
    >>> first
    'newt'
    >>> second
    42

String Representation
~~~~~~~~~~~~~~~~~~~~~

When converted to a string, a :class:`CompositeField` becomes a
comma-separated, ordered list of its values::

    >>> str(thing.both)
    'newt,42'

Using as a Primary Key
~~~~~~~~~~~~~~~~~~~~~~

:class:`CompositeField` can be used as a primary key::

    >>> thing.both.primary_key = True
    >>> thing.pk
    'newt,42'

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
