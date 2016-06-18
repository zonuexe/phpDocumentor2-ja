@return
=======

The @return tag is used to document the return value of functions or methods.

@return タグは函数またはメソッドの返り値を文書化するために利用します。

Syntax
------

    @return [:term:`Type`] [<description>]

Description
-----------

With the @return tag it is possible to document the return type and function of a
function or method. When provided it MUST contain a :term:`Type` to indicate
what is returned; the description on the other hand is OPTIONAL yet
RECOMMENDED in case of complicated return structures, such as associative arrays.

@return タグでは函数またはメソッドの返り値と機能を文書化することができます。

The @return tag MAY have a multi-line description and does not need explicit
delimiting.

@return タグは複数行の説明を持つことができ、明示的な区切りを必要としません。

It is RECOMMENDED when documenting to use this tag with every function and
method. Exceptions to this recommendation are:

それぞれの函数と機能ごとに @return タグで文書化することを推奨します(RECOMMENDED)。
ただし、以下の場合を除きます

1. **constructors**, the @return tag MAY be omitted here, in which case
   `@return self` is implied.

   **コンストラクタ** ： @return タグを書かなくてもよく(MAY)、暗黙的に `@return self`になります。
2. **functions and methods without a `return` value**, the @return tag MAY be
   omitted here, in which case `@return void` is implied.

   **函数またはメソッドに `return` する値がない** ： @return タグを書かなくてもよく(MAY)、暗黙的に `@return void` になります。

This tag MUST NOT occur more than once in a :term:`PHPDoc` and is limited to
:term:`Structural Elements` of type method or function.

このタグは複数回書いてはいけません(MUST NOT)。また、書くことができるのは :term:`構造要素` のうち、函数またはメソッドに限ります。

Effects in phpDocumentor
------------------------

:term:`Structural Elements` of type method or function, that are tagged with the
@return tag, will have an additional section *Returns* in their content description
that shows the return :term:`Type` and description.

If the return :term:`Type` is a class that is documented by phpDocumentor, then a link
to that class' documentation is provided.

例
--------

Singular type:

.. code-block:: php
   :linenos:

    /**
     * @return integer Indicates the number of items.
     */
    function count()
    {
        <...>
    }

Function can return either of two types:

.. code-block:: php
   :linenos:

    /**
     * @return string|null The label's text or null if none provided.
     */
    function getLabel()
    {
        <...>
    }
