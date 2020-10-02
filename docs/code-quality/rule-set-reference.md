---
title: コード分析規則セットの参照
ms.date: 04/04/2018
ms.topic: reference
helpviewer_keywords:
- code analysis, rule sets reference
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2b20974d2e44661ed7f4a0288ecb9eff82b2035a
ms.sourcegitcommit: c025a5e2013c4955ca685092b13e887ce64aaf64
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2020
ms.locfileid: "91658426"
---
# <a name="code-analysis-rule-set-reference"></a>コード分析規則セットの参照

Visual Studio でマネージコードプロジェクトのレガシ分析を構成する場合は、組み込みの *規則セット*の一覧から選択できます。 規則によっては、組み込みの規則セットのうちの1つ以上に含まれるものがあります。たとえば、"基本正確性規則" 規則セットには、"マネージ推奨規則" 規則セット内の規則が含まれます。

> [!NOTE]
> このセクションのルールセットは、従来の分析に関連しています。 コードアナライザーパッケージで使用できる規則セットの詳細については、「 [コードアナライザーでの規則セットの使用](/dotnet/fundamentals/code-analysis/code-quality-rule-options)」を参照してください。

これらの組み込みの規則セットのいずれかを使用することも、プロジェクトの要件に合わせて [規則セットをカスタマイズ](../code-quality/how-to-create-a-custom-rule-set.md) することもできます。 カスタム規則セットに同じ規則を含む複数の規則セットを含めると、その規則はカスタム規則セットに1回だけ表示されます。

このセクションのトピックでは、組み込みの規則セットとそれらに含まれる規則 (または警告) について説明します。

| 規則セット | 含まれる規則 |
| - | - |
| [すべての規則](all-rules-rule-set.md) | すべての使用可能なマネージおよび C++ 規則を含みます |
| [基本正確性規則](basic-correctness-rules-rule-set-for-managed-code.md) | マネージ推奨規則と、ロジックエラーとフレームワークの使用に関する規則が含まれます。 |
| [拡張正確性規則](extended-correctness-rules-rule-set-for-managed-code.md) | 基本的な正確性規則 (マネージ推奨規則を含む) に加えて、ロジックエラーとフレームワークの使用に関する規則が追加されます。 |
| [基本デザイン ガイドライン規則](basic-design-guideline-rules-rule-set-for-managed-code.md) | マネージ推奨規則と、コードの読み取り、理解、保守を容易にするための規則が含まれています。 |
| [拡張デザイン ガイドライン規則](extended-design-guidelines-rules-rule-set-for-managed-code.md) | 基本的な設計ガイドライン規則 (推奨されるマネージ規則を含む) に加えて、名前付けに重点を置いた保守容易性の規則が含まれています。 |
| [グローバリゼーションルール](globalization-rules-rule-set-for-managed-code.md) | グローバリゼーションの問題に関する規則が含まれています |
| [マネージド最小規則](managed-minimum-rules-rule-set-for-managed-code.md) | 重大なマネージコードの問題に対して4つの規則が含まれています |
| [マネージド推奨規則](managed-recommended-rules-rule-set-for-managed-code.md) | マネージ最小規則に加えて、重大なマネージコードの問題に関する規則を追加します。 |
| [混合最小規則](mixed-minimum-rules-rule-set.md) | CLR の C++ コードでの重大な問題に関する規則が含まれています |
| [混合推奨規則](mixed-recommended-rules-rule-set.md) | CLR の C++ コードでの、混合最小ルールと重大な問題に対するルールの追加が含まれます。 |
| [ネイティブ最小規則](native-minimum-rules-rule-set.md) | ネイティブコードでの重大な問題に関する規則が含まれています |
| [ネイティブ推奨規則](native-recommended-rules-rule-set.md) | ネイティブの最小規則に加え、ネイティブコードの重大な問題に関する規則が追加されます。 |
| [セキュリティ規則](security-rules-rule-set-for-managed-code.md) | セキュリティの脆弱性を検出するための規則が含まれています |
