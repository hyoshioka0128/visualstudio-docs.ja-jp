---
description: .Vcxproj ファイルには、Visual C++ プロジェクトシステムが使用されます。
title: Visual C++ プロジェクトの機能拡張
ms.date: 04/23/2019
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
author: corob-msft
ms.author: corob
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fc538402ae39753f14a3bccd8bcd17ddb0081078
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221237"
---
# <a name="visual-studio-c-project-system-extensibility-and-toolset-integration"></a>Visual Studio C++ プロジェクトシステムの拡張性とツールセットの統合

.Vcxproj ファイルには、Visual C++ プロジェクトシステムが使用されます。 これは、 [Visual Studio Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/Index.md) に基づいており、新しいツールセット、ビルドアーキテクチャ、およびターゲットプラットフォームの統合を容易にするために、C++ 固有の拡張ポイントが追加されています。

## <a name="c-msbuild-targets-structure"></a>C++ MSBuild ターゲット構造体

すべての .vcxproj ファイルは、次のファイルをインポートします。

```xml
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.Default.props" />
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.props" />
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />
```

これらのファイルは、単独で定義されます。 代わりに、次のプロパティ値に基づいて他のファイルをインポートします。

- `$(ApplicationType)`

   例: Windows ストア、Android、Linux

- `$(ApplicationTypeRevision)`

   この形式の有効なバージョン文字列を指定してください。 major [. build [. revision]] の形式にする必要があります。

   例: 1.0、10.0.0.0

- `$(Platform)`

   歴史的な理由を示す "Platform" という名前のビルドアーキテクチャ。

   例: Win32、x86、x64、ARM

- `$(PlatformToolset)`

   例: v140、v141、v141_xp、llvm

これらのプロパティ値では、ルートフォルダーの下にフォルダー名を指定し `$(VCTargetsPath)` ます。

> `$(VCTargetsPath)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;*アプリケーションの種類*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(ApplicationType)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(ApplicationTypeRevision)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*・*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(Platform)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*PlatformToolsets セット*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(PlatformToolset)` \
&nbsp;&nbsp;&nbsp;&nbsp;*・*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(Platform)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*PlatformToolsets セット*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(PlatformToolset)`

`$(VCTargetsPath)` \\ *プラットフォーム* \\ フォルダーは、が空のときに `$(ApplicationType)` Windows デスクトッププロジェクトに使用されます。

### <a name="add-a-new-platform-toolset"></a>新しいプラットフォームツールセットの追加

新しいツールセット (既存の win32 プラットフォームの "mytoolset セット" など) を追加するには 、 `$(VCTargetsPath)` *\\ プラットフォーム \\ Win32 \\ platformtoolsets セット \\* の下に mytoolset セットフォルダーを作成し、そこに *ツール* セットとツールセットの *.targets* ファイルを作成します。

次に示すように、 *Platformtoolsets セット* の下にある各フォルダー名は、指定したプラットフォームの使用可能な **プラットフォームツールセット** として [**プロジェクトのプロパティ**] ダイアログボックスに表示されます。

![プロジェクトの [プロパティページ] ダイアログボックスの [プラットフォームツールセット] プロパティ](media/vc-project-extensibility-platform-toolset-property.png "プロジェクトの [プロパティページ] ダイアログボックスの [プラットフォームツールセット] プロパティ")

このツールセットでサポートされている既存の各プラットフォームフォルダーに、同様の *Mytoolset セット* フォルダーと *ツール* セットファイルと *ツール* セットファイルを作成します。

### <a name="add-a-new-platform"></a>新しいプラットフォームを追加する

"Myplatform" などの新しいプラットフォームを追加するには、[プラットフォーム `$(VCTargetsPath)` *\\ \\*] の下に myplatform フォルダーを作成し、その中に *platform.object*、 *platform.object、* および *platform.object* の各ファイルを作成します。 また、 `$(VCTargetsPath)` *\\ プラットフォーム \\*<strong><em>myplatform</em></strong>*\\ platformtoolsets セット \\* フォルダーを作成し、その中に少なくとも1つのツールセットを作成します。

各の *プラットフォーム* フォルダーにあるすべてのフォルダー名は、 `$(ApplicationType)` プロジェクトに `$(ApplicationTypeRevision)` 使用できる **プラットフォーム** の選択肢として IDE に表示されます。

![[新しいプロジェクトプラットフォーム] ダイアログボックスでの新しいプラットフォームの選択](media/vc-project-extensibility-new-project-platform.png "[新しいプロジェクトプラットフォーム] ダイアログボックスでの新しいプラットフォームの選択")

### <a name="add-a-new-application-type"></a>新しいアプリケーションの種類の追加

新しいアプリケーションの種類を追加するには 、アプリケーションの種類 `$(VCTargetsPath)` *\\ \\* の下に myapplicationtype フォルダーを作成し、その中に *既定の. props* ファイルを作成します。 アプリケーションの種類には少なくとも1つのリビジョンが必要であるため、アプリケーションの種類として `$(VCTargetsPath)` *\\ \\ myapplicationtype \\ 1.0* フォルダーを作成し、その中に *既定の. props* ファイルを作成します。 また、 `$(VCTargetsPath)` *\\ applicationtype \\ myapplicationtype \\ \\ 1.0* platform フォルダーを作成し、その中に少なくとも1つのプラットフォームを作成する必要があります。

`$(ApplicationType)``$(ApplicationTypeRevision)`プロパティとプロパティは、ユーザーインターフェイスに表示されません。 これらはプロジェクトテンプレートで定義され、プロジェクトの作成後に変更することはできません。

## <a name="the-vcxproj-import-tree"></a>.Vcxproj インポートツリー

Microsoft C++ props およびターゲットファイルのインポートの簡略化されたツリーは次のようになります。

> `$(VCTargetsPath)`\\*Microsoft .Cpp. 既定値. props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(MSBuildExtensionsPath)`\\`$(MSBuildToolsVersion)`\\*Microsoft. 共通* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Importbefore* \\*既定値* \\ \* 。*props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*アプリケーションの種類* \\ `$(ApplicationType)` \\*既定の props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*アプリケーション* \\ `$(ApplicationType)` \\ の `$(ApplicationTypeRevision)` 種類 \\*既定の props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*アプリケーション* \\ `$(ApplicationType)` \\ の `$(ApplicationTypeRevision)` 種類 \\ \\ `$(Platform)` プラットフォーム \\*Platform. 既定値. props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Importafter* \\*既定値* \\ \* 。*props*

