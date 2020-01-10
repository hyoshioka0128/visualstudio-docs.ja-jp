---
title: マネージド コードの警告に対応するコードの解析
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vc.project.vcfxcoptool.enablefxcop
helpviewer_keywords:
- managed code analyis, warnings
- warnings, managed code analysis
- managed code analysis warnings
- code analysis,managed code
ms.assetid: 3c2741ff-0d3a-42e6-acd5-d42310bd03c4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: d18763f3638442de4e0142204d696ee13b1bdb19
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75587772"
---
# <a name="code-analysis-for-managed-code-warnings"></a>マネージド コードの警告に対応するコードの解析
マネージド コード分析ツールには、マネージド コード ライブラリの規則違反を示す警告機能があります。 警告は、デザイン、ローカリゼーション、パフォーマンス、セキュリティなどの規則の区分に分類されています。 個々の警告によって、マネージド コード分析規則の違反がわかります。 ここでは、マネージド コード分析の各警告について、詳細な説明と例を紹介します。

 次の表に、各警告で示される情報の種類を示しています。

|項目|説明|
|----------|-----------------|
|の型|規則の TypeName。|
|CheckId|規則の一意の識別子。 CheckId とカテゴリは、ソース内で警告の省略表記として使用されます。|
|[カテゴリ]|警告のカテゴリ。|
|互換性に影響する変更点|規則違反を修正することが、互換性に影響する変更点かどうかを示します。 互換性に影響する変更点とは、違反の原因となった対象に対して依存関係を持つアセンブリが、新たに修正したバージョンで再コンパイルされないこと、または変更によって実行時にエラーになる可能性があることを示します。 複数の修正プログラムが利用可能であり、少なくとも1つの修正プログラムが互換性に影響する変更であり、1つの修正が行われていない場合は、"中断" と "非互換性" の両方が指定されます。|
|原因|規則に従って警告が生成される原因になった特定のマネージド コード。|
|説明|警告の背景にある問題について説明します。|
|違反の修正方法|規則に適合し、警告が生成されないようにソース コードを変更する方法について説明します。|
|警告を抑制する状況|規則による警告を抑制しても安全な場合について説明します。|
|コードの例|規則に違反する例と、規則に適合する修正した例を示します。|
|関連する警告|関連する警告。|

## <a name="in-this-section"></a>このセクションの内容

|||
|-|-|
|[警告 (CheckId 別)](../code-quality/code-analysis-warnings-for-managed-code-by-checkid.md)|すべての警告を CheckId 別に一覧表示します。|
|[暗号化警告](../code-quality/cryptography-warnings.md)|暗号化の適切な使用によって、より安全なライブラリとアプリケーションをサポートする警告です。|
|[デザインの警告](../code-quality/design-warnings.md)|.NET デザインガイドラインによって指定された正しいライブラリデザインをサポートする警告。|
|[ドキュメントの警告](../code-quality/documentation-warnings.md)|XML ドキュメントコメントの正しい使用によって、適切にドキュメント化されたライブラリデザインをサポートする警告。|
|[グローバリゼーションに関する警告](../code-quality/globalization-warnings.md)|国際対応ライブラリおよびアプリケーションをサポートする警告です。|
|[相互運用性の警告](../code-quality/interoperability-warnings.md)|COM クライアントとの相互作用をサポートする警告です。|
|[保守性の警告](../code-quality/maintainability-warnings.md)|ライブラリとアプリケーションの保守をサポートする警告です。|
|[モビリティの警告](../code-quality/mobility-warnings.md)|効率的な電力の使用法をサポートする警告です。|
|[名前付けに関する警告](../code-quality/naming-warnings.md)|.NET デザインガイドラインの名前付け規則への準拠をサポートする警告。|
|[パフォーマンスに関する警告](../code-quality/performance-warnings.md)|高パフォーマンスのライブラリとアプリケーションをサポートする警告です。|
|[Portability Warnings](../code-quality/portability-warnings.md)|異なるプラットフォーム間の移植性をサポートする警告です。|
|[信頼性の警告](../code-quality/reliability-warnings.md)|メモリやスレッドの適切な使用など、ライブラリとアプリケーションの信頼性をサポートする警告です。|
|[セキュリティの警告](../code-quality/security-warnings.md)|より安全なライブラリとアプリケーションをサポートする警告です。|
|[使用法に関する警告](../code-quality/usage-warnings.md)|.NET の適切な使用をサポートする警告。|
|[Code Analysis Policy Errors](../code-quality/code-analysis-policy-errors.md)|チェックインにおいてコード分析ポリシーに適合しない場合に発生するエラーです。|
