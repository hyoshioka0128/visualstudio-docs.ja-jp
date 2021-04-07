---
title: MSBuild によってプロジェクトがビルドされる方法
description: Visual Studio またはコマンド ラインやスクリプトから呼び出された MSBuild によってプロジェクト ファイルが処理されるしくみについて説明します。
ms.custom: SEO-VS-2020
ms.date: 05/18/2020
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, build process overview
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9bc7fe3898bec19b4eb0130e7279974823669e7f
ms.sourcegitcommit: 155d5f0fd54ac1d20df2f5b0245365924faa3565
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2021
ms.locfileid: "106082540"
---
# <a name="how-msbuild-builds-projects"></a>MSBuild によってプロジェクトがビルドされる方法

MSBuild は実際にどのように機能するのでしょうか。 この記事では、Visual Studio またはコマンド ラインやスクリプトから呼び出された MSBuild によってプロジェクト ファイルが処理される方法について説明します。 MSBuild の動作を理解することは、問題の診断やビルド プロセスのカスタマイズをより適切に行うのに役立ちます。 この記事で説明するビルド プロセスのほとんどが、すべてのプロジェクトの種類に適用されます。

完全なビルド プロセスは、プロジェクトをビルドするターゲットとタスクの[初期スタートアップ](#startup)、[評価](#evaluation-phase)、[実行](#execution-phase)で構成されます。 これらの入力に加えて、外部インポートによってビルド プロセスの詳細が定義されます。これには、*Microsoft.Common.targets* などの [標準インポート](#standard-imports)と、ソリューション レベルまたはプロジェクト レベルでの [ユーザー構成可能インポート](#user-configurable-imports)の両方が含まれます。

## <a name="startup"></a>スタートアップ

MSBuild は、Visual Studio から *Microsoft.Build.dll* の MSBuild オブジェクト モデルを通して、またはコマンド ラインやスクリプト (CI システムなど) で実行可能ファイルを直接呼び出すことによって、呼び出すことができます。 どちらの場合も、ビルド プロセスに影響を与える入力には、プロジェクト ファイル (または、Visual Studio 内部のプロジェクト オブジェクト)、場合によってはソリューション ファイル、環境変数、コマンドライン スイッチまたはオブジェクト モデルでの同等機能が含まれます。 スタートアップ フェーズの間に、コマンドライン オプションまたはオブジェクト モデルのそれに相当する機能を使用して、ロガーの構成などの MSBuild の設定を構成します。 コマンド ラインで `-property` または `-p` スイッチを使用して設定されるプロパティは、グローバル プロパティとして設定されます。これにより、後でプロジェクト ファイルが読み込まれる場合でも、プロジェクト ファイルで設定されるすべての値がオーバーライドされます。

次のセクションでは、ソリューション ファイルやプロジェクト ファイルなどの入力ファイルについて説明します。

### <a name="solutions-and-projects"></a>ソリューションとプロジェクト

MSBuild のインスタンスは、1 つのプロジェクトで構成される場合、またはソリューションの一部として多くのプロジェクトで構成される場合があります。 ソリューション ファイルは MSBuild の XML ファイルではありませんが、MSBuild では、それを解釈することにより、特定の構成とプラットフォームの設定に対してビルドする必要のあるすべてのプロジェクトが認識されます。 MSBuild によってこの XML 入力が処理されるとき、それはソリューション ビルドと呼ばれます。 それには、すべてのソリューション ビルドで何かを実行できる拡張ポイントがいくつかありますが、このビルドは個々のプロジェクト ビルドとは別に実行されるため、ソリューション ビルドでのプロパティやターゲットの定義の設定は、個々のプロジェクト ビルドには関連しません。

ソリューション ビルドを拡張する方法については、「[ソリューション ビルドをカスタマイズする](customize-your-build.md#customize-the-solution-build)」を参照してください。

### <a name="visual-studio-builds-vs-msbuildexe-builds"></a>Visual Studio でのビルドと MSBuild.exe でのビルド

Visual Studio でプロジェクトをビルドする場合と、MSBuild の実行可能ファイルを使用するか、MSBuild オブジェクト モデルを使用してビルドを開始することにより、MSBuild を直接呼び出す場合では、大きな違いがいくつかあります。 Visual Studio では、Visual Studio のビルドに対するプロジェクト ビルドの順序が管理されます。それでは、個々のプロジェクト レベルでのみ MSBuild が呼び出され、そのとき、MSBuild の動作に大きく影響する 2 つのブール型プロパティ (`BuildingInsideVisualStudio`、`BuildProjectReferences`) が設定されます。 各プロジェクトの内部では、実行は MSBuild で呼び出されたときと同じですが、参照されるプロジェクトに違いがあります。 MSBuild では、参照されているプロジェクトが必要な場合は、実際にビルドが行われます。つまり、タスクとツールが実行されて、出力が生成されます。 Visual Studio のビルドで参照されるプロジェクトが検出されると、MSBuild からはその参照されるプロジェクトからの予想される出力のみが返され、Visual Studio でそれらの他のプロジェクトのビルドを制御できるようになります。 Visual Studio によってすべてが完全に制御され、ビルドの順序の決定と、MSBuild の個別の呼び出し (必要な場合) が行われます。

ソリューション ファイルで MSBuild が呼び出されたときのもう 1 つの違いは、MSBuild によってソリューション ファイルが解析され、標準の XML 入力ファイルが作成されて評価され、プロジェクトとして実行されることです。 ソリューション ビルドは、すべてのプロジェクトの前に実行されます。 Visual Studio からのビルドでは、このような処理は行われません。MSBuild でソリューション ファイルが参照されることはありません。 その結果、ソリューション ビルドの (*before.SolutionName.sln.targets* と *after.SolutionName.sln.targets* を使用した) カスタマイズは、MSBuild.exe またはオブジェクト モデルを使用する場合にのみ適用され、Visual Studio でのビルドには適用されません。

### <a name="project-sdks"></a>プロジェクト SDK

MSBuild プロジェクト ファイルの SDK 機能は、比較的新しいものです。 この変更の前は、特定のプロジェクトの種類に対するビルド プロセスが定義されている *.targets* ファイルと *.props* ファイルが、プロジェクト ファイルによって明示的にインポートされていました。

.NET Core プロジェクトでは、それに対して適切な .NET SDK のバージョンがインポートされます。 「[.NET Core プロジェクト SDK](/dotnet/core/project-sdk/overview)」の概要と、[プロパティ](/dotnet/core/project-sdk/msbuild-props)に関するリファレンスを参照してください。

## <a name="evaluation-phase"></a>評価フェーズ

このセクションでは、これらの入力ファイルがどのように処理および解析されて、ビルドされるものを決定するメモリ内のオブジェクトが生成されるかについて説明します。

評価フェーズの目的は、入力 XML ファイルとローカル環境に基づいて、メモリ内のオブジェクト構造を作成することです。 評価フェーズは、プロジェクト XML ファイルのような入力ファイルと、通常 *.props* または *.targets* ファイルという名前 (主にプロパティを設定するか、ビルド ターゲットを定義するかによる) のインポートされた XML ファイルを処理する 6 つのパスで構成されます。 各パスでは、後のプロジェクト ビルド実行フェーズで使用されるメモリ内オブジェクトの一部がビルドされますが、評価フェーズの間に実際のビルド アクションが発生することはありません。 各パス内では、要素が出現順に処理されます。

評価フェーズのパスは次のとおりです。

- 環境変数を評価する
- インポートとプロパティを評価する
- 項目の定義を評価する
- 項目を評価する
- [UsingTask](usingtask-element-msbuild.md) 要素を評価する
- ターゲットを評価する

これらのパスの順序は大きな影響を与えるため、プロジェクト ファイルをカスタマイズするときに注意が必要です。 「[プロパティと項目の評価順序](comparing-properties-and-items.md#property-and-item-evaluation-order)」を参照してください。

### <a name="evaluate-environment-variables"></a>環境変数を評価する

このフェーズでは、環境変数を使用して同等のプロパティが設定されます。 たとえば、PATH 環境変数は、プロパティ `$(PATH)` として使用できるようになります。 コマンド ラインまたはスクリプトから実行されるときは、コマンド環境が通常どおりに使用され、Visual Studio から実行されるときは、Visual Studio の起動時に有効になっている環境が使用されます。

### <a name="evaluate-imports-and-properties"></a>インポートとプロパティを評価する

このフェーズでは、入力 XML 全体が読み込まれます。これには、プロジェクト ファイルとインポートのチェーン全体が含まれます。 MSBuild により、プロジェクトの XML とインポートされたすべてのファイルを表すメモリ内の XML 構造が作成されます。 この時点で、ターゲットに含まれていないプロパティが評価されて設定されます。

プロセスの初期段階ですべての XML 入力ファイルが MSBuild によって読み取られる結果、ビルド プロセスの間にそれらの入力を変更しても、現在のビルドには影響しません。

ターゲットの外部にあるプロパティは、ターゲット内のプロパティとは異なる方法で処理されます。 このフェーズでは、ターゲットの外部で定義されているプロパティのみが評価されます。

プロパティはプロパティ パスでの順序で処理されるため、入力のあるポイントでのプロパティは、入力でそれより前に出現するプロパティ値にはアクセスできますが、それより後に出現するプロパティにはアクセスできません。

項目が評価される前にプロパティが処理されるため、プロパティ パスのどの部分においても、どの項目の値にもアクセスできません。 

### <a name="evaluate-item-definitions"></a>項目の定義を評価する

このフェーズでは、[項目の定義](item-definitions.md)が解釈され、これらの定義のメモリ内表現が作成されます。

### <a name="evaluate-items"></a>項目を評価する

ターゲット内で定義されている項目の処理方法は、ターゲットの外部の項目とは異なります。 このフェーズでは、ターゲットの外部の項目と、それに関連付けられているメタデータが処理されます。  項目定義によって設定されたメタデータは、項目のメタデータ設定によってオーバーライドされます。 項目は出現順序で処理されるため、前に定義されている項目を参照することはできますが、後で出現する項目は参照できません。 項目パスはプロパティ パスの後であるため、プロパティの定義が後で出現するかどうかに関係なく、ターゲットの外部で定義されている任意のプロパティに、項目からアクセスできます。

### <a name="evaluate-usingtask-elements"></a>`UsingTask` 要素を評価する

このフェーズでは、[UsingTask](usingtask-element-msbuild.md) 要素が読み取られ、後の実行フェーズの間に使用できるようにタスクが宣言されます。

### <a name="evaluate-targets"></a>ターゲットを評価する

このフェーズでは、実行の準備として、すべてのターゲット オブジェクト構造がメモリ内に作成されます。 実際の実行は行われません。 

## <a name="execution-phase"></a>実行フェーズ

実行フェーズでは、ターゲットが並べ替えられて実行され、すべてのタスクが実行されます。 ただし最初に、ターゲット内で定義されているプロパティと項目が、出現順に 1 つのフェーズでまとめて評価されます。 特に、処理の順序が、ターゲットに含まれていないプロパティと項目の処理方法と異なります。最初にすべてのプロパティが処理された後、それとは異なるパスですべての項目が処理されます。 ターゲット内のプロパティと項目に対する変更は、それらが変更されたターゲットの後で観察できます。

### <a name="target-build-order"></a>ターゲットのビルド順序

1つのプロジェクトでは、ターゲットは順番に実行されます。 中心となる問題は、依存関係が適切な順序でターゲットのビルドに使用されるよう、すべてのもののビルド順序を決定する方法です。  

ターゲットのビルド順序は、各ターゲットで `BeforeTargets`、`DependsOnTargets`、`AfterTargets` 属性を使用して決定されます。 前のターゲットの実行中にこれらの属性で参照されているプロパティを変更することで、後のターゲットの順序を変更できます。

順序指定の規則については、「[ターゲットのビルド順序の決定](target-build-order.md#determine-the-target-build-order)」を参照してください。 プロセスは、ビルドするターゲットが含まれるスタックの構造によって決まります。 このタスクの先頭にあるターゲットの実行が開始され、それが他のものに依存している場合は、それらのターゲットがスタックの先頭にプッシュされて、それらの実行が開始されます。  依存関係のないターゲットがある場合は、完了まで実行されて、その親ターゲットが再開されます。

### <a name="project-references"></a>プロジェクト参照

MSBuild で使用できるコード パスは 2 つあり、ここで説明した通常のパスと、次のセクションで説明するグラフ オプションです。

個々のプロジェクトでは、`ProjectReference` 項目を使用して、他のプロジェクト上の依存関係を指定します。 スタックの先頭にあるプロジェクトで開始されたビルドは、共通のターゲット ファイルで定義されている標準ターゲットである `ResolveProjectReferences` ターゲットが実行されるポイントに到達します。

`ResolveProjectReferences` では、`ProjectReference` 項目を入力にして MSBuild タスクが呼び出され、出力が取得されます。 `ProjectReference` 項目は、`Reference` などのローカル項目に変換されます。 参照されているプロジェクトを処理するための実行フェーズが開始されている間 (必要に応じて、評価フェーズが最初に実行されます)、現在のプロジェクトに対する MSBuild 実行フェーズは一時停止されます。 参照されているプロジェクトは、依存プロジェクトのビルドが開始された後でのみビルドされるため、これによりプロジェクトのビルドのツリーが作成されます。

Visual Studio では、ソリューション (.sln) ファイルでプロジェクトの依存関係を作成できます。 依存関係はソリューション ファイルで指定され、ソリューションをビルドするとき、または Visual Studio の内部でビルドするときにのみ適用されます。 単独のプロジェクトをビルドする場合、この種類の依存関係は無視されます。 ソリューションの参照は、MSBuild によって `ProjectReference` 項目に変換された後、同じ方法で処理されます。

### <a name="graph-option"></a>グラフ オプション

グラフ ビルド スイッチ (`-graphBuild` または `-graph`) を指定すると、`ProjectReference` が MSBuild によって使用されるファーストクラスの概念になります。 MSBuild によって、すべてのプロジェクトが解析され、ビルド順序グラフ (プロジェクトの実際の依存関係グラフ) が構築されます。その後、このグラフが走査されて、ビルド順序が決定されます。 個別のプロジェクトのターゲットと同様に、MSBuild では、参照されているプロジェクトは、それらが依存しているプロジェクトの後でビルドされます。

## <a name="parallel-execution"></a>並列実行

マルチプロセッサのサポート (`-maxCpuCount` または `-m` スイッチ) を使用している場合は、MSBuild により、使用可能な CPU コアを使用する MSBuild プロセスであるノードが作成されます。 各プロジェクトは、使用可能なノードに送信されます。 ノード内では、個々のプロジェクト ビルドが順番に実行されます。

ブール型変数 <xref:Microsoft.Build.Tasks.MSBuild.BuildInParallel%2A> を設定することにより、タスクの並列実行を有効にすることができます。これは、MSBuild の `$(BuildInParallel)` プロパティの値に従って設定されます。 並列実行が有効なタスクの場合、作業スケジューラによってノードが管理され、作業がノードに割り当てられます。

「[MSBuild での複数のプロジェクトの並行ビルド](building-multiple-projects-in-parallel-with-msbuild.md)」を参照してください

## <a name="standard-imports"></a>標準インポート

*Microsoft.Common.props* と *Microsoft.Common.targets* はどちらも .NET プロジェクト ファイルによって (SDK 形式のプロジェクトで明示的または暗黙的に) インポートされ、Visual Studio のインストールの *MSBuild\Current\bin* フォルダーに配置されます。 C++ プロジェクトには、独自のインポート階層があります。「[C++ プロジェクトの MSBuild の内部](/cpp/build/reference/msbuild-visual-cpp-overview)」を参照してください。

*Microsoft.Common.props* ファイルによって既定値が設定されますが、オーバーライドできます。 それは、プロジェクト ファイルの先頭で (明示的または暗黙的に) インポートされます。 それにより、後で出現するプロジェクトの設定によって既定値がオーバーライドされます。

*Microsoft.Common.targets* ファイルとそれによってインポートされるターゲット ファイルでは、.NET プロジェクトの標準のビルド プロセスが定義されています。 また、ビルドのカスタマイズに使用できる拡張ポイントも提供されます。

実装では、*Microsoft.Common.targets* は *Microsoft.Common.CurrentVersion.targets* をインポートする薄いラッパーです。 このファイルには、標準プロパティの設定が含まれており、ビルド プロセスを定義する実際のターゲットが定義されています。 `Build` ターゲットはここで定義されていますが、実際には空です。 ただし、`Build` ターゲットには、実際のビルド手順を構成する個々のターゲット (`BeforeBuild`、`CoreBuild`、`AfterBuild`) を指定する `DependsOnTargets` 属性が含まれています。 `Build` ターゲットは次のように定義されています。

```xml
  <PropertyGroup>
    <BuildDependsOn>
      BeforeBuild;
      CoreBuild;
      AfterBuild
    </BuildDependsOn>
  </PropertyGroup>

  <Target
      Name="Build"
      Condition=" '$(_InvalidConfigurationWarning)' != 'true' "
      DependsOnTargets="$(BuildDependsOn)"
      Returns="@(TargetPathWithTargetPlatformMoniker)" />
```

`BeforeBuild` と `AfterBuild` は拡張ポイントです。 それらは *Microsoft.Common.CurrentVersion.targets* ファイルでは空ですが、プロジェクトで、独自の `BeforeBuild` ターゲットと `AfterBuild` ターゲットおよびメイン ビルド プロセスの前後で実行する必要があるタスクを提供できます。 `AfterBuild` は、no-op ターゲット `Build` の前に実行されます。これは、`AfterBuild` は `Build` ターゲットの `DependsOnTargets` 属性に出現しますが、それは `CoreBuild` の後で発生するためです。

`CoreBuild` ターゲットには、次のようなビルド ツールの呼び出しが含まれています。

```xml
  <PropertyGroup>
    <CoreBuildDependsOn>
      BuildOnlySettings;
      PrepareForBuild;
      PreBuildEvent;
      ResolveReferences;
      PrepareResources;
      ResolveKeySource;
      Compile;
      ExportWindowsMDFile;
      UnmanagedUnregistration;
      GenerateSerializationAssemblies;
      CreateSatelliteAssemblies;
      GenerateManifests;
      GetTargetPath;
      PrepareForRun;
      UnmanagedRegistration;
      IncrementalClean;
      PostBuildEvent
    </CoreBuildDependsOn>
  </PropertyGroup>
  <Target
      Name="CoreBuild"
      DependsOnTargets="$(CoreBuildDependsOn)">

    <OnError ExecuteTargets="_TimeStampAfterCompile;PostBuildEvent" Condition="'$(RunPostBuildEvent)'=='Always' or '$(RunPostBuildEvent)'=='OnOutputUpdated'"/>
    <OnError ExecuteTargets="_CleanRecordFileWrites"/>

  </Target>
```

次の表では、これらのターゲットについて説明します。一部のターゲットは、特定の種類のプロジェクトに対してのみ適用できます。

| Target | 説明 |
|--------|-------------|
| BuildOnlySettings | 実際のビルドのみに対する設定。MSBuild が Visual Studio によってプロジェクトの読み込みで呼び出された場合は使用されません。 |
| PrepareForBuild | ビルドの前提条件を準備します |
| PreBuildEvent | ビルドの前に実行するタスクを定義する、プロジェクトに対する拡張ポイント |
| ResolveProjectReferences | プロジェクトの依存関係を分析し、参照されているプロジェクトをビルドします |
| ResolveAssemblyReferences| 参照アセンブリを検索します。 |
| ResolveReferences | `ResolveProjectReferences` と `ResolveAssemblyReferences` で構成され、すべての依存関係を検索します |
| PrepareResources | リソース ファイルを処理します |
| ResolveKeySource| アセンブリへの署名に使用されている厳密な名前のキーと、[ClickOnce](../deployment/clickonce-security-and-deployment.md) マニフェストへの署名に使用されている証明書を解決します。 |
| Compile | コンパイラを呼び出します |
| ExportWindowsMDFile | コンパイラによって生成された WinMDModule ファイルから [WinMD](/uwp/winrt-cref/winmd-files) ファイルを生成します。 |
| UnmanagedUnregistration | 前のビルドで作成された [COM 相互運用](/dotnet/standard/native-interop/cominterop)レジストリのエントリを削除およびクリーンアップします |
| GenerateSerializationAssemblies | [sgen.exe](/dotnet/standard/serialization/xml-serializer-generator-tool-sgen-exe) を使用して、XML シリアル化アセンブリを生成します。|
| CreateSatelliteAssemblies | リソース内の一意のカルチャごとに 1 つのサテライト アセンブリを作成します。 |
| Generate Manifests | [ClickOnce](../deployment/clickonce-security-and-deployment.md) アプリケーションと配置マニフェストまたはネイティブ マニフェストを生成します。 |
| GetTargetPath | このプロジェクトのビルド生成物 (実行可能ファイルまたはアセンブリ) を含む項目とメタデータを返します。 |
| PrepareForRun | ビルド出力が変更された場合は、最終的なディレクトリにそれをコピーします。 |
| UnmanagedRegistration | [COM 相互運用](/dotnet/standard/native-interop/cominterop)のレジストリ エントリを設定します |
| IncrementalClean | 前のビルドでは生成されたが、現在のビルドでは生成されなかったファイルを削除します。 これは、インクリメンタル ビルドで `Clean` を動作させるために必要です。 |
| PostBuildEvent | ビルドの後で実行するタスクを定義する、プロジェクトに対する拡張ポイント |

前の表のターゲットの多くは、*Microsoft.CSharp.targets* などの言語固有のインポートにあります。 このファイルでは、C# .NET プロジェクトに固有の標準ビルド プロセスの手順が定義されています。 たとえば、C# コンパイラを実際に呼び出す `Compile` ターゲットが含まれています。

## <a name="user-configurable-imports"></a>ユーザーが構成可能なインポート

標準のインポートに加えて、ビルド プロセスをカスタマイズするためにユーザーが追加できるインポートがいくつかあります。

- *Directory.Build.props*
- *Directory.Build.targets*

これらのファイルは、それらの下にあるすべてのサブフォルダー内のすべてのプロジェクトに対する標準インポートによって読み取られます。 それは通常、ソリューション内のすべてのプロジェクトを制御するために設定のソリューション レベルにありますが、ファイル システムでそれより上位のドライブのルートまでのどこかに存在することもあります。

*Directory.Build.props* ファイルは *Microsoft.Common.props* によってインポートされるため、そこで定義されているプロパティをプロジェクト ファイルで使用できます。 それらをプロジェクト ファイルで再定義して、プロジェクトごとに値をカスタマイズできます。 *Directory.Build.targets* ファイルは、プロジェクト ファイルの後で読み込まれます。 通常それにはターゲットが含まれますが、ここでは、個々のプロジェクトで再定義する必要のないプロパティを定義することもできます。

## <a name="customizations-in-a-project-file"></a>プロジェクト ファイルでのカスタマイズ

Visual Studio では、**ソリューション エクスプローラー**、 **[プロパティ]** ウィンドウ、または **[プロジェクトのプロパティ]** で変更を行うとプロジェクト ファイルが更新されますが、プロジェクト ファイルを直接編集することによって独自の変更を行うこともできます。

多くのビルド動作は、MSBuild のプロパティを設定することによって構成できます。プロジェクトにローカルな設定の場合はプロジェクト ファイルで行い、プロジェクトとソリューションのフォルダー全体に対するグローバルなプロパティを設定する場合は、前のセクションで説明したように、*Directory.Build.props* ファイルを作成します。 コマンド ラインまたはスクリプトでのアドホックなビルドの場合は、コマンド ラインの `/p` オプションを使用し、MSBuild の特定の呼び出しに対してプロパティを設定することもできます。 設定できるプロパティの詳細については、「[MSBuild プロジェクトの共通プロパティ](common-msbuild-project-properties.md)」を参照してください。

## <a name="next-steps"></a>次の手順

MSBuild のプロセスには、ここで説明したもの以外にもいくつかの拡張ポイントがあります。 「[ビルドのカスタマイズ](customize-your-build.md)」を参照してください。 また、「[方法: Visual Studio ビルド処理を拡張する](how-to-extend-the-visual-studio-build-process.md)」も参照してください。

## <a name="see-also"></a>関連項目

[MSBuild](msbuild.md)