Windows デスクトッププロジェクトでは定義されない `$(ApplicationType)` ため、インポートのみ

> `$(VCTargetsPath)`\\*Microsoft .Cpp. 既定値. props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(MSBuildExtensionsPath)`\\`$(MSBuildToolsVersion)`\\*Microsoft. 共通* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Importbefore* \\*既定値* \\ \* 。*props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\ \\ `$(Platform)` プラットフォーム \\*Platform. 既定値. props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Importafter* \\*既定値* \\ \* 。*props*

このプロパティを使用して、 `$(_PlatformFolder)` プラットフォームフォルダーの場所を保持し `$(Platform)` ます。 このプロパティはです。

> `$(VCTargetsPath)`\\ *・*\\`$(Platform)`

Windows デスクトップアプリの場合

> `$(VCTargetsPath)`\\*アプリケーション* \\ `$(ApplicationType)` \\ の `$(ApplicationTypeRevision)` 種類 \\*プラットフォーム*\\`$(Platform)`

それ以外のすべての場合。

Props ファイルは、次の順序でインポートされます。

> `$(VCTargetsPath)`\\*Microsoft .Cpp. props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Platform.object* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft .Cpp. Platform.object* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Importbefore* \\ \* 。*props* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Platformtoolsets セット* \\ `$(PlatformToolset)` \\*ツールセット. props* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Importafter* \\ \* 。*props*

ターゲットファイルは、次の順序でインポートされます。

> `$(VCTargetsPath)`\\*Microsoft .Cpp. ターゲット* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft .Cpp. Current. targets* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Platform.object* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft .Cpp. Platform.object* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Importbefore* \\ \* 。*ターゲット* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Platformtoolsets セット* \\ `$(PlatformToolset)` \\*ツールセット。ターゲット* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Importafter* \\ \* 。*ターゲット*

ツールセットのいくつかの既定のプロパティを定義する必要がある場合は、適切な ImportBefore および Importbefore フォルダーにファイルを追加できます。

## <a name="author-toolsetprops-and-toolsettargets-files"></a>ツールセットとツールセットの .targets ファイルを作成する

*ツールセット* とツールセットの *.targets* ファイルは、このツールセットの使用時にビルド中に発生する処理を完全に制御します。 また、使用可能なデバッガー、一部の IDE ユーザーインターフェイス ([ **プロパティページ** ] ダイアログの内容など)、およびプロジェクトの動作の他の側面を制御することもできます。

ツールセットはビルドプロセス全体をオーバーライドできますが、通常は、ツールセットでビルドステップを変更または追加するか、または既存のビルドプロセスの一部として別のビルドツールを使用する必要があります。 この目標を達成するために、ツールセットでインポートできる一般的なプロパティとターゲットファイルが多数あります。 ツールセットで実行する内容に応じて、これらのファイルをインポートまたは例として使用すると便利な場合があります。

- `$(VCTargetsPath)`\\*Microsoft. CppCommon. ターゲット*

  このファイルは、ネイティブビルドプロセスの主要部分を定義し、次のインポートも行います。

  - `$(VCTargetsPath)`\\*Microsoft. CppBuild. ターゲット*

  - `$(VCTargetsPath)`\\*Microsoft. BuildSteps. targets*

  - `$(MSBuildToolsPath)`\\*Microsoft. 共通ターゲット*

- `$(VCTargetsPath)`\\*Microsoft .Cpp. のプロパティ*

   Microsoft コンパイラとターゲットウィンドウを使用するツールセットの既定値を設定します。

- `$(VCTargetsPath)`\\*Microsoft .Cpp. WindowsSDK. props*

   このファイルによって Windows SDK の場所が決定され、Windows を対象とするアプリの重要なプロパティがいくつか定義されます。

### <a name="integrate-toolset-specific-targets-with-the-default-c-build-process"></a>ツールセット固有のターゲットを既定の C++ ビルドプロセスと統合する

既定の C++ ビルドプロセスは、 *Microsoft. CppCommon. ターゲット* で定義されています。 ターゲットは、特定のビルドツールを呼び出しません。これらは、主要なビルドステップ、順序、および依存関係を指定します。

C++ のビルドには、次のターゲットで表される3つの主要な手順があります。

- `BuildGenerateSources`

- `BuildCompile`

- `BuildLink`

各ビルドステップは個別に実行される可能性があるため、1つのステップで実行されるターゲットは、別の手順の一部として実行されるターゲットに定義されている項目グループおよびプロパティに依存することはできません。 この分割により、特定のビルドパフォーマンスの最適化が可能になります。 既定では使用されませんが、この分離に従うことをお勧めします。

各ステップ内で実行されるターゲットは、次のプロパティによって制御されます。

- `$(BuildGenerateSourcesTargets)`

- `$(BuildCompileTargets)`

- `$(BeforeBuildLinkTargets)`

各ステップには、プロパティの前後にもあります。

```xml
<Target
  Name="_BuildGenerateSourcesAction"
  DependsOnTargets="$(CommonBuildOnlyTargets);$(BeforeBuildGenerateSourcesTargets);$(BuildGenerateSourcesTargets);$(AfterBuildGenerateSourcesTargets)" />

