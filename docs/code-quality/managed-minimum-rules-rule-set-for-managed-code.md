---
title: マネージド コードの "マネージ最小規則" 規則セット
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 44a50c54-8dd3-42b2-8387-532a150e5a6c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 903b464172d541277de5fbac6d8ab035578b6154
ms.sourcegitcommit: c025a5e2013c4955ca685092b13e887ce64aaf64
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2020
ms.locfileid: "91658504"
---
# <a name="managed-minimum-rules-rule-set-for-managed-code"></a>マネージド コードの "マネージ最小規則" 規則セット

マネージ最小規則は、潜在的なセキュリティホール、アプリケーションのクラッシュ、その他の重要な論理エラーやデザインエラーなど、コードの最も重大な問題に焦点を当てています。 この規則セットは、プロジェクト用に作成するカスタム規則セットに含めます。

|ルール|説明|
|----------|-----------------|
|[CA1001](/dotnet/fundamentals/code-analysis/quality-rules/ca1001)|破棄可能なフィールドを所有する型は、破棄可能でなければなりません|
|[CA1821](/dotnet/fundamentals/code-analysis/quality-rules/ca1821)|空のファイナライザーを削除します|
|[CA2213](/dotnet/fundamentals/code-analysis/quality-rules/ca2213)|破棄可能なフィールドは破棄されなければなりません|
|[CA2231](/dotnet/fundamentals/code-analysis/quality-rules/ca2231)|オーバーライド時に演算子 equals をオーバーロードします `ValueType.Equals`|
