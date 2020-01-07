---
title: FindinFiles コマンド
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- edit.findinfiles
helpviewer_keywords:
- Edit.FindInFiles command
- find in files command
ms.assetid: 2fc78bfe-b339-4599-97f9-4cafd8a194d9
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 25342f86c545752a263d295550222e14c2aa7866
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748776"
---
# <a name="find-in-files-command"></a>FindinFiles コマンド
**[検索と置換]** ウィンドウの **[フォルダーを指定して検索]** タブにあるオプションのサブセットを使って、ファイルを検索します。

## <a name="syntax"></a>構文

```cmd
Edit.FindinFiles findwhat [/case] [/ext:extensions]
[/lookin:searchpath] [/names] [/options] [/reset] [/stop] [/sub]
[/text2] [/wild|/regex] [/word]
```

## <a name="arguments"></a>引数

`findwhat`\
必須です。 検索するテキスト。

## <a name="switches"></a>スイッチ
/case または /c\
任意。 `findwhat` 引数で指定されている語句と大文字および小文字の使い分けが正確に一致する場合にのみ、一致と見なします。

/ext: `extensions`\
任意。 検索するファイルのファイル拡張子を指定します。 指定しないと、前に入力したものがある場合はそれが使われます。

/lookin: `searchpath`\
任意。 検索するディレクトリ。 パスにスペースが含まれる場合は、パス全体を引用符で囲みます。

/names または /n\
任意。 一致を含むファイル名の一覧を表示します。

/options または /t\
任意。 現在の検索オプションの設定の一覧を表示し、検索は行いません。

/regex または /r\
任意。 `findwhat` 引数に含まれる定義済みの特殊文字を、リテラル文字ではなく、テキストのパターンを表す表記として使います。 正規表現文字の一覧については、「[正規表現](../../ide/using-regular-expressions-in-visual-studio.md)」をご覧ください。

/reset または /e\
任意。 検索オプションを既定の設定に戻し、検索は行いません。

/stop\
任意。 現在実行中の検索操作がある場合は、それを停止します。 `/stop` を指定すると、他のすべての引数は無視されます。 たとえば、現在の検索を停止するには、次のように入力します。

```cmd
>Edit.FindinFiles /stop
```

/sub または /s\
任意。 /lookin:`searchpath` 引数で指定したディレクトリ内のサブフォルダーを検索します。

/text2 または /2\
任意。 検索の結果を [検索結果 2] ウィンドウに表示します。

/wild または /l\
任意。 `findwhat` 引数に含まれる定義済みの特殊文字を、文字または文字のシーケンスを表す表記として使います。

/word または /w\
任意。 単語全体と一致するもののみを検索します。

## <a name="example"></a>例
次の例では、"My Visual Studio Projects" フォルダーにあるすべての .cls ファイルで "btnCancel" を検索し、一致情報を [検索結果 2] ウィンドウに表示します。

```cmd
>Edit.FindinFiles btnCancel /lookin:"c:/My Visual Studio Projects" /ext:*.cls /text2
```

## <a name="see-also"></a>関連項目

- [フォルダーを指定して検索](../../ide/find-in-files.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
