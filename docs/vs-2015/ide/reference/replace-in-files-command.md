---
title: Replace In Files コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- edit.replaceinfiles
helpviewer_keywords:
- Edit.ReplaceInFiles command
- Replace In Files command
- ReplaceInFiles command
ms.assetid: f116066a-4f65-4f2c-94ef-12cbd8cfb598
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3d5088366548c9f92d04f1b65a3afc378db29d6a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665617"
---
# <a name="replace-in-files-command"></a>ReplaceinFiles コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**[検索と置換]** ウィンドウの **[フォルダーを指定して置換]** タブにあるオプションのサブセットを使用してファイル内のテキストを置換します。

## <a name="syntax"></a>構文

```
Edit.ReplaceinFiles findwhat replacewith [/all] [/case]
[/ext:extensions] [/keep] [/lookin:searchpath] [/options] [/regex]
[/reset] [/stop] [/sub] [/text2] [/wild] [/word]
```

## <a name="arguments"></a>引数
 `findwhat` 必須。 検索するテキスト。

 `replacewith` 必須。 一致したテキストと置き換えるテキスト。

## <a name="switches"></a>スイッチ
 /all または/a 省略可能。 検索されたすべてのテキストを置換します。

 /case または /c 省略可能。 `findwhat` 引数に指定したテキストと大文字/小文字が完全に一致する場合にだけ、一致したと見なされます。

 /ext: `extensions` 省略可能。 検索するファイルのファイル拡張子を指定します。

 /keep または/k 省略可能。 すべての変更されたファイルを開いたままにするように指定します。

 /lookin: `searchpath` 省略可能。 検索するディレクトリ。 パスにスペースが含まれる場合は、パス全体を引用符で囲みます。

 /options または /t 省略可能。 現在の検索オプションの設定の一覧を表示し、検索は行いません。

 /regex または /r 省略可能。 `findwhat` 引数に含まれる定義済みの特殊文字を、リテラル文字ではなく、テキストのパターンを表す表記として使います。 正規表現文字の一覧については、「[正規表現](../../ide/using-regular-expressions-in-visual-studio.md)」をご覧ください。

 /reset または /e 省略可能。 検索オプションを既定の設定に戻し、検索は行いません。

 /stop 省略可能。 現在実行中の検索操作がある場合は、それを停止します。 `/stop` を指定すると、他のすべての引数は無視されます。 たとえば、現在の置換操作を中止するには、次のように入力します。

```
>Edit.ReplaceinFiles /stop
```

 /sub または /s 省略可能。 /lookin:`searchpath` 引数で指定したディレクトリ内のサブフォルダーを検索します。

 /text2 または /2 省略可能。 **[検索結果 2]** ウィンドウに置換結果を表示します。

 /wild または /l 省略可能。 `findwhat` 引数に含まれる定義済みの特殊文字を、文字または文字のシーケンスを表す表記として使います。

 /word または /w 省略可能。 完全に一致する単語だけを検索します。

## <a name="example"></a>例
 次の例では、"my visual studio projects" フォルダーに含まれるすべての .cls ファイルで `btnCancel` を検索し、それを `btnReset` に置換して、 **[検索結果 2]** ウィンドウに置換情報を表示します。

```
>Edit.ReplaceinFiles btnCancel btnReset /lookin:"c:/my visual studio projects" /ext:.cls /text2
```

## <a name="see-also"></a>関連項目
 [検索と置換](../../ide/finding-and-replacing-text.md) [(フォルダー内のテキストの置換](../../ide/replace-in-files.md))[コマンドウィンドウ](../../ide/reference/command-window.md)[検索] [/[コマンド] ボックス](../../ide/find-command-box.md) [visual studio](../../ide/reference/visual-studio-commands.md)コマンド visual studio コマンドの[エイリアス](../../ide/reference/visual-studio-command-aliases.md)
