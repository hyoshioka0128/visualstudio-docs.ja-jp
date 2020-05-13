---
title: New File コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- file.newfile
helpviewer_keywords:
- File.NewFile command
- New File command
ms.assetid: 767868d6-a525-425b-a43b-2198f636ab6b
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8e0d25d585f518c854ad6176ae4ae7a5f27b22ad
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671957"
---
# <a name="new-file-command"></a>NewFile コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

新規ファイルを作成して開きます。 ファイルは [その他のファイル] フォルダーの下に表示されます。

## <a name="syntax"></a>構文

```
File.NewFile [filename] [/t:templatename] [/editor:editorname]
```

## <a name="arguments"></a>引数
 `filename` 省略可能。 ファイルの名前。 名前を指定しない場合は、既定の名前が付けられます。 テンプレート名がない場合は、テキスト ファイルが作成されます。

## <a name="switches"></a>スイッチ
 /t:`templatename` 省略可能。 作成するファイルの種類を指定します。

 /t:`templatename` 引数の構文は、[新しいファイル] ダイアログ ボックスにある情報を反映します。 カテゴリ名に続けて円記号 (`\`)、およびテンプレート名を入力し、文字列全体を引用符で囲みます。

 たとえば、新しい [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] ソース ファイルを作成するには、/t:`templatename` 引数に対して次のように入力します。

```
/t:"Visual C++\C++ File (.cpp)"
```

 上の例で、C++ File のテンプレートは **[新しいファイル]** ダイアログ ボックスの [Visual C++] カテゴリにあります。

 /e:`editorname` 省略可能。 ファイルを開くために使用するエディターの名前です。 引数は指定されていても、エディター名がない場合、 **[プログラムから開く]** ダイアログ ボックスが表示されます。

 /e:`editorname` 引数の構文では、[ファイルを開くアプリケーションの選択] ダイアログ ボックスで表示されるようにエディター名を入力し、引用符で囲みます。

 たとえば、ソース コード エディターでファイルを開くには、/e:`editorname` 引数に対して次のように入力します。

```
/e:"Source Code (text) Editor"
```

## <a name="example"></a>例
 次の例では、Web ページ "test1.htm" を新規作成し、それをソース コード エディターで開きます。

```
>File.NewFile test1 /t:"General\HTML Page" /e:"Source Code (text) Editor"
```

## <a name="see-also"></a>関連項目
 [Visual Studio コマンド](../../ide/reference/visual-studio-commands.md)[コマンドウィンドウ](../../ide/reference/command-window.md)[イミディエイトウィンドウ](../../ide/reference/immediate-window.md)の[[検索]/[コマンド] ボックス](../../ide/find-command-box.md) [visual studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)
