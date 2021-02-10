---
title: DA0011 - CompareTo の負荷が高くなっています | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.DA0011
- vs.performance.rules.DAExpensiveCompareTo
- vs.performance.11
- vs.performance.rules.DA0011
ms.assetid: 239a381d-0d97-4367-8668-746c93f5af2c
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: aef8135e48b07946803832266ed9dff9e843d3ca
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99916826"
---
# <a name="da0011-expensive-compareto"></a>DA0011:CompareTo の負荷が高くなっています

|アイテム|[値]|
|-|-|
|規則 ID|DA0011|
|カテゴリ|.NET Framework の使用|
|プロファイル方法|サンプリング<br /><br /> .NET メモリ|
|メッセージ|CompareTo 関数の負荷を抑える必要があります。メモリを割り当てることはできません。 可能な場合は、CompareTo 関数の複雑さを軽減してください。|
|規則の種類|警告|

## <a name="cause"></a>原因
 型の CompareTo メソッドが高コストであるか、またはメモリを割り当てています。

## <a name="rule-description"></a>規則の説明
 CompareTo メソッドは効率的にする必要があります。メモリを割り当てることはできません。

## <a name="how-to-fix-violations"></a>違反の修正方法
 CompareTo メソッドの複雑さを軽減してください。
