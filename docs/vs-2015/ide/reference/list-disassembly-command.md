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
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
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

 /カウント: `number` [または/c: `number` [または]/長さ: `number` [または]/l: `number` 省略可能です。 表示する命令の数を指定します。 既定値は 8 です。

 /endaddress: `expression` [または/e: `expression` 省略可能です。 逆アセンブリを停止するアドレスを指定します。

 /codebytes: `yes`&#124; `no` [または]/バイト:&#124; `yes` `no` [または/B:&#124; `yes` `no` 省略可能です。 コード バイトを表示するかどうかを指定します。 既定値は `no`にする必要があります。

 /source: `yes`&#124; `no` [または/s: `yes`&#124; `no` 省略可能です。 ソース コードを表示するかどうかを指定します。 既定値は `no`にする必要があります。

 /symbolnames: `yes`&#124; `no` [または]/名前:&#124; `yes` `no` [または]/N&#124; : `yes` `no` 省略可能です。 シンボル名を表示するかどうかを指定します。 既定値は `yes`にする必要があります。

 [/linenumbers: `yes`&#124; `no`]Optional. ソース コードに関連付けられている行番号の表示を有効にします。 /linenumbers スイッチを使用するには、/source スイッチの値が `yes` である必要があります。

## <a name="example"></a>例

```
>Debug.ListDisassembly
```

## <a name="see-also"></a>関連項目
 [呼び出し履歴の一覧表示コマンド](../../ide/reference/list-call-stack-command.md)[一覧のスレッドコマンド](../../ide/reference/list-threads-command.md) [visual studio コマンド](../../ide/reference/visual-studio-commands.md)[コマンドウィンドウ](../../ide/reference/command-window.md)の[検索/コマンドボックス](../../ide/find-command-box.md) [visual studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)
