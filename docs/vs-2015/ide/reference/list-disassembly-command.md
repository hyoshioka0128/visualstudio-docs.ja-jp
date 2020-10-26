---
title: List Disassembly コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.listdisassembly
helpviewer_keywords:
- Debug.ListDisassembly command
- list disassembly command
ms.assetid: eb363e35-e86a-4121-966f-991210c27e2a
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8ff5e620d4c53889afe17274364d6f92936025d3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672740"
---
# <a name="list-disassembly-command"></a>ListDisassembly コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッグ プロセスが開始され、エラーの処理方法を指定できるようになります。

## <a name="syntax"></a>構文

```
Debug.ListDisassembly [/count:number] [/endaddress:expression]
[/codebytes:yes|no] [/source:yes|no] [/symbolnames:yes|no]
[/linenumbers:yes|no]
```

## <a name="switches"></a>スイッチ
 各スイッチは、完全な形式または短い形式を使用して、呼び出すことができます。

 /カウント: `number` [または/c: `number` [または]/長さ: `number` [または]/L: `number` 省略可能。 表示する命令の数を指定します。 既定値は 8 です。

 /endaddress: `expression` [or]/e: `expression` 省略可能。 逆アセンブリを停止するアドレスを指定します。

 /codebytes: `yes`&#124;`no` [または]/bytes: `yes`&#124;`no` [or]/B: `yes`&#124;`no` 省略可能です。 コード バイトを表示するかどうかを指定します。 既定値は `no`にする必要があります。

 /source: `yes`&#124;`no` [] または/s `yes` : `no`&#124;省略可能です。 ソース コードを表示するかどうかを指定します。 既定値は `no` です。

 /symbolnames: `yes`&#124;`no` [または]/名前: `yes`&#124;`no` [または]/N: `yes`&#124;`no` 省略可能です。 シンボル名を表示するかどうかを指定します。 既定値は `yes`にする必要があります。

 [/linenumbers: `yes`&#124;`no` ] 省略可能です。 ソース コードに関連付けられている行番号の表示を有効にします。 /linenumbers スイッチを使用するには、/source スイッチの値が `yes` である必要があります。

## <a name="example"></a>例

```
>Debug.ListDisassembly
```

## <a name="see-also"></a>参照
 [呼び出し履歴の一覧表示コマンド](../../ide/reference/list-call-stack-command.md)[一覧のスレッドコマンド](../../ide/reference/list-threads-command.md) [visual studio コマンド](../../ide/reference/visual-studio-commands.md)[コマンドウィンドウ](../../ide/reference/command-window.md)の[検索/コマンドボックス](../../ide/find-command-box.md) [visual studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)
