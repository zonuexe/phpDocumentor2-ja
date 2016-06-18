@var
====

You may use the @var tag to document the "Type" of properties, sometimes called class variables.

プロパティ(クラス変数とも呼ばれる)の型を記述することができます。

構文
------

    @var ["Type"] [$element_name] [<description>]

説明
-----------

The @var tag defines which type of data is represented by the value of a property_.

@var タグは プロパティ_ の値のデータ型を定義します。

The @var tag MUST contain the name of the element it documents. An exception to this is when property declarations only
refer to a single property. In this case the name of the property MAY be omitted.

@var タグは必ず文書化する要素名を含まねばなりません(MUST)。
そのひとつの例外は、プロパティ宣言でひとつのプロパティに言及するときのみです。
この場合、プロパティの名前を省略することもできます(MAY)。

This is used when compound statements are used to define a series of properties. Such a compound statement can only have
one DocBlock while several items are represented.

これは複合文でプロパティがまとめて定義されるときに使用されます。複合文でいくつかのプロパティが表現されるとき、Docブロックをひとつだけ持つことができます。

例
--------

.. code-block:: php

    class Foo
    {
      /** @var string|null Should contain a description */
      protected $description = null;
    }

.. code-block:: php

    class Foo
    {
      /** @var string|null ここに説明を書きます */
      protected $description = null;
    }

複合文は以下のように文書化することができます。

.. code-block:: php

    class Foo
    {
      /**
       * @var string $name        ここに説明を書きます
       * @var string $description ここに説明を書きます
       */
      protected $name, $description;
    }

.. _property: http://www.php.net/manual/en/language.oop5.properties.php
.. _プロパティ: http://php.net/manual/language.oop5.properties.php
