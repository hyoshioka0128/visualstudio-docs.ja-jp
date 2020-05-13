---
title: List Source コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- Debug.ListSource
helpviewer_keywords:
- Debug.ListSource command
- list source command
- ListSource command
ms.assetid: e45f08d2-f4a3-49c3-9452-aa60508e2f74
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3f13689b6e3ac4db2d58c1def3a5d0dd05c219f2
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672320"
---
# <a name="list-source-command"></a>List Source コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ソース コードの指定行が表示されます。

## <a name="syntax"></a>構文

```
Debug.ListSource [/Count:number] [/Current] [/File:filename]
[/Line:number] [/ShowLineNumbers:yes|no]
```

## <a name="switches"></a>スイッチ
 /Count: `number` 省略可能です。 表示する行数を指定します。

 /現在のオプション。 現在の行を表示します。

 の場合: `filename` 省略可能です。 表示するファイルのパス。 ファイル名が指定されていない場合は、現在のステートメントの行のソース コードが表示されます。

 /Line: `number` 省略可能です。 特定の行番号を表示します。

 /ShowLineNumbers: `yes|no` 省略可能です。 行番号を表示するかどうかを指定します。

## <a name="remarks"></a>解説

## <a name="example"></a>例
 この例では、Form1.vb ファイルの 4 行目からソース コードが行番号付きでリストされます。

```
Debug.ListSource /File:"C:\Visual Studio Projects\Form1.vb" /Line:4 /ShowLineNumbers:yes
```

## <a name="see-also"></a>関連項目
 [Visual Studio コマンド](../../ide/reference/visual-studio-commands.md)の[コマンドウィンドウ](../../ide/reference/command-window.md)
