---
title: SetCurrentProcess | Microsoft ドキュメント
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Debug.SetCurrentProcess command
- Set Current Process command
ms.assetid: 1e016ebd-aadd-411f-a606-03bf69d3f8aa
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c362d3f5dda5015e91ac88dd8f0abd60a185ba72
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665464"
---
# <a name="set-current-process"></a>SetCurrentProcess
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定されたプロセスをデバッガーでアクティブなプロセスとして設定します。

## <a name="syntax"></a>構文

```
Debug.SetCurrentProcess index
```

## <a name="arguments"></a>引数
 `index` 必須。 プロセスのインデックスです。

## <a name="remarks"></a>解説
 デバッグ中には複数のプロセスにアタッチできますが、デバッガーでアクティブになっているプロセスは常に 1 つだけです。 `SetCurrentProcess` コマンドを使用すると、アクティブなプロセスを設定できます。

## <a name="example"></a>例

```
>Debug.SetCurrentProcess 1
```

## <a name="see-also"></a>関連項目
 [Visual studio](../../ide/reference/visual-studio-commands.md)コマンドの[コマンドウィンドウ](../../ide/reference/command-window.md) [visual studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)
