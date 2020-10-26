---
title: .runsettings ファイルを使用して単体テストを構成する
ms.date: 07/15/2020
ms.topic: conceptual
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: f638d60b7bd4416bb7a19cc960cac1159c755ab3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86972297"
---
# <a name="configure-unit-tests-by-using-a-runsettings-file"></a>*.runsettings ファイルを使用して単体テストを構成する*

Visual Studio の単体テストは、 *.runsettings* ファイルを使用して構成できます。 たとえば、テストが実行される .NET のバージョン、テスト結果のディレクトリ、テストの実行中に収集されるデータを変更できます。 *.runsettings* ファイルをよく使うのは、[コード カバレッジ分析](../test/customizing-code-coverage-analysis.md)をカスタマイズする場合です。

[コマンド ライン](vstest-console-options.md)から、IDE から、あるいは Azure Test Plans または Team Foundation Server (TFS) を使用する[ビルド ワークフロー](/azure/devops/pipelines/test/getting-started-with-continuous-testing?view=vsts)で実行されるテストを実行設定ファイルを使用して構成できます。

実行設定ファイルは省略可能です。 特殊な構成を行う必要がない場合、 *.runsettings* ファイルは不要です。

## <a name="create-a-run-settings-file-and-customize-it"></a>実行設定ファイルを作成してカスタマイズする

1. 実行設定ファイルをソリューションに追加します。 **ソリューション エクスプローラー**でソリューションのショートカット メニューを開き、 **[追加]**  >  **[新しい項目]** 、 **[XML ファイル]** の順に選択します。 *test.runsettings* などの名前でファイルを保存します。

   > [!TIP]
   > 拡張子 *.runsettings* を使用していれば、ファイル名は自由です。