<Target
  Name="\_BuildCompileAction"
  DependsOnTargets="$(CommonBuildOnlyTargets);$(BeforeBuildCompileTargets);$(BuildCompileTargets);$(AfterBuildCompileTargets)" />

<Target
  Name="\_BuildLinkAction"
  DependsOnTargets="$(CommonBuildOnlyTargets);$(BeforeBuildLinkTargets);$(BuildLinkTargets);$(AfterBuildLinkTargets)" />
```

各手順に含まれるターゲットの例については、「 *Microsoft. CppBuild. .targets* ファイル」を参照してください。

```xml
<BuildCompileTargets Condition="'$(ConfigurationType)'\!='Utility'">
  $(BuildCompileTargets);
  _ClCompile;
  _ResGen;
  _ResourceCompile;
  $(BuildLibTargets);
</BuildCompileTargets>
```

などのターゲットを確認すると、それ `_ClCompile` 自体には何も行われませんが、代わりに次のような他のターゲットに依存していることがわかります `ClCompile` 。

```xml
<Target Name="_ClCompile"
  DependsOnTargets="$(BeforeClCompileTargets);$(ComputeCompileInputsTargets);MakeDirsForCl;ClCompile;$(AfterClCompileTargets)" >
</Target>
```

`ClCompile` およびその他のビルドツール固有のターゲットは、 *Microsoft. CppBuild. ターゲット* の空のターゲットとして定義されます。

```xml
<Target Name="ClCompile"/>
```

`ClCompile`ターゲットは空であるため、ツールセットによってオーバーライドされない限り、実際のビルドアクションは実行されません。 ツールセットターゲットは、ターゲットをオーバーライドすることができます。 `ClCompile` つまり、次のように、 `ClCompile` *Microsoft. cppbuild. ターゲット* をインポートした後に、別の定義を含めることができます。

```xml
<Target Name="ClCompile"
  Condition="'@(ClCompile)' != ''"
  DependsOnTargets="SelectClCompile">
  <!-- call some MSBuild tasks -->
