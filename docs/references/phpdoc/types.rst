型の定義
======================

Many tags use a :term:`Type` as part of their definition (such as the @return tag).
These types differ from the official PHP definition to be able to represent all
kinds of data.

多くのタグは定義に :term:`Type` を含みます (たとえば @return タグ)。
これらの型はあらゆる種類のデータを表現でき、PHP公式の定義とは異なります。

A complete definition will be given of these types and what they represent in 
the following sections.

これらの型の完全な定義と、型が何を表すかを次章で示します。

ABNF
----

::

    type-expression          = 1*(array-of-type-expression|array-of-type|type ["|"])
    array-of-type-expression = "(" type-expression ")[]"
    array-of-type            = type "[]"
    type                     = class-name|keyword
    class-name               = 1*CHAR
    keyword                  = "string"|"integer"|"int"|"boolean"|"bool"|"float"
                               |"double"|"object"|"mixed"|"array"|"resource"
                               |"void"|"null"|"callable"|"false"|"true"|"self"

When a :term:`Type` is used the user will expect a value, or set of values, as
detailed below.

:term:`Type` が使用される場合、以下に詳しく述べる値もしくは値の集合を期待します。

単一型 / Atomic (singular) type
-------------------------------

The supported atomic types are either a *valid class name* or *keyword*.

サポートされる単一型は *有効なクラス名* または *キーワード* です。

有効なクラス名 / Valid Class Name
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A valid class name seen from the context where this type is mentioned. Thus
this may be either a Fully Qualified Class Name (FQCN) or if present in a
namespace a local name.

この型が言及される文脈から見て有効なクラス名です。
これはおそらく完全修飾クラス名(FQCN)または名前空間内でのローカルな名前です。

The element to which this type applies is either an instance of this class
or an instance of a class that is a (sub-)child to the given class.

この型が適用される要素は、そのクラスのインスタンスと子クラス(孫クラス)のインスタンスです。

例:

.. code-block:: php
   :linenos:

    @param \My\Namespace\Class
    @return Exception

キーワード / Keyword
~~~~~~~~~~~~~~~~~~~~

A keyword defining the purpose of this type. Not every element is determined
by a class but still worth of a classification to assist the developer in
understanding the code covered by the :term:`PHPDoc`.

「キーワード」は型の目的を定義します。全ての要素がクラスによって決定されるわけではなく、開発者がコードを理解することの助けになるよう :term:`PHPDoc` によって分類されます。

.. NOTE::

    Most of these keywords are allowed as class names in PHP and as
    such are hard to distinguish from real classes. As such the keywords MUST
    be lowercase, as most class names start with an uppercase first character,
    and you SHOULD NOT use classes with these names in your code.

    キーワードのほとんどはPHPのクラス名として許容され、本物のクラスと区別することは難しいです。
    キーワードは小文字で記述する必要があり、ほとんどのクラスは先頭が大文字です。
    あなたのコードでこれらの名前をクラス名として使用すべきではありません。

    There are more reasons to not name classes with the names of these
    keywords but that falls beyond the scope of this specification.

    これらの名前をクラス名として使ってはいけない理由はいくつもありますが、この仕様の範疇を超えます。

The following keywords are recognized:

以下のようなキーワードが認識されます：

1.  **string**, the element to which this type applies is a string of
    binary characters.

    この型が適用される要素はバイナリ文字の文字列です。

2.  **integer** or **int**, the element to which this type applies is a whole
    number or integer.

    この型が適用される要素は整数です。

3.  **boolean** or **bool**, the element to which this type applies only has
    state true or false.

    この型が適用される要素は true または false です。

4.  **float** or **double**, the element to which this type applies is a
    continuous, or real, number.

    この型が適用される要素は連続量または実数です。

5.  **object**, the element to which this type applies is the instance of an
    undetermined class.

    この型が適用される要素はクラスを特定しないインスタンスです。

6.  **mixed**, the element to which this type applies can be of any type as
    specified here. It is not known on compile time which type will be used.

    この型が適用される要素は任意の型の値です。それはコンパイル時に型が使用されません。

7.  **array**, the element to which this type applies is an array of values,
    see the section on `Arrays`_ for more details.

    この型が適用される要素は値の配列で、詳しくは `Arrays`_ の節をお読みください。

8.  **resource**, the element to which this type applies is a resource per
    the definition of PHP at
    http://www.php.net/manual/en/language.types.resource.php.

    この型が適用される要素はリソース値で、それぞれの定義は http://www.php.net/manual/language.types.resource.php にあります。

9.  **void**, this type is commonly only used when defining the return type of a
    method or function.
    The basic definition is that the element indicated with this type does not
    contain a value and the user should not rely on any retrieved value.

    この型は函数またはメソッドの返り値の定義にのみ利用されます。
    基本的な定義としてはこの要素は値を含まず、ユーザーは返り値に依存してはいけないことを意味します。

    例：

    .. code-block:: php
       :linenos:

        /**
         * @return void
         */
        function outputHello()
        {
            echo 'Hello world';
        }

    In the example above no return statement is specified and thus is the return
    value not determined.

    この例ではreturn文がなく、返り値が決定されません。

    例 2：

    .. code-block:: php
       :linenos:

        /**
         * @param boolean $quiet trueなら 'Hello world' がechoされる
         *
         * @return void
         */
        function outputHello($quiet)
        {
            if ($quiet} {
                return;
            }
            echo 'Hello world';
        }

    In this example the function contains a return statement without a given
    value. Because there is no actual value specified does this also constitute
    as type 'void'.

    この例の函数にはreturn文がありますが、値がないため‘void’型になります。

