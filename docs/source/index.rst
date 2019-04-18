.. Popet documentation master file, created by
   sphinx-quickstart on Sun Feb 24 01:43:54 2019.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

The Useless Easy Tool to Handle Pope's Data
===========================================
|image1| |image2|

.. |image1| image:: https://img.shields.io/pypi/v/popet.svg
   :target: https://pypi.org/project/popet/
.. |image2| image:: https://img.shields.io/pypi/l/popet.svg
   :target: https://pypi.org/project/popet/

Powered by `Yamato Nagata <https://twitter.com/514YJ>`_

Data by `Tako <https://twitter.com/TLE_Maker>`_

`GitHub <https://github.com/delta114514/Popet>`_

`ReadTheDocs <https://japanera.readthedocs.io/en/latest/>`_


.. code:: python

   from datetime import date

   from popet import Popet

   pope = Popet.who(date(1970, 5, 1))

   print(pope)
       # <Pope: Servant of God Paul VI, 21/06/1963-06/08/1978>
   print(vars(pope))
       # {'start': datetime.date(1963, 6, 21), 'end': datetime.date(1978, 8, 6), 'english_name': 'Servant of God Paul VI', 'regnal_name': 'PAULUS Sextus', 'personal_name': 'Giovanni Battista Enrico Antonio Maria Montini'}

Instllation
===========

Install with pip

.. code::

   $ pip install popet

How to Use
==========

You can use :code:`Popet`, :code:`Pope` (Awful naming).

.. code:: python

   from datetime import date

   from popet import Popet, Pope

   pope = Popet.who(date(1970, 5, 1))

   popes_who_has_god_in_english_name = \
       Popet.pope_match("god", cmp=lambda pope, value: value in pope.english_name.lower())

   print(popes_who_has_god_in_english_name) #[<Pope: Servant of God Paul VI, 21/06/1963-06/08/1978>, <Pope: Servant of God John Paul I, 26/08/1978-28/09/1978>]

   print(pope)                     # <Pope: Servant of God Paul VI, 21/06/1963-06/08/1978>
   print(pope.english_name)        # Servant of God Paul VI
   print(pope.personal_name)       # Giovanni Battista Enrico Antonio Maria Montini
   print(pope.regnal_name)         # PAULUS Sextus
   print(pope.start)               # 1963-06-21
   print(pope.end)                 # 1978-08-06
   print(pope.in_inauguration(date(1964, 1, 1))) # True

Documentation
=============

`Popet`
=======
vars
----
- :code:`popes` - :code:`list`: stores all :code:`Popet.pope`

methods
---------
- :code:`Popet.who(dt)`
- :code:`Popet.pope_match(value, key=lambda pope: pope, cmp=lambda pope, value: pope.in_inauguration(value), error="warn")`

`Popet.who(dt)`
---------------
- :code:`dt`: instance of :code:`datetime.date` or :code:`datetime.datetime`. Return first pope which return :code:`Pope.in_inaugration(dt)`


`Popet.pope_match(value, key=lambda pope: pope, cmp=lambda pope, value: pope.in_inauguration(value), error="warn")`
-------------------------------------------------------------------------------------------------------------------------
- :code:`value`: any
- :code:`key`: callable with one argument
- :code:`cmp`: callable with two arguments
- :code:`error` - :code:`str`: setting of how to handle errors.

Return all :code:`popet.Pope` objects stored in :code:`cls.popes` which :code:`cmp(key(Pope), value)` is :code:`True`.
if :code:`key` is not provided, :code:`key` is :code:`lambda pope: pope`
if :code:`cmp` is not provided, :code:`cmp` is :code:`lambda pope, value: pope.in_inauguration(value)`

`error` sets error level

- :code:`"ignore"`: ignore all errors occurred while running compare
- :code:`"warn"`: just warn error - default
- :code:`"raise"`: raise any errors

Default, this will return all :code:`Pope` which in inauguration at given :code:`value`(which must be :code:`datetime.date`).

`Pope`
======
vars
----
- :code:`start` - :code:`datetime.date`: The date The pope inaugurated
- :code:`end` - :code:`datetime.date`: The date The pope left his position
- :code:`english_name` - :code:`str`: His English name
- :code:`regnal_name` - :code:`str`: His Regnal name in latin
- :code:`personal_name` - :code:`str`: His Personal name

`Pope.in_inauguration(dt)`
--------------------------

- :code:`dt`: instance of :code:`datetime.date` or :code:`datetime.datetime`.

Return if he is in inauguration at :code:`dt`.

`Pope` will be return :code:`True` if :code:`dt` is in between :code:`Pope.start` (from very first of the day) and :code:`Pope.end` (until very end of the day).


In End
======
Sorry for my poor English, And that I made useless library.
I want **you** to join us and send many pull requests about Doc, code, features and more!!
