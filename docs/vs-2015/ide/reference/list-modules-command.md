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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
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
 /Address: `yes|no` 省略可能。 モジュールのメモリ アドレスを表示するかどうかを指定します。 既定値は `yes`にする必要があります。

 /Name:`yes|no` 省略可能です。 モジュールの名前を表示するかどうかを指定します。 既定値は `yes`にする必要があります。

 /Order: `yes|no` 省略可能。 モジュールの順序を表示するかどうかを指定します。 既定値は `no`にする必要があります。

 /Path: `yes|no` 省略可能。 モジュールのパスを表示するかどうかを指定します。 既定値は `yes` です。

 /Process: `yes|no` 省略可能。 モジュールのプロセスを表示するかどうかを指定します。 既定値は `no`にする必要があります。

 /SymbolFile: `yes|no` 省略可能。 モジュールのシンボル ファイルを表示するかどうかを指定します。 既定値は `no`にする必要があります。

 /SymbolStatus: `yes|no` 省略可能。 モジュールのシンボル ステータスを表示するかどうかを指定します。 既定値は `yes`にする必要があります。

 /Timestamp: `yes|no` 省略可能。 モジュールのタイムスタンプを表示するかどうかを指定します。 既定値は `no` です。

 /Version:`yes|no` 省略可能です。 モジュールのバージョンを表示するかどうかを指定します。 既定値は `no`にする必要があります。

## <a name="remarks"></a>Remarks

## <a name="example"></a>例
 次の例では、現在のプロセスのモジュール名、アドレス、およびタイムスタンプを一覧表示します。

```
Debug.ListModules /Address:yes /Name:yes /Order:no /Path:no /Process:no /SymbolFile:no /SymbolStatus:no /Timestamp:yes /Version:no
```

## <a name="see-also"></a>参照
 [Visual Studio コマンド](../../ide/reference/visual-studio-commands.md)の[コマンドウィンドウ](../../ide/reference/command-window.md)[方法: [モジュール] ウィンドウを使用する](../../debugger/how-to-use-the-modules-window.md)