10. **null**, the element to which this type applies is a NULL value or, in
    technical terms, does not exist.

    この型が適用される値は NULL で、これは技術用語で「存在しない」ことです。

    A big difference compared to void is that this type is used in any situation
    where the described element may at any given time contain an explicit NULL
    value.

    明示的に NULL 値を含む可能性のある状況で使用されることが void との大きな差異です。

    例：

    .. code-block:: php
       :linenos:

        /**
         * @return null
         */
        function foo()
        {
            echo 'Hello world';
            return null;
        }

    This type is commonly used in conjunction with another type to indicate that
    it is possible that nothing may be returned.

    この型は一般に別の型に関連して、何の値も返されない可能性がある場合に使用されます。

    例：

    .. code-block:: php
       :linenos:

        /**
         * @param boolean $create_new trueのとき stdClass のインスタンスが返される
         *
         * @return stdClass|null
         */
        function foo($create_new)
        {
            if ($create_new) {
                return new stdClass();
            }

            return null;
        }


11. **callable**, the element to which this type applies is a pointer to a
    function call. This may be any type of callback as defined in the PHP manual
    at http://php.net/manual/en/language.pseudo-types.php.

    この型が適用されるのは函数呼び出しへのポインタです。
    PHPマニュアル http://php.net/manual/language.pseudo-types.php で定義される、callbackのどのようなタイプでも良いです。

12. **false** or **true**, the element to which this type applies will have
    the value true or false. No other value will be returned from this
    element.

    この型が適用される要素はtrueまたはfalse値です。この要素からほかの値は返されません。

        This type is commonly used in conjunction with another type to indicate
        that it is possible that true or false may be returned instead of an
        instance of the other type.

        この型は一般に別の型に関連して、true/falseと別の型のインスタンスが返される可能性がある場合に使用されます。


13. **self**, the element to which this type applies is of the same Class,
    or any of its children, as which the documented element is originally
    contained.

    この型が適用される要素は同じクラス及び子クラスで、文書化された要素そのものが含まれます。

    例：

        Method C() is contained in class A. The DocBlock states
        that its return value is of type `self`. As such method C()
        returns an instance of class A.

        クラス A に含まれるメソッド C() のDocブロックが戻り値 `self` を返すと記述されるなら、メソッド C()はクラス A のインスタンスを返します。

    This may lead to confusing situations when inheritance is involved.

    継承する際、これは混乱を引き起すかもしれません。

    例 (前の状況が継続されます)：

        Class B extends Class A and does not redefine method C(). As such
        it is possible to invoke method C() from class B.

        クラス B がクラス A を継承しメソッド C() は再定義されません。
        そのとき、クラス B からメソッド C() を呼び出すことができます。

    In this situation ambiguity may arise as `self` could be interpreted as
    either class A or B. In these cases `self` MUST be interpreted as being
    an instance of the Class where the DocBlock containing the `self` type
    is written or any of its child classes.

    このように `self` がクラス A と B のどちらとも解釈できる曖昧な状況が生じます。
    この場合において `self` は必ず `self` 型が記述されたクラスまたは子クラスのどれかのインスタンスであるように解釈しなければいけません(MUST)。

    In the examples above `self` MUST always refer to class A or B, since
    it is defined with method C() in class A.

    この例では C() は A で定義されるので、要素 `self` は常にクラス A または B を参照しなければいけません(MUST)。

    If method C() was to be redefined in class B, including the type
    definition in the DocBlock, then `self` would refer to class B or any
    of its children.

    もしメソッド C() がクラス B で再定義されDocブロックに型定義を含むなら、 `self` はクラス B または子クラスのどれかを参照します。

複合型 / Multiple types
-----------------------

When the :term:`Type` consists of multiple (sub-)types then these MUST be
separated with the vertical bar sign (|).

:term:`Type` が複数の型からなるとき、必ず複数の(派生)型を縦棒/vertical bar sign `|` で区切って書かなければいけません(MUST)。

例：

.. code-block:: php
   :linenos:

    @return int|null

配列 / Arrays
-------------

The value represented by :term:`Type` can be an array. The type MUST be defined
following the format of one of the following options:

:term:`Type` で表現される値は配列にすることができます。この型は以下の形式のどれかで記述しなければいけません(MUST)。

1. **unspecified**, no definition of the contents of the represented array is given.

   **指定しない**。内容について定義しないときはarrayを記述します。

   例： ``@return array``

2. **specified containing a single type**, the :term:`Type` definition informs
   the reader of the type of each array element. Only one :term:`Type` is then
   expected as element for a given array.

   **内容の単一型を指定**。この型定義は配列に含まれる要素の型を表します。この配列にはひとつの :term:`Type` だけが含まれることが期待されます。

   例: ``@return int[]``

   Please note that *mixed* is also a single type and with this keyword it is
   possible to indicate that each array element contains any possible type.

   *mixed* は単一型であり、このキーワードは配列の要素にあらゆる型を含むことを示すことに注意してください。

3. **specified containing multiple types**, the Type definition informs the reader
   of the type of each array element. Each element can be of any of the given
   types.

   **内容の複合型を指定**。この型定義は配列に含まれる要素の型を表します。この配列は各要素に指定された型のどれかを含みます。

   例: ``@return (int|string)[]``

   .. NOTE::

       many IDEs probably do not support this notation yet.

       多くのIDEは、おそらくまだこの表記をサポートしません。
