---
title: 既存項目の追加コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- project.addexistingitem
helpviewer_keywords:
- File.AddExistingItem command
- Add Existing Item command
ms.assetid: 41f56131-d4c7-4f81-83b7-bdac713ea870
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c2f636c2a0eb2cfdcebf383fdc7eea70f72cb90e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670236"
---
# <a name="add-existing-item-command"></a>AddExistingSolutionItem コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

既存のファイルを現在のソリューションに追加して、そのファイルを開きます。

## <a name="syntax"></a>構文

```
File.AddExistingItem filename [/e:editorname]
```

## <a name="arguments"></a>引数
 `filename` 必須。 現在のソリューションに追加する項目の完全なパスとファイル名 (拡張子付き)。 ファイル パスまたはファイル名にスペースが含まれている場合は、パス全体を引用符で囲みます。

## <a name="switches"></a>スイッチ
 /e: `editorname` 省略可能。 ファイルを開くために使用するエディターの名前です。 引数は指定されていても、エディター名がない場合、 **[プログラムから開く]** ダイアログ ボックスが表示されます。

 /e:`editorname` 引数の構文では、 **[プログラムから開く] ダイアログ ボックス**に表示されるエディター名 (引用符で囲まれている) が使用されます。 たとえば、ソース コード エディターでスタイル シートを開く場合、/e:`editorname` 引数に対して次のように入力します。

```
/e:"Source Code (text) Editor"
```

## <a name="remarks"></a>解説
 オート コンプリートでは、入力された正しいパスとファイル名の検索を試みます。

## <a name="example"></a>例
 この例では、Form1.frm というファイルを現在のソリューションに追加します。

```
>File.AddExistingItem "C:\public\solution files\Form1.frm"
```

## <a name="see-also"></a>関連項目
 [Visual Studio コマンド](../../ide/reference/visual-studio-commands.md)の[コマンドウィンドウ](../../ide/reference/command-window.md)の[検索/コマンドボックス](../../ide/find-command-box.md) [visual studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)