2. 「[*.runsettings ファイルの例](#example-runsettings-file)」からの内容を追加し、後続の各セクションの説明に従って、ニーズに合わせてカスタマイズします。

3. 次のいずれかの方法を利用し、必要な *.runsettings ファイルを指定します。

   - [Visual Studio IDE](#specify-a-run-settings-file-in-the-ide)
   - [コマンド ライン](#specify-a-run-settings-file-from-the-command-line)
   - Azure Test Plans または Team Foundation Server (TFS) を使用する[ビルド ワークフロー](/azure/devops/pipelines/test/getting-started-with-continuous-testing?view=vsts)

4. カスタムの実行設定を使用する単体テストを実行します。

::: moniker range="vs-2017"

IDE でカスタム設定のオンとオフを切り替える場合、 **[テスト]** の **[テストの設定]** メニューでファイルを選択したり選択解除したりします。

![Visual Studio 2017 でのカスタム設定ファイルがある設定メニュー](../test/media/codecoverage-settingsfile.png)

::: moniker-end

::: moniker range=">=vs-2019"

IDE でカスタム設定のオンとオフを切り替える場合、 **[テスト]** メニューでファイルを選択したり選択解除したりします。

::: moniker-end

> [!TIP]
> ソリューションに複数の *.runsettings* ファイルを作成し、必要に応じて、いずれかをアクティブなテスト設定ファイルとして選択することができます。

## <a name="specify-a-run-settings-file-in-the-ide"></a>IDE で実行設定ファイルを指定する

使用できる方法は、Visual Studio のバージョンによって異なります。

::: moniker range="vs-2017"
IDE で実行設定ファイルを指定するには、 **[テスト]** > **[テストの設定]** > **[テスト設定ファイルの選択]** を選択し、 *.runsettings* ファイルを選択します。

![Visual Studio 2017 の [テスト設定ファイルの選択] メニュー](media/select-test-settings-file.png)

ファイルは、[テストの設定] メニューに表示され、選択または選択解除できます。 選択されている間、実行設定ファイルは、 **[コード カバレッジの分析]** を選ぶたびに適用されます。
::: moniker-end

::: moniker range=">=vs-2019"

### <a name="visual-studio-2019-version-164-and-later"></a>Visual Studio 2019 バージョン 16.4 以降

Visual Studio 2019 バージョン 16.4 以降で実行設定ファイルを指定するには、次の 3 つの方法があります。

- [実行設定を自動検出する](#autodetect-the-run-settings-file)
- [実行設定を手動で設定する](#manually-select-the-run-settings-file)
- [ビルド プロパティを設定する](#set-a-build-property)

#### <a name="autodetect-the-run-settings-file"></a>実行設定ファイルを自動検出する

実行設定ファイルを自動検出するには、それをソリューションのルートに配置します。

実行設定ファイルの自動検出が有効になっている場合、このファイル内の設定は実行されるすべてのテストに適用されます。 runsettings ファイルの自動検出は、次の 2 つの方法で有効にすることができます。
  
- **[ツール]** 、 **[オプション]** 、 **[テスト]** 、 **[runsettings ファイルの自動検出]** の順に選択する

   ![Visual Studio 2019 での [runsettings ファイルの自動検出] オプション](media/vs-2019/auto-detect-runsettings-tools-window.png)
      
- **[テスト]** 、 **[実行設定の構成]** 、 **[runsettings ファイルの自動検出]** を選択する
    
   ![Visual Studio 2019 での [runsettings ファイルの自動検出] メニュー](media/vs-2019/auto-detect-runsettings-menu.png)

#### <a name="manually-select-the-run-settings-file"></a>実行設定ファイルを手動で選択する

IDE で、 **[テスト]** > **[実行設定の構成]** > **[ソリューション全体の runsettings ファイルの選択]** を選択し、 *.runsettings* ファイルを選択します。

   - このソリューションのルートに *.runsettings* ファイルが存在する場合は、このファイルによりオーバーライドされます。このファイルは実行されるすべてのテストに適用されます。  
   - このファイルの選択は、ローカルにのみ保持されます。

![Visual Studio 2019 の [テスト] の [ソリューション全体の runsettings ファイルの選択] メニュー](media/vs-2019/select-solution-settings-file.png)

#### <a name="set-a-build-property"></a>ビルド プロパティを設定する

プロジェクト ファイルまたは Directory.Build.props ファイルを使用して、プロジェクトにビルド プロパティを追加します。 プロジェクトの実行設定ファイルは、**RunSettingsFilePath** プロパティによって指定されます。

- 現在、プロジェクト レベルの実行設定は、C#、VB、C++、および F# プロジェクトに対してサポートされています。
- プロジェクトに対して指定したファイルにより、ソリューションで指定された他のあらゆる実行設定ファイルがオーバーライドされます。
- [これらの MSBuild プロパティ](https://docs.microsoft.com/visualstudio/msbuild/msbuild-reserved-and-well-known-properties?view=vs-2019)を使用し、runsettings ファイルのパスを指定できます。 

プロジェクトに対して *.runsettings* ファイルを指定する例:
    
```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <RunSettingsFilePath>$(MSBuildProjectDirectory)\example.runsettings</RunSettingsFilePath>
  </PropertyGroup>
  ...
</Project>
```

### <a name="visual-studio-2019-version-163-and-earlier"></a>Visual Studio 2019 バージョン 16.3 以前

IDE で実行設定ファイルを指定するには、 **[テスト]**  >  **[設定ファイルの選択]** の順に選択します。 *.runsettings* ファイルを参照し、選択します。

![Visual Studio 2019 の [テスト設定ファイルの選択] メニュー](media/vs-2019/select-settings-file.png)

ファイルは、[テスト] メニューに表示され、選択または選択解除できます。 選択されている間、実行設定ファイルは、 **[コード カバレッジの分析]** を選ぶたびに適用されます。
::: moniker-end

## <a name="specify-a-run-settings-file-from-the-command-line"></a>コマンド ラインから実行設定ファイルを指定する

コマンド ラインからテストを実行するには、*vstest.console.exe* を使い、 **/Settings** パラメーターを使って設定ファイルを指定します。

1. Visual Studio の[開発者コマンド プロンプト](/dotnet/framework/tools/developer-command-prompt-for-vs)を開きます。

2. 次のようなコマンドを入力します。

   ```cmd
   vstest.console.exe MyTestAssembly.dll /EnableCodeCoverage /Settings:CodeCoverage.runsettings
   ```

   or

   ```cmd
   vstest.console.exe --settings:test.runsettings test.dll
   ```

詳細については、「[VSTest.Console.exe のコマンド ライン オプション](vstest-console-options.md)」を参照してください。

## <a name="the-runsettings-file"></a>*.runsettings ファイル

*.runsettings ファイルは、**RunSettings** 要素内にさまざまな構成要素を含む XML ファイルです。 後続のセクションでさまざまな要素について説明します。 完全なサンプルが必要であれば、「[*.runsettings ファイルの例](#example-runsettings-file)」を参照してください。

```xml
<?xml version="1.0" encoding="utf-8"?>
<RunSettings>
  <!-- configuration elements -->
</RunSettings>
```

既定値があるため、各構成要素は省略可能です。

## <a name="runconfiguration-element"></a>RunConfiguration 要素

```xml
<RunConfiguration>
    <MaxCpuCount>1</MaxCpuCount>
    <ResultsDirectory>.\TestResults</ResultsDirectory>
    <TargetPlatform>x86</TargetPlatform>
    <TargetFrameworkVersion>Framework40</TargetFrameworkVersion>
    <TestAdaptersPaths>%SystemDrive%\Temp\foo;%SystemDrive%\Temp\bar</TestAdaptersPaths>
    <TestSessionTimeout>10000</TestSessionTimeout>
</RunConfiguration>
```

**RunConfiguration** 要素には、次の要素を含めることができます。

|ノード|Default|値|
|-|-|-|
|**MaxCpuCount**|1|この設定では、単体テストを実行するときに、マシンで使用可能なコアを使用してテストを並列実行する程度を制御します。 テストの実行エンジンは、使用可能な各コア上の別個のプロセスとして起動し、実行するテストが入ったコンテナーを各コアに与えます。 コンテナーとしては、アセンブリ、DLL、または関連する成果物を指定できます。 テスト コンテナーはスケジューリングの単位です。 各コンテナーでは、テストはテスト フレームワークに従って実行されます。 コンテナーが多くある場合、あるコンテナー内のテストの実行を終了したプロセスには、次の使用可能なコンテナーが与えられます。<br /><br />MaxCpuCount には次の値を指定することができます。<br /><br />n。ここで n は、1 以上、コアの数以下です。最大 n 個のプロセスが起動されます<br /><br />n。ここで n はその他の値です。起動するプロセスの数は、利用可能なコアの数まで指定できます。 たとえば、"n = 0" と設定すると、環境に基づいて起動するプロセスの最適な数がプラットフォームによって自動的に決定されます。|
|**ResultsDirectory**||テスト結果が配置されるディレクトリ。 パスは .runsettings ファイルが含まれるディレクトリの相対パスになります。|
|**TargetFrameworkVersion**|Framework40|.NET Core ソースの場合は `FrameworkCore10`、UWP ベースのソースの場合は `FrameworkUap10`、.NET Framework 4.5 以降の場合は `Framework45`、.NET Framework 4.0 の場合は `Framework40`、.NET Framework 3.5 の場合は `Framework35`。<br /><br />この設定では、テストを検出して実行するために使用される単体テスト フレームワークのバージョンを指定します。 これは、単体テスト プロジェクトのビルド プロパティで指定した .NET プラットフォームのバージョンと異なっていてもかまいません。<br /><br />`TargetFrameworkVersion` 要素を *.runsettings* ファイルから省略した場合、フレームワークのバージョンはビルド済みバイナリに基づいてプラットフォームにより自動的に決定されます。|
|**TargetPlatform**|x86|x86、x64|
|**TreatTestAdapterErrorsAsWarnings**|False|false、true|
|**TestAdaptersPaths**||TestAdapter が配置されているディレクトリの 1 つまたは複数のパス|
|**TestSessionTimeout**||指定されたタイムアウトを超えたときにユーザーがテスト セッションを終了できるようにします。 タイムアウトを設定すると、リソースが適切に消費され、テスト セッションが設定された時間に制限されます。 この設定は、**Visual Studio 2017 バージョン 15.5** 以降で使用できます。|
|**DotnetHostPath**||testhost を実行するために使用される dotnet host へのカスタム パスを指定します。 これは、dotnet/runtime リポジトリをビルドする場合など、独自の dotnet をビルドするときに便利です。 このオプションを指定すると、testhost.exe の検索がスキップされ、常に testhost.dll が使用されます。 

## <a name="datacollectors-element-diagnostic-data-adapters"></a>DataCollectors 要素 (診断データ アダプター)

**DataCollectors** 要素は、診断データ アダプターの設定を指定します。 診断データ アダプターは、テスト対象の環境とアプリケーションに関する追加情報を収集します。 各アダプターには既定の設定があるため、既定値を使用しない場合にのみ設定を指定する必要があります。

```xml
<DataCollectionRunSettings>
  <DataCollectors>
    <!-- data collectors -->
  </DataCollectors>
</DataCollectionRunSettings>
```

### <a name="codecoverage-data-collector"></a>CodeCoverage データ コレクター

コード カバレッジ データ コレクターは、アプリケーション コードのどの部分がテストで実行されたかを示すログを作成します。 コード カバレッジの設定のカスタマイズの詳細については、「[コード カバレッジ分析のカスタマイズ](../test/customizing-code-coverage-analysis.md)」を参照してください。

```xml
<DataCollector friendlyName="Code Coverage" uri="datacollector://Microsoft/CodeCoverage/2.0" assemblyQualifiedName="Microsoft.VisualStudio.Coverage.DynamicCoverageDataCollector, Microsoft.VisualStudio.TraceCollector, Version=11.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a">
  <Configuration>
    <CodeCoverage>
      <ModulePaths>
        <Exclude>
          <ModulePath>.*CPPUnitTestFramework.*</ModulePath>
        </Exclude>
      </ModulePaths>

      <UseVerifiableInstrumentation>True</UseVerifiableInstrumentation>
      <AllowLowIntegrityProcesses>True</AllowLowIntegrityProcesses>
      <CollectFromChildProcesses>True</CollectFromChildProcesses>
      <CollectAspDotNet>False</CollectAspDotNet>
    </CodeCoverage>
  </CodeCoverage>
</Configuration>
```

### <a name="videorecorder-data-collector"></a>VideoRecorder データ コレクター

ビデオ データ コレクターは、テストが実行されたときに、画面記録をキャプチャします。 この記録は、UI テストのトラブルシューティングに役立ちます。 ビデオ データ コレクターは、**Visual Studio 2017 バージョン 15.5** 以降で使用できます。 このデータ コレクターの構成例が必要であれば、「[*.runsettings ファイルの例](#example-runsettings-file)」を参照してください。

他の種類の診断データ アダプターをカスタマイズするには、[テスト設定ファイル](../test/collect-diagnostic-information-using-test-settings.md)を使用します。

### <a name="blame-data-collector"></a>Blame データ コレクター

このオプションは、テスト ホストがクラッシュする原因となる問題のあるテストを分離するのに役立ちます。 コレクターを実行すると、出力ファイル (*Sequence.xml*) が *TestResults* に作成されます。これには、クラッシュ前のテストの実行順序がキャプチャされます。 

```xml
<DataCollector friendlyName="blame" enabled="True">
</DataCollector>
```

## <a name="testrunparameters"></a>TestRunParameters

```xml
<TestRunParameters>
    <Parameter name="webAppUrl" value="http://localhost" />
    <Parameter name="docsUrl" value="https://docs.microsoft.com" />
</TestRunParameters>
```

テスト実行パラメーターでは、実行時にテストで使用できる変数と値の定義方法が指定します。 MSTest <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext.Properties%2A?displayProperty=nameWithType> プロパティ (または NUnit [TestContext](https://docs.nunit.org/articles/nunit/writing-tests/TestContext.html)) を使用してパラメーターにアクセスします。

```csharp
private string _appUrl;
public TestContext TestContext { get; set; }

[TestMethod] // [Test] for NUnit
public void HomePageTest()
{
    string _appURL = TestContext.Properties["webAppUrl"];
}
```

テスト実行パラメーターを使用するには、パブリックの <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext> プロパティをテスト クラスに追加します。

## <a name="loggerrunsettings-element"></a>LoggerRunSettings 要素

`LoggerRunSettings` セクションによって、テスト実行に使用される 1 つ以上のロガーが定義されます。 最も一般的なロガーは、コンソール、Visual Studio テスト結果ファイル (trx)、html です。

```xml
<LoggerRunSettings>
    <Loggers>        
      <Logger friendlyName="console" enabled="True">
        <Configuration>
            <Verbosity>quiet</Verbosity>
        </Configuration>
      </Logger>
      <Logger friendlyName="trx" enabled="True">
        <Configuration>
          <LogFileName>foo.trx</LogFileName>
        </Configuration>
      </Logger>
      <Logger friendlyName="html" enabled="True">
        <Configuration>
          <LogFileName>foo.html</LogFileName>
        </Configuration>
      </Logger>
    </Loggers>
  </LoggerRunSettings>
```

## <a name="mstest-element"></a>MSTest 要素

これらは、 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> 属性を持つテスト メソッドを実行するテスト アダプターに固有の設定です。

```xml
<MSTest>
    <MapInconclusiveToFailed>True</MapInconclusiveToFailed>
    <CaptureTraceOutput>false</CaptureTraceOutput>
    <DeleteDeploymentDirectoryAfterTestRunIsComplete>False</DeleteDeploymentDirectoryAfterTestRunIsComplete>
    <DeploymentEnabled>False</DeploymentEnabled>
    <AssemblyResolution>
      <Directory Path="D:\myfolder\bin\" includeSubDirectories="false"/>
    </AssemblyResolution>
</MSTest>
```

|構成|Default|値|
|-|-|-|
|**ForcedLegacyMode**|False|Visual Studio 2012 で、MSTest アダプターは処理速度を向上させ、よりスケーラブルになるように最適化されました。 テストが実行される順序などの一部の動作は、Visual Studio の以前のエディションでの動作と完全に同じではない場合もあります。 以前のテスト アダプターを使用するには、この値を **true** に設定します。<br /><br />たとえば、単体テスト用に指定された *app.config* ファイルがある場合は、この設定を使用することがあります。<br /><br />より新しいアダプターを使用できるように、テストのリファクタリングを検討することをお勧めします。|
|**IgnoreTestImpact**|False|テストの影響機能は、MSTest で実行したとき、または Microsoft Test Manager (Visual Studio 2017 では非推奨) から実行したときに最近の変更の影響を受けるテストの優先順位を付けます。 この設定は機能を非アクティブ化します。 詳細については、「[前回のビルド以降に実行する必要があるテストの検索](https://msdn.microsoft.com/library/dd286589)」を参照してください。|
|**SettingsFile**||ここで、MSTest アダプターで使用するテスト設定ファイルを指定できます。 また、[[設定] メニューから](#specify-a-run-settings-file-in-the-ide)テスト設定ファイルを指定することもできます。<br /><br />この値を指定する場合は、 **ForcedlegacyMode** も **true**に設定する必要があります。<br /><br />`<ForcedLegacyMode>true</ForcedLegacyMode>`|
|**KeepExecutorAliveAfterLegacyRun**|False|テストの実行が完了した後、MSTest がシャットダウンされます。 テストの一部として起動されたプロセスも中止されています。 テスト実行プログラムを中止しない場合は、この値を **true** に設定します。 たとえば、コード化された UI テストの間にブラウザーの実行を維持するために、この設定を使用できます。|
|**DeploymentEnabled**|true|値を **false** に設定すると、テスト メソッドで指定した配置項目が配置ディレクトリにコピーされません。|
|**CaptureTraceOutput**|true|<xref:System.Diagnostics.Trace.WriteLine%2A?displayProperty=nameWithType> を使用して、テスト メソッドからデバッグ トレースに書き込むことができます。|
|**DeleteDeploymentDirectoryAfterTestRunIsComplete**|true|テストの実行後に配置ディレクトリを保持するには、この値を **false** に設定します。|
|**MapInconclusiveToFailed**|False|テストが結果不確定の状態で完了した場合は、**テスト エクスプローラー**でスキップ状態にマップされます。 結果不確定のテストを失敗として表示する場合は、この値を **true** に設定します。|
|**InProcMode**|False|テストを MSTest アダプターと同じプロセスで実行する場合は、この値を **true** に設定します。 この設定で、わずかにパフォーマンスが向上します。 ただし、あるテストが例外で終了した場合、残りのテストは続行されません。|
|**AssemblyResolution**|False|単体テストを検索して実行する場合、追加のアセンブリへのパスを指定できます。 たとえば、テスト アセンブリと同じディレクトリにない依存関係アセンブリにこれらのパスを使用します。 パスを指定するには、**Directory Path** 要素を使用します。 パスには環境変数を含めることができます。<br /><br />`<AssemblyResolution>  <Directory Path="D:\myfolder\bin\" includeSubDirectories="false"/> </AssemblyResolution>`|

## <a name="example-runsettings-file"></a>*.runsettings* ファイルの例

次の XML は、一般的な *.runsettings* ファイルの内容を示しています。 このコードをコピーし、自分のニーズに合わせて編集します。

ファイルの各要素には既定値があるため、省略可能です。

```xml
<?xml version="1.0" encoding="utf-8"?>
<RunSettings>
  <!-- Configurations that affect the Test Framework -->
  <RunConfiguration>
    <MaxCpuCount>1</MaxCpuCount>
    <!-- Path relative to directory that contains .runsettings file-->
    <ResultsDirectory>.\TestResults</ResultsDirectory>

    <!-- x86 or x64 -->
    <!-- You can also change it from the Test menu; choose "Processor Architecture for AnyCPU Projects" -->
    <TargetPlatform>x86</TargetPlatform>

    <!-- Framework35 | [Framework40] | Framework45 -->
    <TargetFrameworkVersion>Framework40</TargetFrameworkVersion>

    <!-- Path to Test Adapters -->
    <TestAdaptersPaths>%SystemDrive%\Temp\foo;%SystemDrive%\Temp\bar</TestAdaptersPaths>

    <!-- TestSessionTimeout was introduced in Visual Studio 2017 version 15.5 -->
    <!-- Specify timeout in milliseconds. A valid value should be greater than 0 -->
    <TestSessionTimeout>10000</TestSessionTimeout>
  </RunConfiguration>

  <!-- Configurations for data collectors -->
  <DataCollectionRunSettings>
    <DataCollectors>
      <DataCollector friendlyName="Code Coverage" uri="datacollector://Microsoft/CodeCoverage/2.0" assemblyQualifiedName="Microsoft.VisualStudio.Coverage.DynamicCoverageDataCollector, Microsoft.VisualStudio.TraceCollector, Version=11.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a">
        <Configuration>
          <CodeCoverage>
            <ModulePaths>
              <Exclude>
                <ModulePath>.*CPPUnitTestFramework.*</ModulePath>
              </Exclude>
            </ModulePaths>

            <!-- We recommend you do not change the following values: -->
            <UseVerifiableInstrumentation>True</UseVerifiableInstrumentation>
            <AllowLowIntegrityProcesses>True</AllowLowIntegrityProcesses>
            <CollectFromChildProcesses>True</CollectFromChildProcesses>
            <CollectAspDotNet>False</CollectAspDotNet>

          </CodeCoverage>
        </Configuration>
      </DataCollector>

      <DataCollector uri="datacollector://microsoft/VideoRecorder/1.0" assemblyQualifiedName="Microsoft.VisualStudio.TestTools.DataCollection.VideoRecorder.VideoRecorderDataCollector, Microsoft.VisualStudio.TestTools.DataCollection.VideoRecorder, Version=15.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a" friendlyName="Screen and Voice Recorder">
        <!--Video data collector was introduced in Visual Studio 2017 version 15.5 -->
        <Configuration>
          <!-- Set "sendRecordedMediaForPassedTestCase" to "false" to add video attachments to failed tests only -->
          <MediaRecorder sendRecordedMediaForPassedTestCase="true"  xmlns="">           
            <ScreenCaptureVideo bitRate="512" frameRate="2" quality="20" />
          </MediaRecorder>
        </Configuration>
      </DataCollector>

      <!-- Configuration for blame data collector -->
      <DataCollector friendlyName="blame" enabled="True">
      </DataCollector>

    </DataCollectors>
  </DataCollectionRunSettings>

  <!-- Parameters used by tests at run time -->
  <TestRunParameters>
    <Parameter name="webAppUrl" value="http://localhost" />
    <Parameter name="webAppUserName" value="Admin" />
    <Parameter name="webAppPassword" value="Password" />
  </TestRunParameters>
  
  <!-- Configuration for loggers -->
  <LoggerRunSettings>
    <Loggers>      
      <Logger friendlyName="console" enabled="True">
        <Configuration>
            <Verbosity>quiet</Verbosity>
        </Configuration>
      </Logger>
      <Logger friendlyName="trx" enabled="True">
        <Configuration>
          <LogFileName>foo.trx</LogFileName>
        </Configuration>
      </Logger>
      <Logger friendlyName="html" enabled="True">
        <Configuration>
          <LogFileName>foo.html</LogFileName>
        </Configuration>
      </Logger>
      <Logger friendlyName="blame" enabled="True" />
    </Loggers>
  </LoggerRunSettings>

  <!-- Adapter Specific sections -->

  <!-- MSTest adapter -->
  <MSTest>
    <MapInconclusiveToFailed>True</MapInconclusiveToFailed>
    <CaptureTraceOutput>false</CaptureTraceOutput>
    <DeleteDeploymentDirectoryAfterTestRunIsComplete>False</DeleteDeploymentDirectoryAfterTestRunIsComplete>
    <DeploymentEnabled>False</DeploymentEnabled>
    <AssemblyResolution>
      <Directory path="D:\myfolder\bin\" includeSubDirectories="false"/>
    </AssemblyResolution>
  </MSTest>

</RunSettings>
```

## <a name="specify-environment-variables-in-the-runsettings-file"></a>環境変数を *.runsettings* ファイルに指定する

環境変数はテスト ホストとの直接の対話処理が可能な *.runsettings* ファイルに設定できます。 *DOTNET_ROOT* のような環境変数の設定を必要とする単純ではないプロジェクトをサポートするには、 *.runsettings* ファイルに環境変数を指定する必要があります。 これらの変数は、テスト ホスト プロセスの生成中に設定され、ホストで使用できます。

### <a name="example"></a>例

次のコードは、環境変数を渡すサンプルの *.runsettings* ファイルです。

```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- File name extension must be .runsettings -->
<RunSettings>
  <RunConfiguration>
    <EnvironmentVariables>
      <!-- List of environment variables we want to set-->
      <DOTNET_ROOT>C:\ProgramFiles\dotnet</DOTNET_ROOT>
      <SDK_PATH>C:\Codebase\Sdk</SDK_PATH>
    </EnvironmentVariables>
  </RunConfiguration>
</RunSettings>
```

**RunConfiguration** ノードには、**EnvironmentVariables** ノードが含まれている必要があります。 環境変数は、要素名とその値として指定できます。

> [!NOTE]
> これらの環境変数は、テスト ホストが開始されるときに常に設定される必要があるため、テストは常に別のプロセスで実行する必要があります。 このため、テスト ホストが常に呼び出されるよう、環境変数があるときは */InIsolation* フラグが設定されます。

## <a name="see-also"></a>関連項目

- [テスト実行を構成する](https://github.com/microsoft/vstest-docs/blob/master/docs/configure.md)
- [コード カバレッジ分析のカスタマイズ](../test/customizing-code-coverage-analysis.md)
- [Visual Studio テスト タスク (Azure Test Plans)](/azure/devops/pipelines/tasks/test/vstest?view=vsts)