</Target>
```

Visual Studio がクロスプラットフォームサポートを実装する前に作成された名前で `ClCompile` も、ターゲットは CL.exe を呼び出す必要がありません。 また、適切な MSBuild タスクを使用して、Clang、gcc、またはその他のコンパイラを呼び出すこともできます。

ターゲットは、 `ClCompile` `SelectClCompile` 1 つのファイルのコンパイルコマンドが IDE で動作するために必要なターゲット以外の依存関係を持つことはできません。

## <a name="msbuild-tasks-to-use-in-toolset-targets"></a>ツールセットターゲットで使用する MSBuild タスク

実際のビルドツールを呼び出すには、ターゲットが MSBuild タスクを呼び出す必要があります。 実行するコマンドラインを指定できる基本的な [Exec タスク](../msbuild/exec-task.md) があります。 ただし、通常、ビルドツールには多くのオプション、入力があります。 とはインクリメンタルビルドを追跡するための出力であるため、これらに対して特別なタスクを行うことをお勧めします。 たとえば、タスクは `CL` MSBuild プロパティを CL.exe スイッチに変換し、応答ファイルに書き込み、CL.exe を呼び出します。 また、後でインクリメンタルビルドを行うために、すべての入力ファイルと出力ファイルを追跡します。 詳細については、「 [インクリメンタルビルドと](#incremental-builds-and-up-to-date-checks)最新のチェック」を参照してください。

Microsoft.Cpp.Common.Tasks.dll には、次のタスクが実装されています。

- `BSCMake`

- `CL`

- `ClangCompile` (clang-gcc スイッチ)

- `LIB`

- `LINK`

- `MIDL`

- `Mt`

- `RC`

- `XDCMake`

- `CustomBuild` (Exec と同じですが、入力と出力の追跡があります)

- `SetEnv`

- `GetOutOfDateItems`

既存のツールと同じアクションを実行するツールがあり、それに類似したコマンドラインスイッチ (clang-cl および CL do) がある場合は、両方に同じタスクを使用できます。

ビルドツールの新しいタスクを作成する必要がある場合は、次のいずれかのオプションを選択できます。

1. このタスクをめったに使用しない場合、または数秒でビルドに関係がない場合は、MSBuild のインラインタスクを使用できます。

   - Xaml タスク (カスタムビルド規則)

     Xaml タスク宣言の一例については、「buildcustomizationsmasm.xml」を参照してください。 `$(VCTargetsPath)` \\  \\ ** その使用方法については、「 `$(VCTargetsPath)` \\ *buildcustomizations* \\ *masm. targets*」を参照してください。

   - [コードタスク](../msbuild/msbuild-inline-tasks.md)

1. タスクのパフォーマンスを向上させる必要がある場合、またはより複雑な機能が必要な場合は、通常の MSBuild [タスク書き込み](../msbuild/task-writing.md) プロセスを使用します。

   、、およびの場合と同様に、ツールのすべての入力と出力がツールのコマンドラインに一覧表示されない場合は、 `CL` `MIDL` `RC` 自動入力および出力ファイルの追跡と tlog ファイルの作成が必要な場合は、クラスからタスクを派生させます `Microsoft.Build.CPPTasks.TrackedVCToolTask` 。 現時点では、基本 [Tooltask](/dotnet/api/microsoft.build.utilities.tooltask) クラスに関するドキュメントがありますが、クラスの詳細についての例やドキュメントはありません `TrackedVCToolTask` 。 これが特に興味深い場合は、 [開発者コミュニティ](https://aka.ms/feedback/suggest?space=62)でお客様の声を要求に追加してください。

## <a name="incremental-builds-and-up-to-date-checks"></a>インクリメンタルビルドと最新チェック

既定の MSBuild インクリメンタルビルドターゲットは、 `Inputs` 属性と属性を使用し `Outputs` ます。 これらを指定すると、MSBuild は、入力のいずれかがすべての出力よりも新しいタイムスタンプを持つ場合にのみターゲットを呼び出します。 多くの場合、ソースファイルには他のファイルが含まれているかインポートされており、ビルドツールはツールのオプションに応じて異なる出力を生成するため、MSBuild ターゲットで使用可能なすべての入力と出力を指定するのは困難です。

この問題を管理するために、C++ のビルドでは、インクリメンタルビルドをサポートするためにさまざまな手法を使用します。 ほとんどのターゲットは入力と出力を指定せず、その結果、ビルド中に常に実行されます。 ターゲットによって呼び出されるタスクは、すべての入力と出力に関する情報を、tlog 拡張子を持つ *tlog* ファイルに書き込みます。 この tlog ファイルは、変更されたものと再構築が必要なもの、最新のものを確認するために、後のビルドで使用されます。 また、このファイルは、IDE の既定のビルドの最新チェックに使用される唯一のソースです。

すべての入力と出力を確認するために、ネイティブツールタスクは tracker.exe と MSBuild によって提供される [Filetracker](/dotnet/api/microsoft.build.utilities.filetracker) クラスを使用します。

Microsoft.Build.CPPTasks.Common.dll は、 `TrackedVCToolTask` パブリック抽象基本クラスを定義します。 ほとんどのネイティブツールタスクは、このクラスから派生します。

Visual Studio 2017 更新プログラム15.8 以降では、Microsoft.Cpp.Common.Tasks.dll に実装されているタスクを使用して、 `GetOutOfDateItems` 既知の入力と出力を持つカスタムターゲットの tlog ファイルを作成できます。
または、タスクを使用して作成することもでき `WriteLinesToFile` ます。 `_WriteMasmTlogs` `$(VCTargetsPath)` \\  \\ 例として、buildcustomizations *masm* のターゲットを参照してください。

## <a name="tlog-files"></a>tlog ファイル

Tlog ファイルには、 *読み取り*、 *書き込み*、および *コマンドライン* の3種類があります。 ファイルの読み取りと書き込みは、インクリメンタルビルドと IDE の最新チェックによって使用されます。 コマンドラインの tlog ファイルは、インクリメンタルビルドでのみ使用されます。

MSBuild では、次のヘルパークラスを使用して、tlog ファイルの読み取りと書き込みを行うことができます。

- [CanonicalTrackedInputFiles](/dotnet/api/microsoft.build.utilities.canonicaltrackedinputfiles)

- [CanonicalTrackedOutputFiles](/dotnet/api/microsoft.build.utilities.canonicaltrackedoutputfiles)

[FlatTrackingData](/dotnet/api/microsoft.build.utilities.flattrackingdata)クラスを使用すると、読み取りと書き込みの両方のファイルにアクセスし、出力より新しい入力を識別できます。または、出力がない場合はを指定できます。 最新のチェックで使用されます。

コマンドラインの tlog ファイルには、ビルドで使用されるコマンドラインに関する情報が含まれています。 これらは増分ビルドに対してのみ使用され、最新のチェックは行われません。そのため、内部形式は、それらを生成する MSBuild タスクによって決定されます。

### <a name="read-tlog-format"></a>Tlog 形式を読み取ります。

 Tlog ファイル ( \* . read. \* .tlog) には、ソースファイルとその依存関係に関する情報が含まれています。

**^** 行の先頭にあるカレット () は、1つ以上のソースを示します。 同じ依存関係を共有するソースは、縦棒 () で区切られ **\|** ます。

依存関係ファイルは、ソースの後にそれぞれ独自の行で一覧表示されます。 すべてのファイル名は完全パスです。

たとえば、プロジェクトソースが *F: \\ test \\ ConsoleApplication1 \\ ConsoleApplication1* にあるとします。 ソースファイル ( *Class1*) に次のものが含まれている場合、

```cpp
#include "stdafx.h" //precompiled header
#include "Class1.h"
```

次に *、ソース* ファイルとその後に2つの依存関係が含まれます。

```tlog
^F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\CLASS1.CPP
F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.PCH
F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\CLASS1.H
```

大文字でファイル名を書き込む必要はありませんが、一部のツールでは便利です。

### <a name="write-tlog-format"></a>Tlog 形式の書き込み

 Tlog ( \* . write. \* .tlog) ファイルは、ソースと出力を接続します。

**^** 行の先頭にあるカレット () は、1つ以上のソースを示します。 複数のソースは、縦棒 () で区切られ **\|** ます。

ソースから作成された出力ファイルは、ソースの後にそれぞれの行に表示されます。 すべてのファイル名は完全なパスである必要があります。

たとえば、追加のソースファイル *Class1* を持つ単純な consoleapplication プロジェクトの場合、次のよう *なファイルが含まれている* 可能性があります。

```tlog
^F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CLASS1.OBJ|F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.OBJ|F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\STDAFX.OBJ
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.ILK
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.EXE
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.PDB
```

## <a name="design-time-build"></a>デザイン時ビルド

IDE では、.vcxproj プロジェクトは一連の MSBuild ターゲットを使用して、プロジェクトから追加情報を取得し、出力ファイルを再生成します。 これらのターゲットの一部は、デザイン時ビルドでのみ使用されますが、その多くは、通常のビルドとデザイン時のビルドの両方で使用されます。

デザイン時ビルドに関する一般的な情報については、 [デザイン時ビルド](https://github.com/dotnet/project-system/blob/master/docs/design-time-builds.md)の CPS ドキュメントを参照してください。 このドキュメントは、Visual C++ プロジェクトにのみ適用されます。

`CompileDesignTime`デザイン時のビルドドキュメントに記載されているとのターゲットは、 `Compile` .vcxproj プロジェクトに対しては実行されません。 Visual C++ .vcxproj プロジェクトは、さまざまなデザイン時のターゲットを使用して、IntelliSense 情報を取得します。

### <a name="design-time-targets-for-intellisense-information"></a>IntelliSense 情報のデザイン時ターゲット

.Vcxproj プロジェクトで使用されるデザイン時のターゲットは、デザイン時で定義されています。 `$(VCTargetsPath)` \\ 

ターゲットは、 `GetClCommandLines` IntelliSense のコンパイラオプションを収集します。

```xml
<Target
  Name="GetClCommandLines"
  Returns="@(ClCommandLines)"
  DependsOnTargets="$(DesignTimeBuildInitTargets);$(ComputeCompileInputsTargets)">
