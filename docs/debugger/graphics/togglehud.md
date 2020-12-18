---
title: ToggleHUD | Microsoft Docs
description: VsgDbg の ToggleHUD() メソッドを使用して、アプリの実行時にグラフィックス診断のヘッドアップ ディスプレイ (HUD) を表示するかどうかを切り替えます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7261e01d-3c72-46ce-9fb3-5f33b2ddb901
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 60bee5a89be0fc1503595a36cfc48a692711d40a
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96996072"
---
# <a name="togglehud"></a>ToggleHUD
グラフィックス診断の *HUD* (ヘッドアップ ディスプレイ) オーバーレイのオンとオフを切り替えます。

## <a name="syntax"></a>構文

```C++
void ToggleHUD();
```

## <a name="remarks"></a>Remarks
 グラフィックス診断の HUD は、グラフィック診断で実行されているアプリケーションの左上隅に表示されます。 これには、アプリとグラフィックス情報キャプチャのランタイム情報、[AddMessage](addmessage.md) メンバー関数の呼び出しによって追加されたメッセージが表示されます。

 HUD を切り替えるには、アクティブにグラフィックス情報をキャプチャする必要はありません。これは、`VsgDbg` クラスのインスタンスを通じて切り替えられますが、[Init](init.md) メンバー関数は最初に呼び出される必要はありません。