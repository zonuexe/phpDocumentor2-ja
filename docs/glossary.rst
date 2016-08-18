用語集
========

.. glossary::

    Docコメント
    DocComment
    DocComments
        This is a special type of comment which starts with `/**`, ends with `*/` and may contain any number of lines
        in between. Every line should start with an asterisk, which is aligned with the first asterisk of the opening
        clause.

        Single line example:

        .. code-block:: php
           :linenos:

            /** <...> */

        Multiline example:

        .. code-block:: php
           :linenos:

            /**
             * <...>
             */

    Docブロック
    DocBlock
    DocBlocks
        This is a :term:`DocComment` containing a single :term:`PHPDoc` and represents the basic in-source
        representation.

        Example:

        .. code-block:: php
           :linenos:

            /**
             * Returns the name of this object.
             *
             * @return string
             */

    抽象構文木
    AST
    Abstract Syntax Tree
    Abstract Syntax Tree (AST)
        phpDocumentor generates a XML file between parsing your source code and generating the HTML output. This
        structure file (called *structure.xml*) contains the raw analyzed data of your project, also called: an Abstract
        Syntax Tree.

        This same file is also used by phpDocumentor to do incremental parsing of your project by comparing the contents
        of this file with the content on disk.

        It is thus recommended to keep your structure file and allow phpDocumentor to re-use the contained information.

    PHPDoc
        This is a section of documentation which provides information on several aspects of :term:`Structural Elements`.

        A :term:`PHPDoc` is usually enveloped in a :term:`DocComment`.

        Example:

        .. code-block:: php
           :linenos:

             Returns the name of this object.

             @return string

        Example enveloped in a :term:`DocComment`:

        .. code-block:: php
           :linenos:

            /**
             * Returns the name of this object.
             *
             * @return string
             */

    構造要素
    Structural Element
    Structural Elements
        This is a collection of Programming Constructs which SHOULD be preceded by a :term:`DocBlock`. The collection
        contains the following constructs:

        :term:`Docブロック` を前置すべき言語構造の総称です。次のようなものが挙げられます。

        * file
        * require(_once)
        * include(_once)
        * クラス / class
        * インターフェイス / interface
        * トレイト / trait
        * 函数 / function (メソッドを含む)
        * プロパティ / property
        * 定数 / constant

        It is RECOMMENDED to precede :term:`Structural Elements` with a :term:`DocBlock` at its definition and not with
        each individual usage.

        :term:`Docブロック` は個々の使用箇所ではなく、定義の :term:`構造要素` に記述することを推奨します(RECOMMENDED)。

        例：

        .. code-block:: php
           :linenos:

            /** @var int This is a counter. */
            $int = 0;

            // there should be no docblock here
            $int++;

        .. code-block:: php
           :linenos:

            /** @var int これはカウンターです。 */
            $int = 0;

            // ここにDocブロックは書けません
            $int++;

        または：

        .. code-block:: php
           :linenos:

            /**
             * This class acts as an example on where to position a DocBlock.
             */
            class Foo
            {
                /** @var string|null Should contain a description if available */
                protected $description = null;

                /**
                 * This method sets a description.
                 *
                 * @param string $description A text with a maximum of 80 characters.
                 *
                 * @return void
                 */
                public function setDescription($description)
                {
                    // there should be no docblock here
                    $this->description = $description;
                }
            }

        .. code-block:: php
           :linenos:

            /**
             * このクラスはDocブロックを書く場所の例です。
             */
            class Foo
            {
                /** @var string|null 有効なら説明文を持つべきです */
                protected $description = null;

                /**
                 * このメソッドには説明文が設定されます。
                 *
                 * @param string $description 最大80文字のテキストです。
                 *
                 * @return void
                 */
                public function setDescription($description)
                {
                    // ここにDocブロックは書けません
                    $this->description = $description;
                }
            }

        Another example is to document the variable in a foreach explicitly; many IDEs use this information to help you
        with auto-completion:

        以下の例では、foreachの中の変数を文書にします。多くのIDEは自動補完の補助としてこの情報を利用します。

        .. code-block:: php
           :linenos:

            /** @var \Sqlite3 $sqlite */
            foreach($connections as $sqlite) {
                // there should be no docblock here
                $sqlite->open('/my/database/path');
                <...>
            }

    型
    Type
        This is a generic name for anything that can be returned or provided as identity for a value.

        It is recommended to read the chapter :doc:`references/phpdoc/types` for a detailed description.

    完全修飾要素名
    FQSEN
    Fully Qualified Structural Element Name (FQSEN)
       Each documentable element can be referenced using a unique name based on its local name and any containers it is
       in.

       It is best demonstrated using an example:

           \\My\\Space\\MyClass::myMethod()

       This FQSEN identifies the *myMethod* method that is contained in the *MyClass* class, which in turn is contained
       inside the *My\\Space* namespace.

    テンプレート
    Template
    Templates
        Templates are configuration files that change how phpDocumentor renders the generated documentation.
        For an overview of templates, see :doc:`guides/templates`.

    Transformation
    Transformations
        Action definitions that are part of :term:`Templates` and are used to determine what the template does.

    サマリ
    要約
    Summary
      Sometimes called a short description, provides a brief introduction into the function of the associated element.

      「短い説明文」とも呼ばれ、函数または関連する要素の要約した紹介を書きます。

      A Summary ends
      in one of these situations:

      サマリの終端は以下のいづれかの場合です：

        1. A dot is following by a line break, or

           行の最後がドットで終る、または
        2. Two subsequent line breaks are encountered.

           二つの連続した改行があるとき。

    説明文
    Description
        Sometimes called the long description, it can provide more information than the :term:`Summary`. Examples of
        additional information are a description of a function's algorithm, a usage example, or a description of how a
        class fits in the whole of the application's architecture. The description ends when the first :term:`Tag`
        is encountered, or when the DocBlock is closed.

    タグ
    Tag
    Tags
        These provide a way to succinctly and uniformly provide meta-information about the associated element. This could,
        for example, describe the type of information that is returned by a method or function. Each tag is preceded by an
        at-sign (`@`) and starts on a new line.

    インラインタグ
    Inline Tag
    Inline Tags
        Some tags can also be used within text such as descriptions, such as the :doc:`references/phpdoc/tags/link` tag.
        Inline tags are surrounded by braces to set them apart from the surrounding text.

        :doc:`references/phpdoc/tags/link` など、いくつかのタグは説明文といったテキストの中にタグを使用できます。インラインタグは周囲と分離するため、波括弧 `{}` で括ります。

    アノテーション
    注釈
    Annotation
    Annotations
        An annotation is a specialized form of tag, that not only documents a specific aspect of the associated element,
        but also influences the way the application behaves.  Specific functionality depends on the library that is
        using them, for instance in Doctrine you can specify that a class represents a database entity as follows:

        アノテーションは特別な形式のタグで、関連要素の仕様を文書化するのみならず、アプリケーションの振舞に影響をもたらします。機能の仕様は利用するライブラリに依存しますが、Doctrineのインスタンスは次のようにデータベースのエンティティを記述できます。

        .. code-block:: php
            :linenos:

            /**
             * @ORM\Entity(repositoryClass="MyProject\UserRepository")
             */

        For more on annotations, see Rafael Dohms' `video presentation <http://protalk.me/annotating-with-annotations>`_ or `slides <http://www.slideshare.net/rdohms/annotations-in-php-they-exist>`_ on annotations.

        ほかのアノテーションについてはRafael Dohmsの `video presentation <http://protalk.me/annotating-with-annotations>`_ または `slides <http://www.slideshare.net/rdohms/annotations-in-php-they-exist>`_ をご覧ください。

    プラグイン
    Plugin
    サービスプロバイダ
    Service Provider
        A Service Provider is part of the Plugin system for phpDocumentor. Each plugin must have a Service Provider
        class that will bind the classes necessary for that plugin into the Dependency Injection Container or one of
        it services.

        The Service Provider is a concept coming from Pimple_, the dependency injection container powering
        phpDocumentor.

.. _Pimple: http://pimple.sensiolabs.org/