```

- `DesignTimeBuildInitTargets` –デザイン時のビルドの初期化に必要な、デザイン時のみのターゲット。 特に、これらのターゲットは、パフォーマンスを向上させるために通常のビルド機能の一部を無効にします。

- `ComputeCompileInputsTargets` –コンパイラオプションと項目を変更するターゲットのセット。 これらのターゲットは、デザイン時と通常のビルドの両方で実行されます。

ターゲットはタスクを呼び出して、 `CLCommandLine` IntelliSense に使用するコマンドラインを作成します。 この場合も、名前にかかわらず、CL オプションだけでなく、Clang オプションと gcc オプションも処理できます。 コンパイラスイッチの型は、プロパティによって制御され `ClangMode` ます。

現在、タスクによって生成されるコマンドラインは、 `CLCommandLine` IntelliSense エンジンが解析しやすくなるため、常に (Clang モードでも) CL スイッチを使用しています。

コンパイル前に実行されるターゲットを追加する場合は、標準またはデザイン時のどちらでも、デザイン時のビルドが中断されないようにするか、パフォーマンスに影響を与えないようにしてください。 ターゲットをテストする最も簡単な方法は、開発者コマンドプロンプトを開き、次のコマンドを実行することです。

```
msbuild /p:SolutionDir=*solution-directory-with-trailing-backslash*;Configuration=Debug;Platform=Win32;BuildingInsideVisualStudio=true;DesignTimebuild=true /t:\_PerfIntellisenseInfo /v:d /fl /fileloggerparameters:PerformanceSummary \*.vcxproj
```

このコマンドを実行すると、詳細なビルドログ ( *msbuild.exe*) が生成されます。このログには、最後のターゲットとタスクのパフォーマンスの概要が示されます。

`Condition ="'$(DesignTimeBuild)' != 'true'"`デザイン時のビルドではなく、通常のビルドにのみ意味を持つすべての操作でを使用してください。

### <a name="design-time-targets-that-generate-sources"></a>ソースを生成するデザイン時ターゲット

*この機能はデスクトップネイティブプロジェクトでは既定で無効になっており、キャッシュされたプロジェクトでは現在サポートされていません*。

`GeneratorTarget`プロジェクト項目に対してメタデータが定義されている場合、プロジェクトが読み込まれるときとソースファイルが変更されるときの両方で、ターゲットが自動的に実行されます。

::: moniker range="vs-2017"

たとえば、.xaml ファイルから .cpp ファイルまたは .h ファイルを自動的に生成するために、 `$(VSInstallDir)` \\ *MSBuild* \\ *microsoft* \\ *windowsxaml* \\ *v 15.0* \\ \* \\ ファイルでは次のエンティティが定義されています。

::: moniker-end

::: moniker range=">=vs-2019"

たとえば、.xaml ファイルから .cpp ファイルまたは .h ファイルを自動的に生成するために、 `$(VSInstallDir)` \\ *MSBuild* \\ *microsoft* \\ *windowsxaml* \\ *v 16.0* \\ \* \\ ファイルでは次のエンティティが定義されています。

::: moniker-end

```xml
<ItemDefinitionGroup>
  <Page>
    <GeneratorTarget>DesignTimeMarkupCompilation</GeneratorTarget>
  </Page>
  <ApplicationDefinition>
    <GeneratorTarget>DesignTimeMarkupCompilation</GeneratorTarget>
  </ApplicationDefinition>
</ItemDefinitionGroup>
<Target Name="DesignTimeMarkupCompilation">
  <!-- BuildingProject is used in Managed builds (always true in Native) -->
  <!-- DesignTimeBuild is used in Native builds (always false in Managed) -->
  <CallTarget Condition="'$(BuildingProject)' != 'true' Or $(DesignTimeBuild) == 'true'" Targets="DesignTimeMarkupCompilationCT" />
