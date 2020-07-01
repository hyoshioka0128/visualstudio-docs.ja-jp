---
title: diagnostic 名前空間 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkersobj/Concurrency, diagnostic
helpviewer_keywords:
- Concurrency, diagnostic namespace
ms.assetid: ad786b19-7c4c-46ee-bfb6-c4752b373a09
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 680d304a8e4d21365d82f654265ae2f34582b636
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330263"
---
# <a name="diagnostic-namespace"></a>diagnostic 名前空間
`diagnostics` 名前空間は、コンカレンシー ビジュアライザー マーカーを出力するための機能を提供します。

## <a name="syntax"></a>構文

```cpp
namespace diagnostic;
```

## <a name="members"></a>メンバー

### <a name="classes"></a>クラス

|名前|説明|
|----------|-----------------|
|[marker_series クラス](../profiling/marker-series-class.md)|1 つのプロバイダーによって生成されたイベントのシリアル チャネルを表します。|
|[span クラス](../profiling/span-class.md)|アプリケーションのフェーズを定義します。|

### <a name="enumerations"></a>列挙

|名前|説明|
|----------|-----------------|
|[marker_importance 列挙型](../profiling/marker-importance-enumeration.md)|コンカレンシー ビジュアライザー マーカーの重要度レベルを表します。|

## <a name="requirements"></a>必要条件
 **ヘッダー:** *cvmarkersobj.h*

 **名前空間:** コンカレンシー

## <a name="see-also"></a>関連項目
- [コンカレンシー名前空間 (コンカレンシー ビジュアライザー)](../profiling/concurrency-namespace-concurrency-visualizer.md)