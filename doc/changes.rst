Change History
**************

2.1
=====

Methods now give their name when stringified.

Java: use a cache for Java implemented methods as
class.getDeclaredMethods can be very slow on some platforms.

2.0
===

There is now a compatible Objective C solution that works on iOS and Mac

Enhanced :doc:`jmp-compile` to evaluate constants in the source (eg
``3+4`` is replaced with ``7``, and ``True or 7`` is replaced with
``True``).  It will also omit unreachable code (eg ``if False``).  You
can turn this optimisation off with :option:`--no-optimizations`.  You
can also supply your own constants such as ``DEBUG=True`` or
``VERSION="2.3"``.  The resulting bytecode still works correctly even
against |project| version 1.0.

:doc:`jmp-compile` detects trying to assign to builtin constants
(eg ``True=0``)

:doc:`jmp-compile` now understands list comprehensions.  The resulting
bytecode still works correctly even against |project| version 1.0.

Added toPyReprString for Java

``bool`` now always returns a value.  Before it would give TypeError
for unknown types, which now give ``True``.

Correct Java string.split for various corner cases.

Made Java implemented methods work correctly as dictionary keys.

Calling a Java non-varargs method with an incorrect number of
args now gives the correct exception type (``TypeError``)

Deal with -2147483648 / -1 (gives -2147483648 because + 2147483648
would be an overflow).  On Intel processors this operation would cause
a `hardware fault <http://kqueue.org/blog/2012/12/31/idiv-dos/>`__
like dividing by zero does, so similar precautions are taken.  Note
that |project| only uses 32 bit signed integers.

Fix global lookup for LOAD_NAME (:issue:`14`)

1.2
===

Filled in the :jdoc:`cause <java/lang/Throwable.html#getCause()>` for
:ref:`ExecutionError <ExecutionError>` and added toDetailedString()
method.

Added several annotations that help when the file is compiled with
very strict warnings.

Minor documentation tweaks and updates.

Added toDetailedString() on the Exception which provides additional
useful detail for logging and analytics.

1.1
===

All Java non-public items marked private to avoid them showing up in
completions if you copied the code to your own package.  (:issue:`1`)

Do not use `String.isEmpty()` as it doesn't exist on Android (:issue:`2`)

Public entry points are synchronized to prevent concurrent usage (:issue:`3`)

Added `dict.get(key, default)` (:issue:`5`)

Dictionary members can be obtained and set via attribute style access
too (:issue:`6`)::

   a={"foo": 3}
   # Get
   print a["foo"], a.foo
   # Set
   a.bar=7
   print a["bar"], a.bar

Added *is/is not* operator.  Behind the scenes this translates *x is
y* into *id(x) == id(y)*.

It is possible to do a form of object orientation keeping data and the
functions that operate on it together in the same dictionary as
:ref:`documented here <pyobject>` (:issue:`7`)

Code that attempted to do a rich compare of dictionaries was removed
and their :func:`id` is used instead.  (:ref:`comparisons`).

Added dict.copy (:issue:`8`)

Added :doc:`jmp-compile` option to only do a syntax check

Fixed returns within for loops (:issue:`10`)
