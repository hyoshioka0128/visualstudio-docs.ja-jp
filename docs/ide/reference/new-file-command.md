---
title: NewFile コマンド
description: NewFile コマンドと、それを使用することで新しいファイルを作成して開く方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- file.newfile
helpviewer_keywords:
- File.NewFile command
- New File command
ms.assetid: 767868d6-a525-425b-a43b-2198f636ab6b
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c800ce0ed130ed78f9537584c95a29a717f405fa
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2020
ms.locfileid: "96304098"
---
# <a name="new-file-command"></a>NewFile コマンド
新規ファイルを作成して開きます。 ファイルは [その他のファイル] フォルダーの下に表示されます。

## <a name="syntax"></a>構文

```cmd
File.NewFile [filename] [/t:templatename] [/editor:editorname]
```

## <a name="arguments"></a>引数
`filename`

任意。 ファイルの名前。 名前を指定しない場合は、既定の名前が付けられます。 テンプレート名がない場合は、テキスト ファイルが作成されます。

## <a name="switches"></a>スイッチ
/t:`templatename`\
省略可能。 作成するファイルの種類を指定します。

/t:`templatename` 引数の構文は、[新しいファイル] ダイアログ ボックスにある情報を反映します。 カテゴリ名に続けて円記号 (`\`)、およびテンプレート名を入力し、文字列全体を引用符で囲みます。

たとえば、新しい [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] ソース ファイルを作成するには、/t:`templatename` 引数に対して次のように入力します。

```cmd
/t:"Visual C++\C++ File (.cpp)"
```

上の例で、C++ File のテンプレートは **[新しいファイル]** ダイアログ ボックスの [Visual C++] カテゴリにあります。

/e:`editorname`\
省略可能。 ファイルを開くために使用するエディターの名前です。 引数は指定されていても、エディター名がない場合、**[プログラムから開く]** ダイアログ ボックスが表示されます。

/e:`editorname` 引数の構文では、[ファイルを開くアプリケーションの選択] ダイアログ ボックスで表示されるようにエディター名を入力し、引用符で囲みます。

たとえば、ソース コード エディターでファイルを開くには、/e:`editorname` 引数に対して次のように入力します。

```cmd
/e:"Source Code (text) Editor"
```

## <a name="example"></a>例
次の例では、Web ページ "test1.htm" を新規作成し、それをソース コード エディターで開きます。

```cmd
>File.NewFile test1 /t:"General\HTML Page" /e:"Source Code (text) Editor"
```

## <a name="see-also"></a>関連項目

- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [イミディエイト ウィンドウ](../../ide/reference/immediate-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
