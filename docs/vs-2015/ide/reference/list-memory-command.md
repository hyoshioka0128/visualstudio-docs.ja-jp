---
title: ListMemory コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.listmemory
helpviewer_keywords:
- Debug.ListMemory command
- ListMemory command
- list memory command
ms.assetid: a84de361-a6a6-4f6d-96aa-a0d4a424371e
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2630402e03d1256f63e542818a9066745206d2c5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672755"
---
# <a name="list-memory-command"></a>ListMemory コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定範囲のメモリの内容を表示します。

## <a name="syntax"></a>構文

```
Debug.ListMemory [/ANSI|Unicode] [/Count:number] [/Format:formattype]
[/Hex|Signed|Unsigned] [expression]
```

## <a name="arguments"></a>引数
 `expression` 省略可能。 メモリの表示を開始するメモリ アドレス。

## <a name="switches"></a>スイッチ
 /ANSI&#124;Unicode オプション。 メモリを、メモリ バイトに対応する ANSI 文字または Unicode 文字として表示します。

 /Count: `number` 省略可能です。 表示するメモリを `expression` からのバイト数で指定します。

 /Format: `formattype` 省略可能です。 **[メモリ]** ウィンドウにメモリ情報を表示する場合の形式の種類は、OneByte、TwoBytes、FourBytes、EightBytes、Float (32 ビット)、または Double (64 ビット) を指定できます。 OneByte を使用する場合、`/Unicode` は使用できません。

 /16&#124;進数&#124;の符号付き符号なしオプション。 数字の表示形式を、符号付き、符号なし、または 16 進数のいずれかに指定します。

## <a name="remarks"></a>解説
 すべてのスイッチを指定して完全な **Debug.ListMemory** コマンドを記述する代わりに、特定のスイッチが指定された値に事前に設定された定義済みのエイリアスを使用してコマンドを起動することもできます。 以下に例を示します。

```
>Debug.ListMemory /Format:float /Count:30 /Unicode
```

 上のコードを入力する代わりに、次のように記述できます。

```
>df /Count:30 /Unicode
```

 **Debug.ListMemory** コマンドで使用できるエイリアスの一覧を以下に示します。

|Alias|コマンドおよびスイッチ|
|-----------|--------------------------|
|**d**|Debug.ListMemory|
|**da**|Debug.ListMemory /Ansi|
|**db**|Debug.ListMemory /Format:OneByte|
|**dc**|Debug.ListMemory /Format:FourBytes /Ansi|
|**dd**|Debug.ListMemory /Format:FourBytes|
|**df**|Debug.ListMemory /Format:Float|
|**dq**|Debug.ListMemory /Format:EightBytes|
|**du**|Debug.ListMemory /Unicode|

## <a name="example"></a>例

```
>Debug.ListMemory /Format:float /Count:30 /Unicode
```

## <a name="see-also"></a>関連項目
 [呼び出し履歴の一覧表示コマンド](../../ide/reference/list-call-stack-command.md)[一覧のスレッドコマンド](../../ide/reference/list-threads-command.md) [visual studio コマンド](../../ide/reference/visual-studio-commands.md)[コマンドウィンドウ](../../ide/reference/command-window.md)の[検索/コマンドボックス](../../ide/find-command-box.md) [visual studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)
