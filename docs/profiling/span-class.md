---
title: span クラス | Microsoft Docs
description: span クラスと、それを使用してアプリケーションのフェーズを定義する方法について学習します。 また、span クラスのパブリック コンストラクターと継承階層についても説明します。
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
ms.openlocfilehash: 0ca1e674b13877ff8a8864c3b7447f15fd0307d7
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2021
ms.locfileid: "98720047"
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