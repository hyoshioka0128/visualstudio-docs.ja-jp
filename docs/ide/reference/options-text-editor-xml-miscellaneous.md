---
title: '[オプション]、[テキスト エディター]、[XML]、[その他]'
ms.date: 10/29/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XML.Miscellaneous
ms.assetid: b6538cbe-badd-4313-a1fb-39e906736bbe
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: dd468945b1ab9ac83b219b9c8c396f017065e2be
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75568127"
---
# <a name="options-text-editor-xml-miscellaneous"></a>[オプション]、[テキスト エディター]、[XML]、[その他]

XML エディターのオート コンプリートとスキーマの設定を変更するには、 **[その他]** オプション ページを使用します。 その他の XML オプションにアクセスするには、 **[ツール]**  >  **[オプション]**  >  **[テキスト エディター]**  >  **[XML]** の順に選択して、 **[その他]** を選択します。

## <a name="auto-insert"></a>[自動挿入]

**終了タグ**

テキスト エディターでは、XML 要素を作成すると、終了タグが追加されます。 要素の開始タグが選択されている場合、エディターは、一致する名前空間プレフィックスも含めて、一致する終了タグを挿入します。 既定では、このチェック ボックスはオンです。

**属性値の引用符**

XML 属性の作成時にエディターは文字 `="` および `"` を挿入し、引用符の内側にキャレット ( **^** ) を配置します。 既定では、このチェック ボックスはオンです。

**名前空間の宣言**

名前空間の宣言が必要な場所には、自動的に宣言が挿入されます。 既定では、このチェック ボックスはオンです。

**その他のマークアップ (コメント、CDATA)**

コメント、CDATA、DOCTYPE、処理命令、その他のマークアップがオートコンプリートされます。 既定では、このチェック ボックスはオンです。

## <a name="network"></a>ネットワーク

**DTD とスキーマを自動的にダウンロードする**

スキーマと DTD (Document Type Definition) は HTTP ロケーションから自動的にダウンロードされます。 この機能では、自動プロキシ サーバー検出が有効な System.Net を使用します。 既定では、このチェック ボックスはオンです。

## <a name="outlining"></a>[アウトライン]

**[ファイルが開かれたときにアウトライン モードを実行する]**

ファイルが開いているときにアウトライン機能をオンにします。 既定では、このチェック ボックスはオンです。

## <a name="caching"></a>キャッシュ

**スキーマ**

スキーマ キャッシュの場所を指定します。 **[参照ボタン]** ボタンをクリックすると、新しいウィンドウで現在のスキーマ キャッシュの場所が開きます。 既定の場所は *%VsInstallDir%\xml\Schemas* です。

## <a name="see-also"></a>参照

- [XML オプション - 書式設定](options-text-editor-xml-formatting.md)
- [Visual Studio の XML ツール](../../xml-tools/xml-tools-in-visual-studio.md)
