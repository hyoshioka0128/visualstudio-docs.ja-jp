---
title: GoTo コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- edit.goto
helpviewer_keywords:
- Debug.Goto command
- Go To command
ms.assetid: 201e1dd2-6701-467d-8cc1-faec2ef20511
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 454b51b6939a78cdaab8d29f51d30910024adbe3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661202"
---
# <a name="go-to-command"></a>GoTo コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定した行にカーソルを移動します。

## <a name="syntax"></a>構文

```
Edit.GoTo [linenumber]
```

## <a name="arguments"></a>引数
 `linenumber` 省略可能。 移動先の行番号を表す整数。

## <a name="remarks"></a>解説
 行番号は 1 から始まります。 `linenumber` の値が 1 未満の場合は、最初の行が表示されます。 `linenumber` の値が最終行の値より大きい場合は、最後の行が表示されます。

 `linenumber` の値が指定されていない場合は、 **[指定行へ移動]** ダイアログ ボックスが表示されます。

 このコマンドのエイリアスは GoToLn です。

## <a name="example"></a>例

```
>Edit.GoTo 125
```

## <a name="see-also"></a>関連項目
 [Visual Studio コマンド](../../ide/reference/visual-studio-commands.md)の[コマンドウィンドウ](../../ide/reference/command-window.md)の[検索/コマンドボックス](../../ide/find-command-box.md) [visual studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)
