---
title: span クラス | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- cvmarkersobj/Concurrency::diagnostic::span
helpviewer_keywords:
- Concurrency::diagnostic::span class
ms.assetid: 527826a8-2590-43ad-b907-7bc0b7288e92
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8d8f31d24dc6c6c2ea20b50c9bf8af1cb4a9f9af
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "62979758"
---
# <a name="span-class"></a>span クラス
アプリケーションのフェーズを定義します。

## <a name="syntax"></a>構文

```cpp
class span;
```

## <a name="members"></a>メンバー

### <a name="public-constructors"></a>パブリック コンストラクター

|名前|説明|
|----------|-----------------|
|[span::span コンストラクター](../profiling/span-span-constructor.md)|`span` クラスの新しいインスタンスを初期化します。|
|[span::~span デストラクター](../profiling/span-tilde-span-destructor.md)|`span` オブジェクトを破棄し、そのリソースを解放します。|

## <a name="inheritance-hierarchy"></a>継承階層
 `span`

## <a name="requirements"></a>必要条件
 **ヘッダー:** *cvmarkersobj.h*

 **名前空間:** Concurrency::diagnostic

## <a name="see-also"></a>関連項目
- [diagnostic 名前空間](../profiling/diagnostic-namespace.md)