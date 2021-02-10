---
title: marker_importance 列挙型 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkersobj/Concurrency, diagnostic::marker_importance
helpviewer_keywords:
- Concurrency, diagnostic::marker_importance enumeration
ms.assetid: d5524ea0-0227-4d8e-9122-332291042df5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f1559dc6c5aa24c54465aee6d29f0745be6c897c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99917819"
---
# <a name="marker_importance-enumeration"></a>marker_importance 列挙型
コンカレンシー ビジュアライザー マーカーの重要度レベルを表します。

## <a name="syntax"></a>構文

```cpp
enum marker_importance;
```

## <a name="members"></a>メンバー

### <a name="values"></a>値

|名前|説明|
|----------|-----------------|
|`critical_importance`|マーカーの重要度がきわめて高いことを指定します。|
|`high_importance`|マーカーの重要度が高いことを指定します。|
|`low_importance`|マーカーの重要度が低いことを指定します。|
|`normal_importance`|マーカーの重要度が標準であることを指定します。|

## <a name="requirements"></a>必要条件
 **ヘッダー:** *cvmarkersobj.h*

 **名前空間:** Concurrency::diagnostic

## <a name="see-also"></a>関連項目
- [diagnostic 名前空間](../profiling/diagnostic-namespace.md)