---
title: FxCop コード分析 (バイナリ分析) と .NET アナライザー (ソース分析)
ms.date: 09/06/2018
description: Visual Studio でのレガシ FxCop (バイナリ分析) と .NET アナライザー (ソース分析) の違いについて説明します。 これらのアナライザーの使用方法に関する質問への回答を参照してください。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- code analysis FAQ
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: d581ef60ebfe9ff5aeceae4c16ee4294eae5d850
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96112178"
---
# <a name="frequently-asked-questions-about-legacy-fxcop-and-net-analyzers"></a>レガシ FxCop と .NET アナライザーに関してよく寄せられる質問

レガシ FxCop (バイナリ分析) と .NET アナライザー (ソース分析) の違いを理解することは、少し紛らわしいかもしれません。 この記事は、ユーザーの方々がお持ちの質問を解決することを意図しています。

## <a name="whats-the-difference-between-legacy-fxcop-and-net-analyzers"></a>レガシ FxCop と .NET アナライザーの違いは何ですか。

従来の FxCop は、コンパイル済みのアセンブリ上でビルド後の分析を実行します。 これは、**FxCopCmd.exe** という別の実行可能ファイルとして実行されます。 FxCopCmd.exe はコンパイル済みのアセンブリを読み込み、コード分析を実行し、結果 (または *診断*) を報告します。

.NET アナライザーは、.NET Compiler Platform ("Roslyn") に基づいています。 .NET SDK から有効にするか、プロジェクトまたはソリューションによって参照される [NuGet パッケージとしてインストール](install-net-analyzers.md) します。 アナライザーは、コンパイラの実行中にソースコードに基づく分析を実行します。 アナライザーは **csc.exe** または **vbc.exe** のいずれかのコンパイラプロセス内でホストされ、プロジェクトのビルド時に分析を実行します。 アナライザーの結果は、コンパイラーの結果と共に報告されます。

## <a name="whats-the-difference-between-fxcop-analyzers-and-net-analyzers"></a>FxCop アナライザーと .NET アナライザーの違いは何ですか。

FxCop アナライザーと .NET アナライザーはどちらも、FxCop CA 規則の .NET Compiler Platform ("Roslyn") アナライザーの実装を参照します。 Visual Studio 2019 16.8 と .NET 5.0 より前のリリースでは、これらのアナライザーは NuGet パッケージとして出荷さ `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)れています。 Visual Studio 2019 16.8 と .NET 5.0 以降、これらのアナライザーは [.NET SDK に含まれて](/dotnet/fundamentals/code-analysis/overview)います。 また、NuGet パッケージとして入手することもでき `Microsoft.CodeAnalysis.NetAnalyzers` [NuGet package](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)ます。 [FxCop アナライザーから .net analyzer に移行することを](migrate-from-fxcop-analyzers-to-net-analyzers.md)検討してください。

## <a name="does-the-run-code-analysis-command-run-net-analyzers"></a>[コード分析の実行] コマンドで .NET アナライザーを実行しますか?

Visual Studio 2019 16.5 リリースより前のバージョンでは、[実行コード分析の **分析**] を選択すると  >  **Run Code Analysis**、従来の分析が実行されます。 Visual Studio 2019 16.5 を起動し、[ **コード分析の実行** ] メニューオプションを選択すると、選択したプロジェクトまたはソリューションに対して Roslyn ベースのアナライザーが実行されます。 .NET アナライザーがインストールされている場合は、それらも実行されます。 詳細については、「 [方法: マネージコードのコード分析を手動で実行する](how-to-run-code-analysis-manually-for-managed-code.md)」を参照してください。

## <a name="does-the-runcodeanalysis-msbuild-project-property-run-analyzers"></a>RunCodeAnalysis msbuild プロジェクト プロパティはアナライザーを実行しますか?

いいえ。 (たとえば *.csproj* の) プロジェクト ファイル内の **RunCodeAnalysis** プロパティは、従来の FxCop を実行するためのみに使用します。 これは、**FxCopCmd.exe** を起動するビルド後の msbuild タスクを実行します。

## <a name="so-how-do-i-run-net-analyzers-then"></a>では、.NET アナライザーを実行するにはどうすればよいでしょうか。

.NET アナライザーを実行するには、最初に [.NET SDK から有効にするか、NuGet パッケージとしてインストール](install-net-analyzers.md)します。 次いでプロジェクトまたはソリューションを Visual Studio または msbuild を使用してビルドします。 Roslyn アナライザーによって生成される警告とエラーは、 **エラー一覧** またはコマンドウィンドウに表示されます。

## <a name="i-get-warning-ca0507-even-after-ive-installed-the-net-analyzers-nuget-package"></a>.NET analyzer NuGet パッケージをインストールした後でも警告 CA0507 が表示される

.NET analyzer がインストールされているにもかかわらず、警告が引き続き表示 **される場合は、ビルド中に実行される FxCop アナライザーを優先して、"コード分析の実行" が非推奨** となりました。[プロジェクトファイル](../ide/solutions-and-projects-in-visual-studio.md#project-file)の **runcodeanalysis** msbuild プロパティを **false** に設定する必要がある場合があります。 それ以外の場合、レガシ分析は各ビルドの後に実行されます。

```xml
<RunCodeAnalysis>false</RunCodeAnalysis>
```

## <a name="which-rules-have-been-ported-to-net-analyzers"></a>どのルールが .NET analyzer に移植されていますか?

.NET アナライザーに移植された従来の分析規則の詳細については、「 [Fxcop rule port status](fxcop-rule-port-status.md)」を参照してください。

## <a name="code-analysis-warnings-are-treated-as-errors"></a>コード分析の警告はエラーとして扱われます

プロジェクトで [ビルド] オプションを使用して警告をエラーとして扱う場合、アナライザーの警告がエラーとして表示されることがあります。 コード分析の警告がエラーとして扱われないようにするには、「 [コード分析](../code-quality/analyzers-faq.md#treat-warnings-as-errors)に関する FAQ」の手順に従います。

## <a name="see-also"></a>関連項目

- [.NET Compiler Platform アナライザーの概要](roslyn-analyzers-overview.md)
- [.NET アナライザーへの移行](migrate-from-legacy-analysis-to-net-analyzers.md)
- [.NET アナライザーのインストール](install-net-analyzers.md)
