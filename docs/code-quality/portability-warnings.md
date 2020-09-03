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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f48cef7ffaf08fc26566fdd04bee15a3e3e1b85f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "78167574"
---
# <a name="portability-warnings"></a>移植性に関する警告
移植性の警告は、異なるオペレーティングシステム間での移植性をサポートします。

## <a name="in-this-section"></a>このセクションの内容

|ルール|説明|
|----------|-----------------|
|[CA1900:値型フィールドはポータブルでなければなりません](../code-quality/ca1900.md)|この規則では、明示的なレイアウト属性を使用して宣言された構造体が、64ビットオペレーティングシステム上のアンマネージコードにマーシャリングされるときに正しく配置されることを確認します。|
|[CA1901: P/Invoke 宣言はポータブルでなければなりません](../code-quality/ca1901.md)|このルールは、P/Invoke の各パラメーターと戻り値のサイズを評価し、32ビットおよび64ビットのオペレーティングシステムでアンマネージコードにマーシャリングされたときに、そのサイズが正しいことを確認します。|
|[CA1903:対象のフレームワークから API のみを使用します](../code-quality/ca1903.md)|メンバーまたは型が、プロジェクトの対象のフレームワークに含まれていない Service Pack で導入されたメンバーまたは型を使用しています。|