</Target>
```

を使用し `Task.HostObject` てソースファイルの保存されていないコンテンツを取得するには、ターゲットとタスクを、pkgdef 内の特定のプロジェクトの [MsbuildHostObjects](/dotnet/api/microsoft.visualstudio.shell.interop.ivsmsbuildhostobject?view=visualstudiosdk-2017&preserve-view=true) として登録する必要があります。

```reg
\[$RootKey$\\Projects\\{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}\\MSBuildHostObjects\]
\[$RootKey$\\Projects\\{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}\\MSBuildHostObjects\\DesignTimeMarkupCompilationCT;CompileXaml\]
@="{83046B3F-8984-444B-A5D2-8029DEE2DB70}"
```

## <a name="visual-c-project-extensibility-in-the-visual-studio-ide"></a>Visual Studio IDE でのプロジェクト拡張機能の Visual C++

Visual C++ プロジェクトシステムは、 [VS プロジェクトシステム](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/Index.md)に基づいており、その機能拡張ポイントを使用します。 ただし、プロジェクト階層の実装は Visual C++ に固有であり、CPS に基づくものではないため、階層の拡張性はプロジェクト項目に限定されます。

### <a name="project-property-pages"></a>[プロジェクト プロパティ] ページ

一般的な設計情報については、「 [VC + + プロジェクトのフレームワークのマルチターゲット](https://devblogs.microsoft.com/visualstudio/framework-multi-targeting-for-vc-projects/)」を参照してください。

簡単に言うと、C++ プロジェクトの [プロジェクトの **プロパティ** ] ダイアログに表示されるプロパティページは、 *規則* ファイルによって定義されます。 ルールファイルでは、プロパティページに表示する一連のプロパティを指定します。また、プロジェクトファイルに保存するプロパティを指定します。 ルールファイルは、Xaml 形式を使用する .xml ファイルです。 これらの型をシリアル化するために使用される型については、 [「」を参照して](/dotnet/api/microsoft.build.framework.xamltypes)ください。 プロジェクトでの規則ファイルの使用の詳細については、「 [プロパティページの XML 規則ファイル](/cpp/build/reference/property-page-xml-files)」を参照してください。

規則ファイルを項目グループに追加する必要があり `PropertyPageSchema` ます。

```xml
<ItemGroup>
  <PropertyPageSchema Include="$(VCTargetsPath)$(LangID)\general.xml;"/>
  <PropertyPageSchema Include="$(VCTargetsPath)$(LangID)\general_file.xml">
    <Context>File</Context>
  </PropertyPageSchema>
</ItemGroup>
```

`Context` メタデータ制限ルールの可視性は、ルールの種類によっても制御され、次のいずれかの値を持つことができます。

`Project` | `File` | `PropertySheet`

CPS は、コンテキスト型の他の値をサポートしますが、Visual C++ プロジェクトでは使用されません。

ルールを複数のコンテキストで表示する必要がある場合は、次に示すように、セミコロン (**;**) を使用してコンテキスト値を区切ります。

```xml
<PropertyPageSchema Include="$(MyFolder)\MyRule.xml">
  <Context>Project;PropertySheet</Context>
</PropertyPageSchema>
```

#### <a name="rule-format-and-main-types"></a>規則の形式と主な種類

規則の形式は簡単であるため、このセクションでは、ユーザーインターフェイスでの規則の表示方法に影響する属性についてのみ説明します。

```xml
<Rule
  Name="ConfigurationGeneral"
  DisplayName="General"
  PageTemplate="generic"
  Description="General"
  xmlns="http://schemas.microsoft.com/build/2009/properties">
```

属性は、 `PageTemplate` [ **プロパティページ** ] ダイアログボックスでのルールの表示方法を定義します。 属性には、次のいずれかの値を指定できます。

| 属性 | 説明 |
|------------| - |
| `generic` | すべてのプロパティは、[カテゴリ見出し] の下の1ページに表示されます。<br/>ルールは、コンテキストおよびコンテキストでは表示できますが、表示することはでき `Project` `PropertySheet` ません `File` 。<br/><br/> 例: `$(VCTargetsPath)` \\ *1033* \\ *general.xml* |
| `tool` | カテゴリはサブページとして表示されます。<br/>ルールは `Project` 、、、およびのすべてのコンテキストで表示できます `PropertySheet` `File` 。<br/>規則がプロジェクトのプロパティに表示されるのは、その `ItemType` `Rule.DataSource` 規則名が項目グループに含まれていない場合に、プロジェクトにで定義されたを持つ項目がある場合のみです `ProjectTools` 。<br/><br/>例: `$(VCTargetsPath)` \\ *1033* \\ *clang.xml* |
| `debugger` | ページは、[デバッグ] ページの一部として表示されます。<br/>カテゴリは現在無視されています。<br/>ルール名は、デバッグランチャー MEF オブジェクトの属性と一致している必要があり `ExportDebugger` ます。<br/><br/>例: `$(VCTargetsPath)` \\ *1033* \\ *デバッガー \_ ローカル \_windows.xml* |
| *ショー* | カスタムテンプレート。 テンプレートの名前は、MEF オブジェクトの属性と一致している必要があり `ExportPropertyPageUIFactoryProvider` `PropertyPageUIFactoryProvider` ます。 「 **VisualStudio. IPropertyPageUIFactoryProvider**」を参照してください。<br/><br/> 例: `$(VCTargetsPath)` \\ *1033* \\ *userMacros.xml* |

ルールでプロパティグリッドベースのテンプレートの1つを使用している場合は、次の機能拡張ポイントをそのプロパティに使用できます。

- [プロパティ値エディター](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/property_value_editors.md)

- [動的列挙値プロバイダー](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDynamicEnumValuesProvider.md)

#### <a name="extend-a-rule"></a>ルールを拡張する

既存の規則を使用するが、いくつかのプロパティだけを追加または削除する必要がある場合は、 [拡張規則](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/extending_rules.md)を作成できます。

#### <a name="override-a-rule"></a>ルールを上書きする

ほとんどの場合、ツールセットでほとんどのプロジェクトの既定の規則を使用しますが、そのうちの1つまたは一部を置き換えることができます。 たとえば、C/c + + の規則のみを変更して、異なるコンパイラスイッチを表示したいとします。 既存の規則と同じ名前と表示名を持つ新しい規則を指定し、 `PropertyPageSchema` 既定の cpp ターゲットのインポート後に項目グループに含めることができます。 プロジェクトでは、指定した名前の規則が1つだけ使用され、項目グループに含まれる最後の規則が優先され `PropertyPageSchema` ます。

#### <a name="project-items"></a>プロジェクト項目

*ProjectItemsSchema.xml* ファイルは、 `ContentType` `ItemType` プロジェクト項目として扱われる項目のおよびの値を定義し、 `FileExtension` 新しいファイルの追加先となる項目グループを決定する要素を定義します。

既定の ProjectItemsSchema ファイルは `$(VCTargetsPath)` \\ *1033* \\ *ProjectItemsSchema.xml* にあります。 拡張するには、 *MyProjectItemsSchema.xml* のように、新しい名前でスキーマファイルを作成する必要があります。

```xml
<ProjectSchemaDefinitions xmlns="http://schemas.microsoft.com/build/2009/properties">

  <ItemType Name="MyItemType" DisplayName="C/C++ compiler"/>

  <ContentType
    Name="MyItems"
    DisplayName="My items"
    ItemType=" MyItemType ">
  </ContentType>

  <FileExtension Name=".abc" ContentType=" MyItems"/>

