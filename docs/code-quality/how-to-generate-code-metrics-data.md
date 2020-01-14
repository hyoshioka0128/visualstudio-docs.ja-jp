---
title: IDE またはコマンドラインからコードメトリックスを生成する
ms.date: 11/02/2018
ms.topic: conceptual
helpviewer_keywords:
- code metrics data
- code metrics results
- code metrics [Visual Studio]
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a43f11df65286e25d0ea19990fa56620695e69df
ms.sourcegitcommit: aa302af53de342e75793bd05b10325939dc69b53
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2020
ms.locfileid: "75886444"
---
# <a name="how-to-generate-code-metrics-data"></a>方法: コードメトリックスデータを生成する

コードメトリックスデータは、次の3つの方法で生成できます。

- [FxCop アナライザー](#fxcop-analyzers-code-metrics-rules)をインストールし、それに含まれる4つのコードメトリックス (保守性) ルールを有効にします。

- Visual Studio 内で [ [ **Analyze** > **Calculate Code Metrics** ](#calculate-code-metrics-menu-command) ] メニューコマンドを選択します。

- および Visual Basic プロジェクトの場合C#は、[コマンドライン](#command-line-code-metrics)から実行します。

## <a name="fxcop-analyzers-code-metrics-rules"></a>FxCop アナライザーのコードメトリックス規則

[FxCopAnalyzers NuGet パッケージ](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)には、いくつかのコードメトリックス[アナライザー](roslyn-analyzers-overview.md)の規則が含まれています。

- [CA1501](ca1501-avoid-excessive-inheritance.md)
- [CA1502](ca1502.md)
- [CA1505](ca1505-avoid-unmaintainable-code.md)
- [CA1506](ca1506.md)

これらの規則は既定で無効になっていますが、[**ソリューションエクスプローラー**](use-roslyn-analyzers.md#set-rule-severity-from-solution-explorer)または[規則セット](using-rule-sets-to-group-code-analysis-rules.md)ファイルで有効にすることができます。 たとえば、ルール CA1502 を警告として有効にするために、ルールセットファイルには次のエントリが含まれます。

```xml
<?xml version="1.0" encoding="utf-8"?>
<RuleSet Name="Rules" Description="Rules" ToolsVersion="16.0">
  <Rules AnalyzerId="Microsoft.CodeQuality.Analyzers" RuleNamespace="Microsoft.CodeQuality.Analyzers">
    <Rule Id="CA1502" Action="Warning" />
  </Rules>
</RuleSet>
```

### <a name="configuration"></a>の構成

FxCop アナライザーパッケージのコードメトリックスルールが起動するしきい値を構成できます。

1. テキスト ファイルを作成します。 たとえば、 *CodeMetricsConfig*という名前を付けます。

2. 次の形式で、必要なしきい値をテキストファイルに追加します。

   ```txt
   CA1502: 10
   ```

   この例では、ルール[CA1502](ca1502.md)は、メソッドのサイクロマティック複雑度が10を超える場合に起動するように構成されています。

3. Visual Studio の **[プロパティ]** ウィンドウまたはプロジェクトファイルで、構成ファイルのビルドアクションを[**additionalfiles**](../ide/build-actions.md#build-action-values)としてマークします。 例:

   ```xml
   <ItemGroup>
     <AdditionalFiles Include="CodeMetricsConfig.txt" />
   </ItemGroup>
   ```

## <a name="calculate-code-metrics-menu-command"></a>[コードメトリックスの計算] メニューコマンド

[ **Analyze** > **Calculate code metrics** ] メニューを使用して、IDE で開いているプロジェクトの1つまたはすべてに対してコードメトリックスを生成します。

### <a name="generate-code-metrics-results-for-an-entire-solution"></a>ソリューション全体のコードメトリックスの結果を生成する

ソリューション全体に対するコードメトリックスの結果は、次のいずれかの方法で生成できます。

- メニューバーで、 **[分析]** を選択し、**ソリューションの** **コードメトリックス** > を計算 > ます。

- **ソリューションエクスプローラー**で、ソリューションを右クリックし、 **[コードメトリックスの計算]** をクリックします。

- **[コードメトリックスの結果]** ウィンドウで、 **[ソリューションのコードメトリックスを計算]** する ボタンを選択します。

結果が生成され、 **[コードメトリックスの結果]** ウィンドウが表示されます。 結果の詳細を表示するには、 **[階層]** 列のツリーを展開します。

### <a name="generate-code-metrics-results-for-one-or-more-projects"></a>1つ以上のプロジェクトのコードメトリックスの結果を生成します

1. **ソリューションエクスプローラー**で、1つ以上のプロジェクトを選択します。

1. メニューバーから **[分析]** を選択し、**選択したプロジェクトの** **コードメトリックス** > を計算 > ます。

結果が生成され、 **[コードメトリックスの結果]** ウィンドウが表示されます。 結果の詳細を表示するには、**階層**内のツリーを展開します。

::: moniker range="vs-2017"

> [!NOTE]
> **[コードメトリックスの計算]** コマンドは、.net Core および .NET Standard プロジェクトでは機能しません。 .NET Core または .NET Standard プロジェクトのコードメトリックスを計算するには、次のようにします。
>
> - 代わりに[コマンドライン](#command-line-code-metrics)からコードメトリックスを計算する
>
> - [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)へのアップグレード

::: moniker-end

## <a name="command-line-code-metrics"></a>コマンドラインコードメトリックス

コードメトリックスデータは、のC#コマンドラインから生成できます。また、.NET FRAMEWORK、.net Core、.NET Standard アプリ用のプロジェクトを Visual Basic します。 コマンドラインからコードメトリックスを実行するには、 [Microsoft CodeAnalysis. Metrics NuGet パッケージ](#microsoftcodeanalysismetrics-nuget-package)をインストールするか、手動で[metrics](#metricsexe)実行可能ファイルをビルドします。

### <a name="microsoftcodeanalysismetrics-nuget-package"></a>Microsoft CodeAnalysis. メトリック NuGet パッケージ

コマンドラインからコードメトリックスデータを生成する最も簡単な方法は、 [Microsoft CodeAnalysis. metrics](https://www.nuget.org/packages/Microsoft.CodeAnalysis.Metrics/) NuGet パッケージをインストールすることです。 パッケージをインストールしたら、プロジェクトファイルが格納されているディレクトリから `msbuild /t:Metrics` を実行します。 例:

```shell
C:\source\repos\ClassLibrary3\ClassLibrary3>msbuild /t:Metrics
Microsoft (R) Build Engine version 16.0.360-preview+g9781d96883 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 1/22/2019 4:29:57 PM.
Project "C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj" on node 1 (Metrics target(s))
.
Metrics:
  C:\source\repos\ClassLibrary3\packages\Microsoft.CodeMetrics.2.6.4-ci\build\\..\Metrics\Metrics.exe /project:C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj /out:ClassLibrary3.Metrics.xml
  Loading ClassLibrary3.csproj...
  Computing code metrics for ClassLibrary3.csproj...
  Writing output to 'ClassLibrary3.Metrics.xml'...
  Completed Successfully.
Done Building Project "C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj" (Metrics target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)
```

出力ファイル名をオーバーライドするには、`/p:MetricsOutputFile=<filename>`を指定します。 `/p:LEGACY_CODE_METRICS_MODE=true`を指定して、[レガシスタイルの](#previous-versions)コードメトリックスデータを取得することもできます。 例:

```shell
C:\source\repos\ClassLibrary3\ClassLibrary3>msbuild /t:Metrics /p:LEGACY_CODE_METRICS_MODE=true /p:MetricsOutputFile="Legacy.xml"
Microsoft (R) Build Engine version 16.0.360-preview+g9781d96883 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 1/22/2019 4:31:00 PM.
The "MetricsOutputFile" property is a global property, and cannot be modified.
Project "C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj" on node 1 (Metrics target(s))
.
Metrics:
  C:\source\repos\ClassLibrary3\packages\Microsoft.CodeMetrics.2.6.4-ci\build\\..\Metrics.Legacy\Metrics.Legacy.exe /project:C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj /out:Legacy.xml
  Loading ClassLibrary3.csproj...
  Computing code metrics for ClassLibrary3.csproj...
  Writing output to 'Legacy.xml'...
  Completed Successfully.
Done Building Project "C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj" (Metrics target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)
```

### <a name="code-metrics-output"></a>コードメトリックスの出力

生成される XML 出力の形式は次のとおりです。

::: moniker range=">=vs-2019"
```xml
<?xml version="1.0" encoding="utf-8"?>
<CodeMetricsReport Version="1.0">
  <Targets>
    <Target Name="ConsoleApp20.csproj">
      <Assembly Name="ConsoleApp20, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
        <Metrics>
          <Metric Name="MaintainabilityIndex" Value="100" />
          <Metric Name="CyclomaticComplexity" Value="1" />
          <Metric Name="ClassCoupling" Value="1" />
          <Metric Name="DepthOfInheritance" Value="1" />
          <Metric Name="SourceLines" Value="11" />
          <Metric Name="ExecutableLines" Value="1" />
        </Metrics>
        <Namespaces>
          <Namespace Name="ConsoleApp20">
            <Metrics>
              <Metric Name="MaintainabilityIndex" Value="100" />
              <Metric Name="CyclomaticComplexity" Value="1" />
              <Metric Name="ClassCoupling" Value="1" />
              <Metric Name="DepthOfInheritance" Value="1" />
              <Metric Name="SourceLines" Value="11" />
              <Metric Name="ExecutableLines" Value="1" />
            </Metrics>
            <Types>
              <NamedType Name="Program">
                <Metrics>
                  <Metric Name="MaintainabilityIndex" Value="100" />
                  <Metric Name="CyclomaticComplexity" Value="1" />
                  <Metric Name="ClassCoupling" Value="1" />
                  <Metric Name="DepthOfInheritance" Value="1" />
                  <Metric Name="SourceLines" Value="7" />
                  <Metric Name="ExecutableLines" Value="1" />
                </Metrics>
                <Members>
                  <Method Name="void Program.Main(string[] args)" File="C:\source\repos\ConsoleApp20\ConsoleApp20\Program.cs" Line="7">
                    <Metrics>
                      <Metric Name="MaintainabilityIndex" Value="100" />
                      <Metric Name="CyclomaticComplexity" Value="1" />
                      <Metric Name="ClassCoupling" Value="1" />
                      <Metric Name="SourceLines" Value="4" />
                      <Metric Name="ExecutableLines" Value="1" />
                    </Metrics>
                  </Method>
                </Members>
              </NamedType>
            </Types>
          </Namespace>
        </Namespaces>
      </Assembly>
    </Target>
  </Targets>
</CodeMetricsReport>
```
::: moniker-end
::: moniker range="vs-2017"
```xml
<?xml version="1.0" encoding="utf-8"?>
<CodeMetricsReport Version="1.0">
  <Targets>
    <Target Name="ConsoleApp20.csproj">
      <Assembly Name="ConsoleApp20, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
        <Metrics>
          <Metric Name="MaintainabilityIndex" Value="100" />
          <Metric Name="CyclomaticComplexity" Value="1" />
          <Metric Name="ClassCoupling" Value="1" />
          <Metric Name="DepthOfInheritance" Value="1" />
          <Metric Name="LinesOfCode" Value="11" />
        </Metrics>
        <Namespaces>
          <Namespace Name="ConsoleApp20">
            <Metrics>
              <Metric Name="MaintainabilityIndex" Value="100" />
              <Metric Name="CyclomaticComplexity" Value="1" />
              <Metric Name="ClassCoupling" Value="1" />
              <Metric Name="DepthOfInheritance" Value="1" />
              <Metric Name="LinesOfCode" Value="11" />
            </Metrics>
            <Types>
              <NamedType Name="Program">
                <Metrics>
                  <Metric Name="MaintainabilityIndex" Value="100" />
                  <Metric Name="CyclomaticComplexity" Value="1" />
                  <Metric Name="ClassCoupling" Value="1" />
                  <Metric Name="DepthOfInheritance" Value="1" />
                  <Metric Name="LinesOfCode" Value="7" />
                </Metrics>
                <Members>
                  <Method Name="void Program.Main(string[] args)" File="C:\source\repos\ConsoleApp20\ConsoleApp20\Program.cs" Line="7">
                    <Metrics>
                      <Metric Name="MaintainabilityIndex" Value="100" />
                      <Metric Name="CyclomaticComplexity" Value="1" />
                      <Metric Name="ClassCoupling" Value="1" />
                      <Metric Name="LinesOfCode" Value="4" />
                    </Metrics>
                  </Method>
                </Members>
              </NamedType>
            </Types>
          </Namespace>
        </Namespaces>
      </Assembly>
    </Target>
  </Targets>
</CodeMetricsReport>
```
::: moniker-end

### <a name="metricsexe"></a>Metrics

NuGet パッケージをインストールしない場合は、 *Metrics*実行可能ファイルを直接生成して使用することができます。 *Metrics*実行可能ファイルを生成するには、次のようにします。

1. [Dotnet](https://github.com/dotnet/roslyn-analyzers)リポジトリを複製します。
2. 管理者として Visual Studio の開発者コマンドプロンプトを開きます。
3. **Roslyn-アナライザー**リポジトリのルートから、次のコマンドを実行します。 `Restore.cmd`
4. ディレクトリを*Src\ Tools*に変更します。
5. 次のコマンドを実行して、**メトリック .csproj**プロジェクトをビルドします。

   ```shell
   msbuild /m /v:m /p:Configuration=Release Metrics.csproj
   ```

   *Metrics*という名前の実行可能ファイルが、リポジトリのルートにある*artifacts\bin*ディレクトリに生成されます。

#### <a name="metricsexe-usage"></a>Metrics の使用状況

*Metrics*を実行するには、プロジェクトまたはソリューションと出力 XML ファイルを引数として指定します。 例:

```shell
C:\>Metrics.exe /project:ConsoleApp20.csproj /out:report.xml
Loading ConsoleApp20.csproj...
Computing code metrics for ConsoleApp20.csproj...
Writing output to 'report.xml'...
Completed Successfully.
```

#### <a name="legacy-mode"></a>レガシモード

*レガシモード*では、 *Metrics*をビルドするように選択できます。 レガシモードバージョンのツールでは、[生成された以前のバージョンのツール](#previous-versions)に近いメトリック値が生成されます。 また、レガシモードでは、以前のバージョンのツールで生成されたコードメトリックスと同じメソッド型のコードメトリックス*が生成されます。* たとえば、フィールドおよびプロパティ初期化子のコードメトリックスデータは生成されません。 レガシモードは、旧バージョンとの互換性を維持したり、コードメトリックスの数値に基づいてコードをチェックインしたりする場合に便利です。 レガシモードで*Metrics*をビルドするコマンドは次のとおりです。

```shell
msbuild /m /v:m /t:rebuild /p:LEGACY_CODE_METRICS_MODE=true Metrics.csproj
```

詳細については、「[レガシモードでコードメトリックスを生成できるようにする](https://github.com/dotnet/roslyn-analyzers/pull/1841)」を参照してください。

### <a name="previous-versions"></a>以前のバージョン

::: moniker range=">=vs-2019"
Visual Studio 2015 には、 *metrics .exe*とも呼ばれるコマンドラインコードメトリックスツールが含まれていました。 このツールの以前のバージョンでは、バイナリ分析 (つまり、アセンブリベースの分析) が行われていました。 新しいバージョンの*Metrics*ツールは、代わりにソースコードを分析します。 新しい*metrics*ツールはソースコードに基づいているため、コマンドラインコードのメトリックの結果は、VISUAL Studio IDE および以前のバージョンの*metrics*によって生成されたものと異なる場合があります。 Visual Studio 2019 以降では、Visual Studio IDE はコマンドラインツールのようなソースコードを分析し、結果は同じである必要があります。

::: moniker-end
::: moniker range="vs-2017"
Visual Studio 2015 には、 *metrics .exe*とも呼ばれるコマンドラインコードメトリックスツールが含まれていました。 このツールの以前のバージョンでは、バイナリ分析 (つまり、アセンブリベースの分析) が行われていました。 代わりに、新しい*Metrics*ツールによってソースコードが分析されます。 新しい*metrics*ツールはソースコードベースであるため、コマンドラインコードのメトリックの結果は、VISUAL Studio IDE および以前のバージョンの*metrics*によって生成されるものとは異なります。
::: moniker-end

新しいコマンドラインコードメトリックスツールでは、ソリューションとプロジェクトを読み込むことができる限り、ソースコードエラーが存在する場合でもメトリックを計算します。

#### <a name="metric-value-differences"></a>メトリック値の違い

::: moniker range=">=vs-2019"
Visual Studio 2019 version 16.4 とメモリメトリックが (2.9.5) から開始して `ExecutableLines` `SourceLines`、以前の `LinesOfCode` メトリックを置き換えることができます。 新しいメトリックの説明については、「[コードメトリックスの値](../code-quality/code-metrics-values.md)」を参照してください。 `LinesOfCode` メトリックは、レガシモードで使用できます。
::: moniker-end
::: moniker range="vs-2017"
新しいコマンドラインコードメトリックスツールでは、`LinesOfCode` メトリックの精度と信頼性が向上しています。 Codegen の違いに依存せず、ツールセットやランタイムが変更されても変更されません。 新しいツールでは、空白行やコメントなど、実際のコード行がカウントされます。
::: moniker-end

`CyclomaticComplexity` や `MaintainabilityIndex` などの他のメトリックでは、以前のバージョンの*metrics*と同じ数式が使用されますが、新しいツールでは中間言語 (IL) 命令ではなく `IOperations` (論理ソースの命令) の数がカウントされます。 これらの数値は、Visual Studio IDE と以前のバージョンの*Metrics*によって生成された数値と若干異なります。

## <a name="see-also"></a>関連項目

- [コード メトリックスの結果 ウィンドウを使用します。](../code-quality/working-with-code-metrics-data.md)
- [コードメトリックスの値](../code-quality/code-metrics-values.md)
