---
title: コンカレンシー名前空間 (コンカレンシー ビジュアライザー) | Microsoft Docs
description: C++ で同時実行プログラムを作成するには、コンカレンシー名前空間を使用します。これにより、C++ のコンカレンシー フレームワークである同時実行ランタイムにアクセスできるようになります。
custom.ms: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- cvmarkersobj/Concurrency
helpviewer_keywords:
- Concurrency namespace
ms.assetid: 001fbfce-a278-4502-aa27-26d65dd61453
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bdb9f2cee62c126f7a8b91fb7be57f558c9a7e5c
ms.sourcegitcommit: 7a5c4f60667b5792f876953d55192b49a73f5fe9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2021
ms.locfileid: "98533434"
---
# <a name="concurrency-namespace-concurrency-visualizer"></a>コンカレンシー名前空間 (コンカレンシー ビジュアライザー)
`Concurrency` 名前空間には、C++ 向けの並列プログラミング フレームワークであるコンカレンシー ランタイムにアクセスするためのクラスおよび関数が用意されています。 詳細については、「[コンカレンシー ランタイム](/cpp/parallel/concrt/concurrency-runtime)」を参照してください。

## <a name="syntax"></a>構文

```cpp
namespace Concurrency;
```

## <a name="members"></a>メンバー

### <a name="namespaces"></a>名前空間

|名前|[説明]|
|----------|-----------------|
|[diagnostic 名前空間](../profiling/diagnostic-namespace.md)|`diagnostics` 名前空間は、コンカレンシー ビジュアライザー マーカーを出力するための機能を提供します。|

## <a name="requirements"></a>必要条件
 **ヘッダー:** cvmarkersobj.h

## <a name="see-also"></a>関連項目
- [C ライブラリ リファレンス](../profiling/c-library-reference.md)