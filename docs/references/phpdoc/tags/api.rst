@api
====

The @api tag is used to declare :term:`Structural Elements` as being suitable for
consumption by third parties.

@api タグは :term:`構造要素` が第三者(third parties)から利用されうることを宣言します。

構文
----

    @api

説明
----

The @api tag represents those :term:`Structural Elements` with a public visibility
which are intended to be the public API components for a library or framework.
Other :term:`Structural Elements` with a public visibility serve to support the
internal structure and are not recommended to be used by the consumer.

@apiタグは :term:`構造要素` がライブラリやフレームワークのために公開されたAPIの構成要素であることを表します。
そのほかの(@apiタグがつかない) public な :term:`構造要素` は内部構造であることを意味し、利用者が直接利用することは推奨されません。

The exact meaning of :term:`Structural Elements` tagged with @api MAY differ per
project. It is however RECOMMENDED that all tagged :term:`Structural Elements` SHOULD
NOT change after publication unless the new version is tagged as breaking
Backwards Compatibility.

@apiタグが付けられた :term:`構造要素` の正確な意味付けはプロジェクトことに異なります。
後方互換性のため、一度タグ付けされた :term:`構造要素` を後のバージョンで変更することは、後方互換性を破壊するため非推奨です。

phpDocumentorでの効果
------------------------

:term:`Structural Elements` tagged with the @api tag will be shown in a separate
sidebar section and the individual entry of will be marked as being an API element.

    Not all templates might show the API sidebar section; it is recommended to
    check this before using a specific template.

例
--------

.. code-block:: php
   :linenos:

    /**
     * This method will not change until a major release.
     *
     * @api
     *
     * @return void
     */
     function showVersion()
     {
        <...>
     }
