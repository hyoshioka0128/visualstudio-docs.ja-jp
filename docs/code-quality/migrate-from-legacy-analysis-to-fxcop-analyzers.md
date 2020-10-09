---
title: FxCop からソース分析への移行 (FxCop アナライザー)
ms.custom: SEO-VS-2020
description: コードを初めて分析する方法、またはバイナリ分析 (FxCop) から、ソース分析 (FxCop アナライザー) を使用してマネージコードを分析する新しい方法に移行する方法について説明します。
ms.date: 03/06/2020
ms.topic: conceptual
f1_keywords:
- vs.projectpropertypages.codeanalysis
helpviewer_keywords:
- FxCop, migration
- legacy analysis, migration
- source code analysis, migration
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cb75b7374e7f88f4643a5ecc4a9c193d8144efc4
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91860475"
---
# <a name="migrate-from-legacy-analysis-fxcop-to-source-analysis-fxcop-analyzers"></a>レガシ分析 (FxCop) からソース分析への移行 (FxCop アナライザー)

.NET Compiler Platform によるソース分析 ("Roslyn") アナライザーは、マネージコードの [従来の分析](../code-quality/code-analysis-for-managed-code-overview.md) に代わるものです。 .NET Core や .NET Standard プロジェクトなどの新しいプロジェクトテンプレートでは、レガシ分析は使用できません。

従来の分析 (FxCop) 規則の多くは、FxCop アナライザー (Roslyn コードアナライザーのセット) に対して既に書き直しられています。 FxCop アナライザーは、プロジェクトまたはソリューションによって参照される [NuGet パッケージとしてインストール](install-fxcop-analyzers.md#nuget-package) します。 FxCop アナライザーは、コンパイラーの実行中にソースコードに基づく分析を実行します。 アナライザーの結果は、コンパイラーの結果と共に報告されます。

レガシ分析とソース分析の相違点の詳細については、次を参照してください。

- [ソース コード分析と従来の分析](../code-quality/fxcop-analyzers-faq.md#whats-the-difference-between-legacy-fxcop-and-fxcop-analyzers)

- [FxCop アナライザーに関する FAQ](../code-quality/fxcop-analyzers-faq.md)

ソース分析に移行するには、 [FxCop アナライザーをインストール](../code-quality/install-fxcop-analyzers.md)します。 従来の分析のルール違反と同様に、ソース コード分析の違反は Visual Studio の [エラー一覧] ウィンドウに表示されます。 さらに、ソース コード分析の違反は、コード エディターで問題のあるコードの下に "*波線*" としても示されます。 波線の色は、ルールの[重要度設定](../code-quality/use-roslyn-analyzers.md#configure-severity-levels)によって異なります。 新しい FxCop アナライザーに移植された規則の状態を確認するには、「移植された [規則およびアン移植](../code-quality/fxcop-rule-port-status.md)された規則」を参照してください。

FxCop アナライザーの構成方法の詳細については、次を参照してください。

- FxCop アナライザーを構成するには、「 [fxcop アナライザーの構成](/dotnet/fundamentals/code-analysis/code-quality-rule-options)」を参照してください。

- EditorConfig またはルールセットファイルで定義済みのルールを使用してアナライザーを構成する方法については、「 [ルールのカテゴリを有効に](/dotnet/fundamentals/code-analysis/code-quality-rule-options)する」を参照してください。
