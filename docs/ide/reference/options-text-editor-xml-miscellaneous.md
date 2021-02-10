---
title: '[オプション]、[テキスト エディター]、[XML]、[その他]'
description: '[XAML] セクションの [その他] ページを使用して、XML エディターのオート コンプリートとスキーマの設定を変更する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 10/29/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XML.Miscellaneous
ms.assetid: b6538cbe-badd-4313-a1fb-39e906736bbe
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.openlocfilehash: d3451a2a8d64edbf0f9000c9e58387704ed815ba
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99932272"
---
# <a name="options-text-editor-xml-miscellaneous"></a>[オプション]、[テキスト エディター]、[XML]、[その他]

XML エディターのオート コンプリートとスキーマの設定を変更するには、**[その他]** オプション ページを使用します。 その他の XML オプションにアクセスするには、 **[ツール]**  >  **[オプション]**  >  **[テキスト エディター]**  >  **[XML]** の順に選択して、 **[その他]** を選択します。

## <a name="auto-insert"></a>自動挿入

**終了タグ**

テキスト エディターでは、XML 要素を作成すると、終了タグが追加されます。 要素の開始タグが選択されると、対応する終了タグが挿入されます。この場合、対応する名前空間プレフィックスも含められます。 既定では、このチェック ボックスはオンになっています。

**属性値の引用符**

XML 属性の作成時にエディターは文字 `="` および `"` を挿入し、引用符の内側にキャレット ( **^** ) を配置します。 既定では、このチェック ボックスはオンになっています。

**名前空間の宣言**

名前空間の宣言が必要な場所には、自動的に宣言が挿入されます。 既定では、このチェック ボックスはオンになっています。

**[その他のマークアップ (コメント、CDATA)]**

コメント、CDATA、DOCTYPE、処理命令、その他のマークアップがオートコンプリートされます。 既定では、このチェック ボックスはオンになっています。

## <a name="network"></a>ネットワーク

**[DTD とスキーマを自動的にダウンロードする]**

スキーマと DTD (Document Type Definition) は HTTP ロケーションから自動的にダウンロードされます。 この機能では、自動プロキシ サーバー検出が有効な System.Net を使用します。 既定では、このチェック ボックスはオンになっています。

## <a name="outlining"></a>アウトライン

**ファイルが開かれたときにアウトライン モードを実行する**

ファイルが開いているときにアウトライン機能をオンにします。 既定では、このチェック ボックスはオンになっています。

## <a name="caching"></a>キャッシュ

**スキーマ**

スキーマ キャッシュの場所を指定します。 **[参照ボタン]** ボタンをクリックすると、新しいウィンドウで現在のスキーマ キャッシュの場所が開きます。 既定の場所は *%VsInstallDir%\xml\Schemas* です。

## <a name="see-also"></a>関連項目

- [XML オプション - 書式設定](options-text-editor-xml-formatting.md)
- [Visual Studio の XML ツール](../../xml-tools/xml-tools-in-visual-studio.md)
