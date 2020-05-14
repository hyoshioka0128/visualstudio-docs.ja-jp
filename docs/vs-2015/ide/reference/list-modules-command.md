---
title: List Modules コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.listmodules
helpviewer_keywords:
- Debug.ListModules command
- ListModules command
- list modules command
ms.assetid: 3cb73774-6ac0-43b2-b781-75ed47175bfd
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4600f27f62d6e840041a65b4128df128e4d36873
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659526"
---
# <a name="list-modules-command"></a>List Modules コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

現在のプロセスのモジュールが一覧表示されます。

## <a name="syntax"></a>構文

```
Debug.ListModules [/Address:yes|no] [/Name:yes|no] [/Order:yes|no]
[/Path:yes|no] [/Process:yes|no] [/SymbolFile:yes|no]
[/SymbolStatus:yes|no] [/Timestamp:yes|no] [/Version:yes|no]
```

#### <a name="parameters"></a>パラメーター
 /Address: `yes|no` 省略可能です。 モジュールのメモリ アドレスを表示するかどうかを指定します。 既定値は `yes`にする必要があります。

 /Name:`yes|no` 省略可能です。 モジュールの名前を表示するかどうかを指定します。 既定値は `yes`にする必要があります。

 /Order: `yes|no` 省略可能です。 モジュールの順序を表示するかどうかを指定します。 既定値は `no`にする必要があります。

 /Path: `yes|no` 省略可能です。 モジュールのパスを表示するかどうかを指定します。 既定値は `yes`にする必要があります。

 /Process: `yes|no` 省略可能です。 モジュールのプロセスを表示するかどうかを指定します。 既定値は `no`にする必要があります。

 /SymbolFile: `yes|no` 省略可能です。 モジュールのシンボル ファイルを表示するかどうかを指定します。 既定値は `no`にする必要があります。

 /SymbolStatus: `yes|no` 省略可能です。 モジュールのシンボル ステータスを表示するかどうかを指定します。 既定値は `yes`にする必要があります。

 /Timestamp: `yes|no` 省略可能です。 モジュールのタイムスタンプを表示するかどうかを指定します。 既定値は `no`にする必要があります。

 /Version:`yes|no` 省略可能です。 モジュールのバージョンを表示するかどうかを指定します。 既定値は `no`にする必要があります。

## <a name="remarks"></a>解説

## <a name="example"></a>例
 次の例では、現在のプロセスのモジュール名、アドレス、およびタイムスタンプを一覧表示します。

```
Debug.ListModules /Address:yes /Name:yes /Order:no /Path:no /Process:no /SymbolFile:no /SymbolStatus:no /Timestamp:yes /Version:no
```

## <a name="see-also"></a>関連項目
 [Visual Studio コマンド](../../ide/reference/visual-studio-commands.md)の[コマンドウィンドウ](../../ide/reference/command-window.md)[方法: [モジュール] ウィンドウを使用する](../../debugger/how-to-use-the-modules-window.md)
