=================================================
POMM: The PHP Object Model Manager for Postgresql
=================================================

**Important** 

This is the DEVEL branch of Pomm. If you want to use the stable version, please use the 1.0 branch for now. 

What is Pomm ?
**************
**Pomm** is a *lightweight*, *fast*, *efficient* and *powerful* PHP object manager for the Postgresql relational database. **Pomm is not an ORM**, it is more like an object hydrator above PDO implementing the `identity map <http://en.wikipedia.org/wiki/Identity_map>`_ design pattern and proposing convenient functionalities. Dropping the abstraction layer makes programmers able to take advantage of most of Postgresql's awesome features.

Pomm works with PHP 5.3 and Postgresql 8.4 and above.

You can reach

* `documentation <http://pomm.coolkeums.org/documentation/manual>`_
* `code examples <http://pomm.coolkeums.org/documentation/examples>`_
* `A gentle introduction to Pomm <http://www.coolkeums.org/en/article/a-gentle-introduction-to-pomm.html>`_
* `Pomm: a concerto for PHP and Postgresql <http://www.coolkeums.org/en/article/pomm-a-concerto-for-php-and-postgresql.html>`_

What does Pomm propose ?
************************

* Database introspection and model generation
* Lazy hydration and on the fly type conversion
* SQL queries, virtual fields, finders and pagers
* Collection, filters and query filters
* A Where clause builder
* Security and debuging tools

Database introspection and model generation
*******************************************
Once you have designed your database using your favorite tool, Pomm can generate PHP model classes for you by inspecting `tables <http://www.postgresql.org/docs/8.4/static/sql-createtable.html>`_ and `views <http://www.postgresql.org/docs/8.4/static/sql-createview.html>`_. It checks the `schema <http://www.postgresql.org/docs/8.4/static/ddl-schemas.html>`_ where your database objects are stored so generated classes use according `PHP namespaces <http://www.php.net/manual/en/language.namespaces.php>`_, there will not be naming collision anymore ! Of Course, Postgresql's `table inheritance <http://www.postgresql.org/docs/8.4/static/ddl-inherit.html>`_ is supported.

Lazy hydration and on the fly type conversion
*********************************************
`Queries <http://pomm.coolkeums.org/documentation/manual#custom-queries>`_ return `collections <http://pomm.coolkeums.org/documentation/manual#collections>`_ which are scrollable iterators on results. Fetched objects are hydrated on demand for minimal memory consumption and data are `converted <http://pomm.coolkeums.org/documentation/manual#database-and-converters>`_ from/to Postgresql. Boolean in Pg are boolean in PHP, `arrays <http://www.postgresql.org/docs/8.4/static/arrays.html>`_ in Pg are arrays in PHP, `geometric types <http://www.postgresql.org/docs/8.4/static/datatype-geometric.html>`_ are converted into geometric PHP objects. Of course this is extendible and custom database types can be converted into custom PHP classes. Almost all standard and geometric types are supported plus `period <http://temporal.projects.postgresql.org/reference.html>`_, `HStore <http://www.postgresql.org/docs/8.4/static/hstore.html>`_ and `ltree <http://www.postgresql.org/docs/8.4/static/ltree.html>`_ extensions.

SQL queries, virtual fields, finders and pagers
***********************************************
Of course 80% of the queries of a web applications are like ``SELECT * FROM my_table WHERE ...``  So there is a method for that. You can configure what you do want in the select fields in case you would like to add your classes extra properties. You can even use them with the converter system with extra fields adding them as virtual fields. For the more complicated queries, SQL is the way to go. You can use all the awesome `operators <http://www.postgresql.org/docs/8.4/static/functions.html>`_, `full text search <http://www.postgresql.org/docs/8.4/static/textsearch.html>`_, `window functions <http://www.postgresql.org/docs/8.4/static/tutorial-window.html>`_, `CTEs and recursive queries <http://www.postgresql.org/docs/8.4/static/queries-with.html>`_, (add your preferred feature here).

Collection filters and query filters
************************************
When retrieving data from the database trough a ``Collection`` object, it is possible to register PHP anonymous functions as filters before objects are hydrated. This is very powerful as you can create foreign objects or code you own filters.

Queries are also made in a Filter Chain design pattern. You can add your own filters to place code before and/or after each query.

A Where clause builder
**********************
Sometimes, you want to create a ``WHERE`` clause dynamically. Pomm proposes a Where class to let you ``AND`` and/or ``OR`` your conditions passing the values as argument each time for escaping. There is even a ``WhereIn`` method with an array of values as parameter.

Security and debuging tools
***************************
All queries are prepared, the values you give as argument are automatically escaped by the server. Furthermore, the converter system ensures there is no type enforcing.

To be sure everything is fine, you can register the ``LoggerFilter`` to your connection so you will keep track of every query with statistics like the time it took, the number of results returned etc.


=====================
How to install Pomm ?
=====================

The easy way: composer
**********************
Using `composer <http://packagist.org/>`_ installer and autoloader is probably the easiest way to install Pomm and get it running. What you need is just a ``composer.json`` file in the root directory of your project:


::

  {
  "require": {
      "pomm/pomm": "master-dev"
    }
  } 

Invoking ``composer.phar`` will automagically download Pomm, install it in a ``vendor`` directory and set up the according autoloader. Check out `this tutorial <http://www.coolkeums.org/en/article/a-gentle-introduction-to-pomm.html>`_  for step by step explanation.

Using Pomm with a PHP framework
*******************************

* Silex `PommServiceProvider <https://github.com/chanmix51/PommServiceProvider>`_
* Symfony2 `PommBundle <https://github.com/chanmix51/PommBundle>`_

===========================
How to contribute to Pomm ?
===========================

That's very easy with github:

* Send feedback to `@chanmix51 <https://twitter.com/#!/chanmix51>`_ on twitter or by mail at <hubert DOT greg AT gmail DOT com>
* Report bugs (very appreciated)
* Fork and PR (very very appreciated)
* Send vacuum tubes to the author (actual preferred are russian 6Φ12Π)
