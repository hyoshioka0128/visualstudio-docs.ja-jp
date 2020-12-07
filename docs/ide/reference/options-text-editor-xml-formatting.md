---
title: '[オプション]、[テキスト エディター]、[XML]、[書式設定]'
description: '[XML] セクションの [書式設定] ページを使用して、XML ドキュメントの要素と属性の書式設定方法を指定する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 10/29/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XML.Formatting
ms.assetid: 203e60b2-7b80-4ff4-9fa1-aa9f4374377b
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 9aac9420d084c64a4bd5d9199f6a7ca96b8c4281
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96040512"
---
# <a name="options-text-editor-xml-formatting"></a>[オプション]、[テキスト エディター]、[XML]、[書式設定]

**[書式設定]** オプション ページでを使用して、XML ドキュメントで要素と属性を書式設定する方法を指定します。 XML 書式設定オプションにアクセスするには、 **[ツール]**  >  **[オプション]**  >  **[テキスト エディター]**  >  **[XML]** の順に選択して、 **[書式設定]** を選択します。

## <a name="attributes"></a>属性

**[手動による属性の書式設定を保持する]**

属性の書式設定を変更しません。 これは、既定の設定です。

> [!NOTE]
> 属性が複数行にある場合、エディターは属性の各行にインデントを設定して、親要素のインデントに一致させます。

**[各行の属性の記述位置を揃える]**

2 番目以降の属性を縦に配置して、最初の属性のインデントに一致させます。 XML テキストで属性がどのように並べられるかについて例を次に示します。

```xml
<item id = "123-A"
      name = "hammer"
      price = "9.95">
</item>
```

## <a name="auto-reformat"></a>[自動再フォーマット]

**クリップボードからの貼り付け時**

クリップボードから貼り付けられる XML テキストの書式設定を変更します。

**[終了タグの完了時]**

終了タグが完了するときに、要素の書式設定を変更します。

## <a name="mixed-content"></a>混合コンテンツ

**[混合したコンテンツを既定でフォーマットする]**

コンテンツが `xml:space="preserve"` 範囲内で検出された場合以外は、混合コンテンツの書式設定を変更します。 これは、既定の設定です。

要素にテキストとマークアップが混在している場合、コンテンツは混合コンテンツと見なされます。 次に、混合コンテンツを含む要素の例を示します。

```xml
<dir>c:\data\AlphaProject\
  <file readOnly="false">test1.txt</file>
  <file readOnly="false">test2.txt</file>
</dir>
```

## <a name="see-also"></a>関連項目

- [XML オプション - その他](options-text-editor-xml-miscellaneous.md)
- [Visual Studio の XML ツール](../../xml-tools/xml-tools-in-visual-studio.md)
