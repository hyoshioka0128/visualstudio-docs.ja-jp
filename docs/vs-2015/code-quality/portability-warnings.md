---
title: 移植性に関する警告 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.PortabilityRules
helpviewer_keywords:
- portability warnings
- managed code analysis warnings, portability warnings
- warnings, portability
ms.assetid: 902e859a-2153-4970-baaa-8a5b4a11806f
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 932474143b4770e81d8bfca14ab05a6538ae84a8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72671169"
---
# <a name="portability-warnings"></a>移植性に関する警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

移植性の警告は、異なるオペレーティングシステム間での移植性をサポートします。

## <a name="in-this-section"></a>このセクションの内容

|ルール|説明|
|----------|-----------------|
|[CA1900:値型フィールドはポータブルでなければなりません](../code-quality/ca1900-value-type-fields-should-be-portable.md)|この規則では、明示的なレイアウト属性を使用して宣言された構造体が、64ビットオペレーティングシステム上のアンマネージコードにマーシャリングされるときに正しく配置されることを確認します。|
|[CA1901: P/Invoke 宣言はポータブルでなければなりません](../code-quality/ca1901-p-invoke-declarations-should-be-portable.md)|このルールは、P/Invoke の各パラメーターと戻り値のサイズを評価し、32ビットおよび64ビットのオペレーティングシステムでアンマネージコードにマーシャリングされたときに、そのサイズが正しいことを確認します。|
|[CA1903:対象のフレームワークから API のみを使用します](../code-quality/ca1903-use-only-api-from-targeted-framework.md)|メンバーまたは型が、プロジェクトの対象のフレームワークに含まれていない Service Pack で導入されたメンバーまたは型を使用しています。|
