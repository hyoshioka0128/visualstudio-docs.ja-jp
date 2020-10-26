---
title: span::span コンストラクター | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- cvmarkersobj/Concurrency::diagnostic::span::span
helpviewer_keywords:
- Concurrency::diagnostic::span constructor
ms.assetid: 8b5578aa-5e5c-4ac7-87c7-ce87c4246e2c
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: df6df731de90a9aad9e6cc637b3f218e481b66b7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198294"
---
# <a name="spanspan-constructor"></a>span::span コンストラクター

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`span` クラスの新しいインスタンスを初期化します。

## <a name="syntax"></a>構文

```
span(
   const marker_series& _Series,
   _In_ LPCTSTR _Format,
   ...
);
span(
   const marker_series& _Series,
   marker_importance _Importance,
   _In_ LPCTSTR _Format,
   ...
);
span(
   const marker_series& _Series,
   int _Category,
   _In_ LPCTSTR _Format,
   ...
);
span(
   const marker_series& _Series,
   marker_importance _Importance,
   int _Category,
   _In_ LPCTSTR _Format,
   ...
);
```

#### <a name="parameters"></a>パラメーター

`_Series` 有効なマーカー シリーズ コンテキスト。

`_Format` 0 個以上の書式項目が混在したテキストを含む複合書式指定文字列。各書式項目は、引数リスト内のオブジェクトに対応します。

`_Importance` 重要度レベル。

`_Category` カテゴリ。

## <a name="requirements"></a>必要条件

**ヘッダー:** cvmarkersobj.h

**名前空間:** Concurrency::diagnostic

## <a name="see-also"></a>参照

[span クラス](../profiling/span-class.md)
