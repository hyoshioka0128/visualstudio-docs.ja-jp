---
title: IDE またはコマンド ラインからコード メトリックを生成する
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
ms.openlocfilehash: 1abae26ed8a5e5db74f7b0d04db66d9d99930d5c
ms.sourcegitcommit: ade07bd1cf69b8b494d171ae648cfdd54f7800d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81649318"
---
# <a name="how-to-generate-code-metrics-data"></a>方法: コード メトリック ス データを生成する

コード メトリック ス データは、次の 3 つの方法で生成できます。

- [FxCop アナライザーを](#fxcop-analyzers-code-metrics-rules)インストールし、それに含まれる 4 つのコード メトリック (保守容易性) ルールを有効にします。

- Visual Studio で [コード メトリックの[**分析** > ]](#calculate-code-metrics-menu-command)メニュー コマンドを選択します。

- C# プロジェクトおよび Visual Basic プロジェクトの[コマンド ライン](#command-line-code-metrics)から。

## <a name="fxcop-analyzers-code-metrics-rules"></a>FxCop アナライザーのコード メトリック規則

[FxCop アナライザーの NuGet パッケージには、](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)いくつかのコード メトリック[アナライザー](roslyn-analyzers-overview.md)ルールが含まれています。

- [CA1501](ca1501-avoid-excessive-inheritance.md)
- [CA1502](ca1502.md)
- [CA1505](ca1505.md)
- [CA1506](ca1506.md)

これらのルールは既定で無効になっていますが、[**ソリューション エクスプローラー**](use-roslyn-analyzers.md#set-rule-severity-from-solution-explorer)または[規則セット](using-rule-sets-to-group-code-analysis-rules.md)ファイルで有効にできます。 たとえば、警告としてルール CA1502 を有効にするには、.ruleset ファイルに次のエントリが含まれます。

```xml
<?xml version="1.0" encoding="utf-8"?>
<RuleSet Name="Rules" Description="Rules" ToolsVersion="16.0">
  <Rules AnalyzerId="Microsoft.CodeQuality.Analyzers" RuleNamespace="Microsoft.CodeQuality.Analyzers">
    <Rule Id="CA1502" Action="Warning" />
  </Rules>
</RuleSet>
```

### <a name="configuration"></a>構成

FxCop アナライザーパッケージのコード メトリック規則が起動するしきい値を設定できます。

1. テキスト ファイルを作成します。 例として、*名前を付けることができます。*

2. 次の形式でテキスト ファイルに必要なしきい値を追加します。

   ```txt
   CA1502: 10
   ```

   この例では、メソッドのサイクロマティック複雑度が 10 を超える場合に、ルール[CA1502](ca1502.md)が起動するように構成されています。

3. Visual Studio の **[プロパティ]** ウィンドウまたはプロジェクト ファイルで、構成ファイルのビルド アクションを[**[追加ファイル]**](../ide/build-actions.md#build-action-values)としてマークします。 次に例を示します。

   ```xml
   <ItemGroup>
     <AdditionalFiles Include="CodeMetricsConfig.txt" />
   </ItemGroup>
   ```

## <a name="calculate-code-metrics-menu-command"></a>[コード メトリックスの計算] メニュー コマンド

IDE で開いているプロジェクトの 1 つまたはすべてのコード**メトリックを**生成するには、[コード メトリックスの**分析** > ] メニューを使用します。

### <a name="generate-code-metrics-results-for-an-entire-solution"></a>ソリューション全体のコード メトリックスの結果を生成する

次のいずれかの方法で、ソリューション全体のコード メトリックス結果を生成できます。

- メニュー バーで、[**ソリューション**の**コード メトリックス** > の**分析** > ] を選択します。

- **ソリューション エクスプローラ**でソリューションを右クリックし、[コード**メトリックスの計算**] を選択します。

- [**コード メトリックスの結果**] ウィンドウで、[**ソリューションのコード メトリックスの計算**] ボタンを選択します。

結果が生成され、[**コード メトリックスの結果**] ウィンドウが表示されます。 結果の詳細を表示するには、[**階層**] 列のツリーを展開します。

### <a name="generate-code-metrics-results-for-one-or-more-projects"></a>1 つ以上のプロジェクトのコード メトリックスの結果を生成する

1. **ソリューション エクスプローラ**で、1 つまたは複数のプロジェクトを選択します。

1. メニュー バーで、[**選択したプロジェクトの****コード メトリックス** > の**分析** > ] を選択します。

結果が生成され、[**コード メトリックスの結果**] ウィンドウが表示されます。 結果の詳細を表示するには、**階層**内のツリーを展開します。

::: moniker range="vs-2017"

> [!NOTE]
> [**コード メトリックスの計算]** コマンドは、.NET Core プロジェクトおよび .NET 標準プロジェクトでは機能しません。 .NET Core または .NET Standard プロジェクトのコード メトリックを計算するには、次の方法があります。
>
> - 代わりに[コマンド ライン](#command-line-code-metrics)からコード メトリックを計算する
>
> - ビジュアル[スタジオ 2019 にアップグレードします。](https://visualstudio.microsoft.com/downloads)

::: moniker-end

## <a name="command-line-code-metrics"></a>コマンド ライン コードメトリック

.NET Framework、.NET Core、および .NET 標準アプリの C# プロジェクトおよび Visual Basic プロジェクトのコマンド ラインからコード メトリック ス データを生成できます。 コマンド ラインからコード メトリックを実行するには[、Microsoft.CodeAnalysis.Metrics NuGet パッケージ](#microsoftcodeanalysismetrics-nuget-package)をインストールするか[、Metrics.exe](#metricsexe)実行可能ファイルを自分でビルドします。

### <a name="microsoftcodeanalysismetrics-nuget-package"></a>パッケージを使用します。

コマンド ラインからコード メトリック データを生成する最も簡単な方法は[、Microsoft.CodeAnalysis.Metrics](https://www.nuget.org/packages/Microsoft.CodeAnalysis.Metrics/) NuGet パッケージをインストールすることです。 パッケージをインストールしたら、プロジェクト ファイルが`msbuild /t:Metrics`格納されているディレクトリから実行します。 次に例を示します。

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

出力ファイル名をオーバーライドするには`/p:MetricsOutputFile=<filename>`、 を指定します。 また、 を指定して[、従来のスタイルの](#previous-versions)コード`/p:LEGACY_CODE_METRICS_MODE=true`メトリック データを取得することもできます。 次に例を示します。

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

### <a name="code-metrics-output"></a>コード メトリック出力

生成された XML 出力は、次の形式をとります。

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

### <a name="metricsexe"></a>メトリックス.exe

NuGet パッケージをインストールしない場合は *、Metrics.exe*実行可能ファイルを直接生成して使用できます。 Metrics.exe 実行可能ファイルを生成するには、次*の手順を実行*します。

1. [ドットネット/ロズリンアナライザリポジトリをクローンします](https://github.com/dotnet/roslyn-analyzers)。
2. 管理者として Visual Studio の開発者コマンド プロンプトを開きます。
3. **roslyn アナライザ**ーのルートから、次のコマンドを実行します。`Restore.cmd`
4. ディレクトリを*src\Tools*に変更します。
5. 次のコマンドを実行して **、Metrics.csproj**プロジェクトをビルドします。

   ```shell
   msbuild /m /v:m /p:Configuration=Release Metrics.csproj
   ```

   *Metrics.exe*という名前の実行可能ファイルが、repo ルートの下の*artifacts\bin*ディレクトリに生成されます。

#### <a name="metricsexe-usage"></a>メトリックス.exe の使用法

*Metrics.exe*を実行するには、プロジェクトまたはソリューションと出力 XML ファイルを引数として指定します。 次に例を示します。

```shell
C:\>Metrics.exe /project:ConsoleApp20.csproj /out:report.xml
Loading ConsoleApp20.csproj...
Computing code metrics for ConsoleApp20.csproj...
Writing output to 'report.xml'...
Completed Successfully.
```

#### <a name="legacy-mode"></a>レガシーモード

*Metrics.exe*を*レガシ モード*でビルドすることを選択できます。 従来のモード バージョンのツールは、[ツールの古いバージョン](#previous-versions)に近いメトリック値を生成します。 また、従来のモードでは *、Metrics.exe*は、以前のバージョンのツールで生成されたコード メトリックスと同じ種類のメソッドのコード メトリックスを生成します。 たとえば、フィールド初期化子とプロパティ初期化子のコード メトリック ス データは生成されません。 レガシー モードは、下位互換性を保つ場合や、コード メトリック番号に基づくコード チェックイン ゲートがある場合に便利です。 レガシー モードで*Metrics.exe*をビルドするコマンドは次のとおりです。

```shell
msbuild /m /v:m /t:rebuild /p:LEGACY_CODE_METRICS_MODE=true Metrics.csproj
```

詳細については、「[レガシ モードでのコード メトリックの生成を有効にする](https://github.com/dotnet/roslyn-analyzers/pull/1841)」を参照してください。

### <a name="previous-versions"></a>以前のバージョン

::: moniker range=">=vs-2019"
Visual Studio 2015 には *、Metrics.exe*とも呼ばれるコマンド ライン コード メトリック ツールが含まれています。 この以前のバージョンのツールは、バイナリ分析、つまりアセンブリベースの分析を行いました。 新しいバージョンの*Metrics.exe*ツールは、代わりにソース コードを分析します。 新しい*Metrics.exe*ツールはソース コード ベースであるため、コマンド ライン コードのメトリックスの結果は、Visual Studio IDE および以前のバージョンの*Metrics.exe*によって生成される結果とは異なる場合があります。 Visual Studio 2019 以降、Visual Studio IDE は、コマンド ライン ツールのようなソース コードを分析し、結果は同じである必要があります。

::: moniker-end
::: moniker range="vs-2017"
Visual Studio 2015 には *、Metrics.exe*とも呼ばれるコマンド ライン コード メトリック ツールが含まれています。 この以前のバージョンのツールは、バイナリ分析、つまりアセンブリベースの分析を行いました。 新しい*Metrics.exe*ツールは、代わりにソース コードを分析します。 新しい*Metrics.exe*ツールはソース コード ベースであるため、コマンド ライン コードのメトリックスの結果は、Visual Studio IDE および以前のバージョンの*Metrics.exe*によって生成されるものとは異なります。
::: moniker-end

新しいコマンド ライン コード メトリック ツールは、ソリューションとプロジェクトを読み込むことができる限り、ソース コード エラーが存在する場合でもメトリックを計算します。

#### <a name="metric-value-differences"></a>メトリック値の差異

::: moniker range=">=vs-2019"
Visual Studio 2019 バージョン 16.4 および Microsoft.CodeAnalysis.Metics (2.9.5) で開始し、`SourceLines``ExecutableLines`以前`LinesOfCode`のメトリックを置き換えます。 新しいメトリックの説明については、「コード[メトリックの値](../code-quality/code-metrics-values.md)」を参照してください。 メトリック`LinesOfCode`はレガシ モードで使用できます。
::: moniker-end
::: moniker range="vs-2017"
メトリック`LinesOfCode`は、新しいコマンド ライン コード メトリック ツールで、より正確で信頼性が高くなっています。 これはコードジェンの違いに依存せず、ツールセットやランタイムが変更されたときには変更されません。 新しいツールは、空白行やコメントを含むコードの実際の行をカウントします。
::: moniker-end

Metrics.exe`CyclomaticComplexity`の`MaintainabilityIndex`以前のバージョンと同じ数式を使用*Metrics.exe*するなどの他の`IOperations`メトリックも使用されますが、新しいツールでは中間言語 (IL) 命令ではなく (論理ソース命令) の数がカウントされます。 数値は、Visual Studio IDE および以前のバージョンの*Metrics.exe*によって生成されるものとは若干異なります。

## <a name="see-also"></a>関連項目

- [[コード メトリックスの結果] ウィンドウを使用する](../code-quality/working-with-code-metrics-data.md)
- [コード メトリックの値](../code-quality/code-metrics-values.md)
