---
title: '[検索/コマンド] ボックス | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.findcommandbox
helpviewer_keywords:
- Find/Command box
ms.assetid: c81736dd-7a26-4e11-95c8-c2a2e56d7a41
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b7c5f9c19573a04b1d9a8d7b8c6e9450aef9bc44
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72645729"
---
# <a name="findcommand-box"></a>[検索/コマンド] ボックス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**[検索]** ボックスでは、テキストを検索し、Visual Studio コマンドを検索できます。 **[検索]** ボックスは、ツール バー コントロールとして使用できますが、既定では表示されません。 **[標準]** ツール バーの **[ボタンの追加または削除]** を選択し、 **[検索]** を選択すると、 **[検索]** ボックスを表示できます。

 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] コマンドを実行するには、コマンドの先頭に不等号 (&gt;) を付けます。

 **[検索]** ボックスでは、最近入力した 20 個のアイテムが記憶され、ドロップダウン リストに表示されます。 方向キーを選択すると、一覧を参照できます。

 ![[&#47;検索] コマンドボックス](../ide/media/findcommandbox.png "|::ref1::|")[検索/コマンド] ボックス

## <a name="searching-for-text"></a>テキストの検索
 既定では、 **[検索]** ボックスにテキストを指定して Enter キーを押すと、Visual Studio によって、 **[フォルダーを指定して検索]** ダイアログ ボックスで指定したオプションが使用され、現在のドキュメント ウィンドウまたはツール ウィンドウで検索されます。 詳細については、「 [Finding and Replacing Text](../ide/finding-and-replacing-text.md)」を参照してください。

## <a name="entering-commands"></a>コマンドの入力
 **[検索]** ボックスを使用して、文字列の検索ではなく、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の単一のコマンドまたはエイリアスを実行するには、先頭に不等号 (&gt;) を付けて [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] コマンドを入力します。 次に例を示します。

```
>File.NewFile c:\temp\MyFile /t:"General\Text File"
```

 または、コマンド ウィンドウを使って、単一または複数のコマンドを入力して実行することもできます。 コマンドまたはエイリアスには、単独で入力して実行できるものと、構文に引数の指定が必要なものがあります。 引数を持つコマンドの一覧については、「[Visual Studio コマンド](../ide/reference/visual-studio-commands.md)」をご覧ください。

## <a name="escape-characters"></a>エスケープ文字
 コマンド ラインにカレット (^) 文字があると、その直後の文字は制御文字としてではなくリテラル文字として解釈されます。 したがって、引用符 (")、スペース、先頭のスラッシュ、カレット、その他の任意のリテラル文字をパラメーターまたはスイッチの値に直接埋め込むことができます。ただし、スイッチ名には埋め込むことができません。 たとえば、オブジェクトに適用された

```
>Edit.Find ^^t /regex
```

 カレットは、引用符の前後のどちらに置かれた場合でも同じ働きをします。 行の最後の文字がカレットの場合は無視されます。

## <a name="see-also"></a>関連項目
 [コマンドウィンドウ](../ide/reference/command-window.md)[テキストの検索と置換](../ide/finding-and-replacing-text.md)
