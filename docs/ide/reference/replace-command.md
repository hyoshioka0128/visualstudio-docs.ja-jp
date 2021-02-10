---
title: Replace コマンド
description: Replace コマンドと、それを使用することにより、[検索と置換] ウィンドウの [フォルダーを指定して置換] タブにあるオプションのサブセットを使用してファイル内のテキストを置換する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- edit.replace
helpviewer_keywords:
- Edit.Replace command
- Replace command
ms.assetid: a15767f1-5a3d-44f5-8c77-7b0f1157f340
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6c3149b55c2b5b3a5ca666fbd780e4efbd03ef22
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99958064"
---
# <a name="replace-command"></a>Replace コマンド
**[検索と置換]** ウィンドウの **[フォルダーを指定して置換]** タブにあるオプションのサブセットを使用してファイル内のテキストを置換します。

## <a name="syntax"></a>構文

```
Edit.Replace findwhat replacewith [/all] [/case]
[/doc|/proc|/open|/sel] [/hidden] [/options] [/reset] [/up]
[/wild|/regex] [/word]
```

## <a name="arguments"></a>引数
`findwhat`

必須です。 検索するテキスト。

`replacewith`

必須。 一致したテキストと置き換えるテキスト。

## <a name="switches"></a>スイッチ
/all または /a

任意。 検索されたすべてのテキストを置換します。

/case または /c

任意。 `findwhat` 引数に指定したテキストと大文字/小文字が完全に一致する場合にだけ、一致したと見なされます。

/doc または /d

任意。 現現在のドキュメントだけを検索します。 使用可能な検索スコープの中から 1 つだけ指定します (`/doc`、`/proc`、`/open`、または `/sel`)。

/hidden または /h

任意。 デザイン時のコントロールのメタデータ、アウトライン表示のドキュメントの非表示の領域、折りたたまれているクラスやメソッドのような、折りたたまれて非表示になっているテキストを検索します。

/open または /o

任意。 開いているすべてのドキュメントを 1 つのドキュメントであるかのように検索します。 使用可能な検索スコープの中から 1 つだけ指定します (`/doc`、`/proc`、`/open`、または `/sel`)。

/options または /t

任意。 現在の検索オプションの設定の一覧を表示し、検索は行いません。

/proc または /p

任意。 現在のプロシージャだけを検索します。 使用可能な検索スコープの中から 1 つだけ指定します (`/doc`、`/proc`、`/open`、または `/sel`)。

/regex または /r

任意。 `findwhat` 引数に含まれる定義済みの特殊文字を、リテラル文字ではなく、テキストのパターンを表す表記として使います。 正規表現文字の一覧については、「[正規表現](../../ide/using-regular-expressions-in-visual-studio.md)」をご覧ください。

/reset または /e

任意。 検索オプションを既定の設定に戻し、検索は行いません。

/sel または /s

任意。 現在の選択項目だけを検索します。 使用可能な検索スコープの中から 1 つだけ指定します (`/doc`、`/proc`、`/open`、または `/sel`)。

/up または /u

任意。 現在の位置から上方向にファイルを検索します。 既定では、ファイルの現在位置から検索を開始し、下方向に検索されます。

/wild または /l

任意。 `findwhat` 引数に含まれる定義済みの特殊文字を、文字または文字のシーケンスを表す表記として使います。

/word または /w

任意。 単語全体と一致するもののみを検索します。

## <a name="example"></a>例
次の例では、開いているすべてのドキュメントで `btnSend` を検索し、`btnSubmit` に置換します。

```
>Edit.Replace btnSend btnSubmit /open
```

## <a name="see-also"></a>関連項目

- [テキストの検索と置換](../../ide/finding-and-replacing-text.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
