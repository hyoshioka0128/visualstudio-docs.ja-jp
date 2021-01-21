---
title: List Modules コマンド
description: List Modules コマンドと、これにより、現在のプロセスのモジュールを一覧表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.listmodules
helpviewer_keywords:
- Debug.ListModules command
- ListModules command
- list modules command
ms.assetid: 3cb73774-6ac0-43b2-b781-75ed47175bfd
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fa0c3f6445a22ee80457e8a7f9f24fb7008f77ed
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2020
ms.locfileid: "96305308"
---
# <a name="list-modules-command"></a>List Modules コマンド
現在のプロセスのモジュールが一覧表示されます。

## <a name="syntax"></a>構文

```
Debug.ListModules [/Address:yes|no] [/Name:yes|no] [/Order:yes|no]
[/Path:yes|no] [/Process:yes|no] [/SymbolFile:yes|no]
[/SymbolStatus:yes|no] [/Timestamp:yes|no] [/Version:yes|no]
```

#### <a name="parameters"></a>パラメーター
/Address:`yes|no`

任意。 モジュールのメモリ アドレスを表示するかどうかを指定します。 既定値は `yes` です。

/Name:`yes|no`

任意。 モジュールの名前を表示するかどうかを指定します。 既定値は `yes` です。

/Order:`yes|no`

任意。 モジュールの順序を表示するかどうかを指定します。 既定値は `no` です。

/Path:`yes|no`

任意。 モジュールのパスを表示するかどうかを指定します。 既定値は `yes` です。

/Process:`yes|no`

任意。 モジュールのプロセスを表示するかどうかを指定します。 既定値は `no` です。

/SymbolFile:`yes|no`

任意。 モジュールのシンボル ファイルを表示するかどうかを指定します。 既定値は `no` です。

/SymbolStatus:`yes|no`

任意。 モジュールのシンボル ステータスを表示するかどうかを指定します。 既定値は `yes` です。

/Timestamp:`yes|no`

任意。 モジュールのタイムスタンプを表示するかどうかを指定します。 既定値は `no` です。

/Version:`yes|no`

任意。 モジュールのバージョンを表示するかどうかを指定します。 既定値は `no` です。

## <a name="example"></a>例
次の例では、現在のプロセスのモジュール名、アドレス、およびタイムスタンプを一覧表示します。

```
Debug.ListModules /Address:yes /Name:yes /Order:no /Path:no /Process:no /SymbolFile:no /SymbolStatus:no /Timestamp:yes /Version:no
```

## <a name="see-also"></a>関連項目

- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [方法: [モジュール] ウィンドウを使用する](../../debugger/how-to-use-the-modules-window.md)
