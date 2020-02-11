---
title: 移植性に関する警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.PortabilityRules
helpviewer_keywords:
- portability warnings
- managed code analysis warnings, portability warnings
- warnings, portability
ms.assetid: 902e859a-2153-4970-baaa-8a5b4a11806f
author: jillre
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 61efbc2022b2c0cd60e005936e148bbaf1d900a4
ms.sourcegitcommit: 00ba14d9c20224319a5e93dfc1e0d48d643a5fcd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2020
ms.locfileid: "77091731"
---
# <a name="portability-warnings"></a>移植性に関する警告
移植性の警告は、異なるオペレーティングシステム間での移植性をサポートします。

## <a name="in-this-section"></a>このセクションの内容

|Rule|説明|
|----------|-----------------|
|[CA1900: 値型フィールドはポータブルでなければなりません](../code-quality/ca1900.md)|この規則では、明示的なレイアウト属性を使用して宣言された構造体が、64ビットオペレーティングシステム上のアンマネージコードにマーシャリングされるときに正しく配置されることを確認します。|
|[CA1901: P/Invoke 宣言はポータブルでなければなりません](../code-quality/ca1901.md)|このルールは、P/Invoke の各パラメーターと戻り値のサイズを評価し、32ビットおよび64ビットのオペレーティングシステムでアンマネージコードにマーシャリングされたときに、そのサイズが正しいことを確認します。|
|[CA1903: 対象のフレームワークから API のみを使用します](../code-quality/ca1903.md)|メンバーまたは型が、プロジェクトの対象のフレームワークに含まれていない Service Pack で導入されたメンバーまたは型を使用しています。|
