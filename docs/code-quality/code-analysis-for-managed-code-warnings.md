---
title: マネージド コードの警告に対応するコードの解析
ms.date: 08/31/2020
ms.topic: reference
f1_keywords:
- vc.project.vcfxcoptool.enablefxcop
helpviewer_keywords:
- managed code analyis, warnings
- warnings, managed code analysis
- managed code analysis warnings
- code analysis,managed code
ms.assetid: 3c2741ff-0d3a-42e6-acd5-d42310bd03c4
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 77428bfc815a963e8fae4ddae5e5e7a7b7d991fe
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90034105"
---
# <a name="net-code-analysis-rules"></a>.NET コード分析規則
.NET コード分析では、コード品質違反やコード品質向上の提案を示すルールが提供されます。 ルールは、設計、ローカライズ、パフォーマンス、セキュリティなどのルール領域に分類されます。 特定の規則は .NET API の使用に固有であり、残りの規則は汎用コードの品質に関するものです。 ここでは、各ルールの詳細な説明と例を示します。

 次の表は、診断ごとに提供される情報の種類を示しています。

|項目|説明|
|----------|-----------------|
|Type|規則の TypeName。|
|CheckId|規則の一意の識別子。 CheckId とカテゴリは、ソース内で警告の省略表記として使用されます。|
|カテゴリ|警告のカテゴリ。|
|互換性に影響する変更点|規則違反を修正することが、互換性に影響する変更点かどうかを示します。 互換性に影響する変更点とは、違反の原因となった対象に対して依存関係を持つアセンブリが、新たに修正したバージョンで再コンパイルされないこと、または変更によって実行時にエラーになる可能性があることを示します。 複数の修正プログラムが利用可能であり、少なくとも1つの修正プログラムが互換性に影響する変更であり、1つの修正が行われていない場合は、"中断" と "非互換性" の両方が指定されます。|
|原因|規則に従って警告が生成される原因になった特定のマネージド コード。|
|説明|警告の背景にある問題について説明します。|
|違反の修正方法|規則に適合し、警告が生成されないようにソース コードを変更する方法について説明します。|
|警告を抑制する状況|規則による警告を抑制しても安全な場合について説明します。|
|コード例|規則に違反する例と、規則に適合する修正した例を示します。|
|関連する警告|関連する警告。|

## <a name="in-this-section"></a>このセクションの内容

|カテゴリ|説明|
|-|-|
|[ID によるルール](../code-quality/code-analysis-warnings-for-managed-code-by-checkid.md)|RuleID によってすべてのルールを一覧表示します。|
|[[デザイン規則]](../code-quality/design-warnings.md)|.NET デザインガイドラインによって指定された正しいライブラリデザインをサポートする規則。|
|[ドキュメントルール](../code-quality/documentation-warnings.md)|XML ドキュメントのコメントを適切に使用して、適切にドキュメント化されたライブラリデザインをサポートするルール。|
|[[グローバリゼーション規則]](../code-quality/globalization-warnings.md)|国際対応ライブラリおよびアプリケーションをサポートするルール。|
|[[保守容易性の規則]](../code-quality/maintainability-warnings.md)|ライブラリとアプリケーションのメンテナンスをサポートするルール。|
|[名前付け規則](../code-quality/naming-warnings.md)|.NET デザインガイドラインの名前付け規則への準拠をサポートする規則。|
|[パフォーマンス ルール](../code-quality/performance-warnings.md)|高パフォーマンスのライブラリとアプリケーションをサポートするルール。|
|[移植性と相互運用性の規則](../code-quality/interoperability-warnings.md)|さまざまなプラットフォーム間の移植性と COM クライアントとの相互作用をサポートする規則。|
|[規則の発行](../code-quality/publish-warnings.md)|.NET アプリケーションの適切な発行をサポートする規則。|
|[信頼性の規則](../code-quality/reliability-warnings.md)|メモリやスレッドの適切な使用など、ライブラリとアプリケーションの信頼性をサポートする規則。|
|[セキュリティ規則](../code-quality/security-warnings.md)|より安全なライブラリとアプリケーションをサポートする規則。|
|[使用規則](../code-quality/usage-warnings.md)|.NET の適切な使用をサポートする規則。|
