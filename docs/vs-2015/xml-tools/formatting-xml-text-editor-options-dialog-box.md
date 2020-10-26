---
title: '[書式設定] ([オプション] ダイアログボックス-[テキストエディター]-[XML])Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: bb539b3a-027c-4b2f-906e-403e0e22ba8d
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 962321a1ab1a1ca5332300eea0d21781a9e4bbf5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670971"
---
# <a name="formatting-xml-text-editor-options-dialog-box"></a>[書式設定] ([オプション] ダイアログ ボックス - [テキスト エディター] - [XML])
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このダイアログ ボックスでは、XML エディターの書式設定を指定できます。 **[ツール]** メニューから **[オプション]** ダイアログ ボックスにアクセスできます。

> [!NOTE]
> 次の設定は、**[テキスト エディター]** フォルダーを展開し、**[XML]** フォルダーを展開して、**[オプション]** ダイアログ ボックスの **[書式設定]** オプションを選択したときに利用可能になります。

## <a name="attributes"></a>属性
 **手動による属性の書式設定を保持** する属性は再フォーマットされません。 既定値です。

> [!NOTE]
> 属性が複数行にある場合、エディターは属性の各行にインデントを設定して、親要素のインデントに一致させます。

 **属性をそれぞれの行に配置** する最初の属性のインデントに一致するように、2番目とそれ以降の属性を垂直方向に揃えます。 次の XML テキストは、属性を配置する方法の例です。

```
<item id = "123-A"
      name = "hammer"
      price = "9.95">
</item>
```

## <a name="auto-reformat"></a>[自動再フォーマット]
 **クリップボードからの貼り付け時** クリップボードから貼り付けられた XML テキストを再フォーマットします。

 **終了タグの完了時** 終了タグが完了したときに要素を再フォーマットします。

## <a name="mixed-content"></a>混合コンテンツ
 **既定で混合コンテンツを保持** するエディターが混合コンテンツを再フォーマットするかどうかを決定します。 既定では、コンテンツが `xml:space="preserve"` スコープで見つかった場合を除き、エディターは混合コンテンツの書式を再設定しようとします。

 要素にテキストとマークアップが混在している場合、コンテンツは混合コンテンツと見なされます。 混合コンテンツを持つ要素の例を次に示します。

```
<dir>c:\data\AlphaProject\
  <file readOnly="false">test1.txt</file>
  <file readOnly="false">test2.txt</file>
</dir>
```

## <a name="see-also"></a>参照
 [Xml ドキュメントのプロパティ、[プロパティ] ウィンドウの](../xml-tools/xml-document-properties-properties-window.md) [Xml エディターのコンポーネント](../xml-tools/xml-editor-components.md)