</ProjectSchemaDefinitions>
```

次に、ターゲットファイルに以下を追加します。

```xml
<ItemGroup>
  <PropertyPageSchema Include="MyProjectItemsSchema.xml"/>
</ItemGroup>
```

例: `$(VCTargetsPath)` \\ *buildcustomizations* \\ *masm.xml*

### <a name="debuggers"></a>デバッガー

Visual Studio のデバッグサービスは、デバッグエンジンの機能拡張をサポートしています。 詳細については、次のサンプルを参照してください。

- [Lldb デバッグをサポートする MIEngine のオープンソースプロジェクト](https://github.com/Microsoft/MIEngine)

- [Visual Studio デバッグエンジンのサンプル](https://code.msdn.microsoft.com/windowsdesktop/Visual-Studio-Debug-Engine-c2e21c0e)

デバッグセッションのデバッグエンジンとその他のプロパティを指定するには、 [デバッグランチャー](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDebugLaunchProvider.md) MEF コンポーネントを実装し、ルールを追加する必要があり `debugger` ます。 例については、 `$(VCTargetsPath)` \\ 1033 \\ デバッガー \_ ローカル \_windows.xml ファイルを参照してください。

### <a name="deploy"></a>配置

.vcxproj プロジェクトは、Visual Studio のプロジェクトシステムの拡張機能を使用して、 [プロバイダーを配置](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDeployProvider.md)します。

### <a name="build-up-to-date-check"></a>最新のチェックをビルドする

既定では、ビルドの最新のチェックでは、 `$(TlogLocation)` すべてのビルド入力と出力のビルド時にフォルダーに作成される tlog ファイルと書き込みファイルが必要です。

カスタムの最新のチェックを使用するには、次のようにします。

1. `NoVCDefaultBuildUpToDateCheckProvider`*ツールセットの .targets* ファイルに機能を追加して、既定の最新のチェックを無効にします。

   ```xml
   <ItemGroup>
     <ProjectCapability Include="NoVCDefaultBuildUpToDateCheckProvider" />
   </ItemGroup>
   ```

1. 独自の [IBuildUpToDateCheckProvider](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IBuildUpToDateCheckProvider.md)を実装します。

## <a name="project-upgrade"></a>プロジェクトのアップグレード

### <a name="default-vcxproj-project-upgrader"></a>既定の .vcxproj プロジェクト upgrader (

既定の .vcxproj プロジェクト upgrader (は、、 `PlatformToolset` `ApplicationTypeRevision` 、MSBuild ツールセットのバージョン、および .net framework を変更します。 最後の2つは常に Visual Studio のバージョンの既定値に変更されますが、 `PlatformToolset` とは `ApplicationTypeRevision` 特別な MSBuild プロパティによって制御できます。

Upgrader (は、次の基準を使用して、プロジェクトをアップグレードできるかどうかを判断します。

1. およびを定義するプロジェクトでは `ApplicationType` `ApplicationTypeRevision` 、現在のバージョンよりも高いリビジョン番号を持つフォルダーが存在します。

1. 現在の `_UpgradePlatformToolsetFor_<safe_toolset_name>` ツールセットに対してプロパティが定義されていますが、その値が現在のツールセットと等しくありません。

   これらのプロパティ名では、は、 *\<safe_toolset_name>* すべての英数字以外の文字がアンダースコア () で置き換えられたツールセットの名前を表し **\_** ます。

プロジェクトをアップグレードできる場合は、 *ソリューション再ターゲット* に参加します。 詳細については、「 [IVsTrackProjectRetargeting2](/dotnet/api/microsoft.visualstudio.shell.interop.ivstrackprojectretargeting2)」を参照してください。

プロジェクトが特定のツールセットを使用する場合 **ソリューションエクスプローラー** でプロジェクト名を装飾するには、プロパティを定義 `_PlatformToolsetShortNameFor_<safe_toolset_name>` します。

`_UpgradePlatformToolsetFor_<safe_toolset_name>`プロパティ定義とプロパティ定義の例につい `_PlatformToolsetShortNameFor_<safe_toolset_name>` ては、「」を参照して *ください*。 使用例については、「」を参照してください。 `$(VCTargetPath)` \\ 

### <a name="custom-project-upgrader"></a>カスタムプロジェクト upgrader (

カスタム project upgrader (オブジェクトを使用するには、次に示すように MEF コンポーネントを実装します。

```csharp
/// </summary>
[Export("MyProjectUpgrader", typeof(IProjectRetargetHandler))]
[Export(typeof(IProjectRetargetHandler))]
[ExportMetadata("Name", "MyProjectUpgrader")]
[OrderPrecedence(20)]
[PartMetadata(ProjectCapabilities.Requires, ProjectCapabilities.VisualC)]

internal class MyProjectUpgrader: IProjectRetargetHandler
{
    // ...
}
```

コードでは、既定の .vcxproj upgrader (オブジェクトをインポートして呼び出すことができます。

```csharp
// ...
[Import("VCDefaultProjectUpgrader")]
// ...
    IProjectRetargetHandler Lazy<IProjectRetargetHandler>
    VCDefaultProjectUpgrader { get; set; }
// ...
```

`IProjectRetargetHandler` は *Microsoft.VisualStudio.ProjectSystem.VS.dll* で定義され、に似てい `IVsRetargetProjectAsync` ます。

プロパティを定義して、 `VCProjectUpgraderObjectName` カスタム upgrader (オブジェクトを使用するようにプロジェクトシステムに指示します。

```xml
<PropertyGroup>
  <VCProjectUpgraderObjectName>MyProjectUpgrader</VCProjectUpgraderObjectName>
</PropertyGroup>
```

#### <a name="disable-project-upgrade"></a>プロジェクトのアップグレードを無効にする

プロジェクトのアップグレードを無効にするには、次の値を使用し `NoUpgrade` ます。

```xml
<PropertyGroup>
  <VCProjectUpgraderObjectName>NoUpgrade</VCProjectUpgraderObjectName>
</PropertyGroup>
```

## <a name="project-cache-and-extensibility"></a>プロジェクトキャッシュと拡張性

Visual Studio 2017 で大規模な C++ ソリューションを使用するときのパフォーマンスを向上させるために、 [プロジェクトキャッシュ](https://devblogs.microsoft.com/cppblog/faster-c-solution-load-with-vs-15/) が導入されました。 これは、プロジェクトデータを格納する SQLite データベースとして実装され、MSBuild または CPS プロジェクトをメモリに読み込まずにプロジェクトを読み込むために使用されます。

.Vcxproj プロジェクトには CPS オブジェクトが存在しないため、キャッシュから読み込まれた拡張子の MEF コンポーネントは、インポート `UnconfiguredProject` または `ConfiguredProject` 作成できません。 拡張機能をサポートするために、プロジェクトが MEF 拡張を使用する (または使用する可能性がある) かどうかを Visual Studio が検出するときに、プロジェクトキャッシュは使用されません。

これらのプロジェクトの種類は常に完全に読み込まれ、メモリ内に CPS オブジェクトがあるため、すべての MEF 拡張が作成されます。

- スタートアッププロジェクト

- カスタムプロジェクトが upgrader (されている (つまり、プロパティを定義する) プロジェクト `VCProjectUpgraderObjectName`

- デスクトップウィンドウを対象としない、つまりプロパティを定義するプロジェクト `ApplicationType`

- 共有項目プロジェクト (.vcxitems) と、.vcxitems プロジェクトのインポートによってそれらを参照するすべてのプロジェクト。

これらの条件がいずれも検出されない場合は、プロジェクトキャッシュが作成されます。 キャッシュには、インターフェイスのクエリに応答するために必要な MSBuild プロジェクトのすべてのデータが含まれてい `get` `VCProjectEngine` ます。 これは、拡張機能によって実行されるファイルレベルの MSBuild props およびターゲットへの変更はすべて、キャッシュから読み込まれたプロジェクトでのみ機能する必要があることを意味します。

## <a name="shipping-your-extension"></a>拡張機能を配布する

VSIX ファイルを作成する方法の詳細については、「 [Visual Studio 拡張機能の配布](../extensibility/shipping-visual-studio-extensions.md)」を参照してください。 特別なインストール場所にファイルを追加する方法 (の下にファイルを追加する方法など) については `$(VCTargetsPath)` 、「 [extensions フォルダー以外にインストール](../extensibility/set-install-root.md)する」を参照してください。

## <a name="additional-resources"></a>その他のリソース

Microsoft Build System ([MSBuild](../msbuild/msbuild.md)) は、プロジェクトファイルのビルドエンジンと拡張可能な XML ベースの形式を提供します。 Msbuild の基本的な [概念](../msbuild/msbuild-concepts.md) と、Visual C++ プロジェクトシステムを拡張するため [の msbuild Visual C++ の](/cpp/build/reference/msbuild-visual-cpp-overview) 動作方法について理解しておく必要があります。

Managed Extensibility Framework ([MEF](/dotnet/framework/mef/)) には、CPS および Visual C++ プロジェクトシステムで使用される拡張 api が用意されています。 CPS での MEF の使用方法の概要については、「 [mef の Vsprojectsystem の概要](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/mef.md)」の「 [CPS and mef](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/mef.md#cps-and-mef) 」を参照してください。

既存のビルドシステムをカスタマイズして、ビルドステップまたは新しいファイルの種類を追加できます。 詳細については、「 [MSBuild (Visual C++) の概要](/cpp/build/reference/msbuild-visual-cpp-overview) 」および「 [プロジェクトプロパティの操作](/cpp/build/working-with-project-properties)」を参照してください。
