---
title: MSBuild プロジェクトの共通プロパティ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- msbuild, common properties
- msbuild, project file properties
- ExcludeDeploymentUrl property
- project file properties (MSBuild)
ms.assetid: 9857505d-ae15-42f1-936d-6cd7fb9dd276
caps.latest.revision: 39
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1eb56d1334eb18dd5872457d032e5780a3f75eb3
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65698718"
---
# <a name="common-msbuild-project-properties"></a>MSBuild プロジェクトの共通プロパティ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

次の表は、Visual Studio プロジェクト ファイルで定義される、または MSBuild に用意されているターゲット ファイルに含まれている、使用頻度の高いプロパティを示しています。  
  
 Visual Studio のプロジェクト ファイル (.csproj、vbproj、vcxproj など) には、IDE を使用してプロジェクトをビルドするときに実行される MSBuild XML コードが含まれています。 通常、プロジェクトでは、ビルド プロセスを定義するために、1 つ以上の .targets ファイルをインポートします。 詳しくは、「[.Targets ファイル](../msbuild/msbuild-dot-targets-files.md)」をご覧ください。  
  
## <a name="list-of-common-properties-and-parameters"></a>共通のプロパティおよびパラメーター一覧  
  
|プロパティ名またはパラメーター名|説明|  
|--------------------------------|-----------------|  
|AdditionalLibPaths|コンパイラが参照アセンブリを検索する追加のフォルダーを指定します。|  
|AddModules|指定ファイル内のすべての型情報をコンパイル対象のプロジェクトで使用できるようにします。 このプロパティは、`/addModules` コンパイラ スイッチに相当します。|  
|ALToolPath|AL.exe の保存先のパスです。 このプロパティによって、AL.exe の現在のバージョンをオーバーライドし、別のバージョンを使用できます。|  
|ApplicationIcon|Win32 アイコンとして埋め込むためにコンパイラに渡す .ico アイコン ファイルです。 このプロパティは、`/win32icon` コンパイラ スイッチに相当します。|  
|ApplicationManifest|外部のユーザー アカウント制御 (UAC: User Account Control) マニフェスト情報を生成するのに使用するファイルのパスを指定します。 [!INCLUDE[windowsver](../includes/windowsver-md.md)] を対象とする Visual Studio プロジェクトにのみ適用されます。<br /><br /> ほとんどの場合、マニフェストは埋め込まれます。 ただし、登録を必要としない COM 配置または [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 配置を使用する場合は、アプリケーション アセンブリと共にインストールされる外部ファイルをマニフェストとして使用できます。 詳細については、このトピックの NoWin32Manifest プロパティを参照してください。|  
|AssemblyOriginatorKeyFile|アセンブリ (.snk または .pfx) に署名するために使用されるファイルを指定します。また、このファイルは [ResolveKeySource Task](../msbuild/resolvekeysource-task.md) に渡され、アセンブリの署名に使用される実際のキーが生成されます。|  
|AssemblySearchPaths|ビルド時に参照アセンブリを解決するときに検索する場所のリストです。 このリストでは、先頭から順に優先度が低くなるため、パスを指定する順序が意味を持ちます。|  
|AssemblyName|プロジェクトのビルド後に生成される最終的な出力アセンブリの名前です。|  
|BaseAddress|メイン出力アセンブリのベース アドレスを指定します。‎ このプロパティは、`/baseaddress` コンパイラ スイッチに相当します。|  
|BaseOutputPath|出力ファイルのベース パスを指定します。 設定されている場合、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] は `OutputPath = $(BaseOutputPath)\$(Configuration)\` を使用します。 構文例: `<BaseOutputPath>c:\xyz\bin\</BaseOutputPath>`|  
|BaseIntermediateOutputPath|すべての構成固有の中間出力ファイルが作成されるトップレベル フォルダーです。 既定値は `obj\` です。 次にコード例を示します。`<BaseIntermediateOutputPath>c:\xyz\obj\</BaseIntermediateOutputPath>`|  
|BuildInParallel|Multi-Proc [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] の使用時に複数のプロジェクト参照を同時にビルドまたはクリーンするかどうかを示すブール値です。 既定値は `true` です。システムに複数のコアまたはプロセッサがある場合に既定値を使用すると、複数のプロジェクトが同時にビルドされます。|  
|BuildProjectReferences|[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] によってプロジェクト参照をビルドするかどうかを示すブール値です。 プロジェクトを [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 統合開発環境 (IDE: Integrated Development Environment) でビルドする場合は `false`、それ以外の場合は `true` を指定します。|  
|CleanFile|"クリーン キャッシュ" として使用されるファイルの名前です。 クリーン キャッシュとは、クリーン操作の実行中に削除される対象の生成されたファイルのリストです。 このファイルは、ビルド プロセスによって中間出力パスに追加されます。<br /><br /> このプロパティでは、パス情報を含まないファイル名だけを指定します。|  
|CodePage|コンパイルですべてのソース コード ファイルに使用するコード ページを指定します。 このプロパティは、`/codepage` コンパイラ スイッチに相当します。|  
|CompilerResponseFile|コンパイラ タスクに渡すことができる応答ファイルです (省略可能)。|  
|構成|ビルドする構成です。"Debug" と "Release" のいずれかを指定します。|  
|CscToolPath|[!INCLUDE[csprcs](../includes/csprcs-md.md)] コンパイラ csc.exe のパスです。|  
|CustomBeforeMicrosoftCommonTargets|共通ターゲットのインポートの前に自動的にインポートされるプロジェクト ファイルまたは targets ファイルの名前です。|  
|DebugSymbols|ビルド時にシンボルを生成するかどうかを示すブール値です。<br /><br /> コマンド ラインで **/p:DebugSymbols=false** と設定すると、プログラム データベース (.pdb) シンボル ファイルの生成が無効になります。|  
|DefineConstants|条件付きコンパイル定数を定義します。 次の構文に従い、シンボルと値のペアをセミコロン (;) で区切って指定します。<br /><br /> *symbol1 = value1 ; symbol2 = value2*<br /><br /> このプロパティは、`/define` コンパイラ スイッチに相当します。|  
|DefineDebug|定数 DEBUG を定義するかどうかを示すブール値です。|  
|DefineTrace|定数 TRACE を定義するかどうかを示すブール値です。|  
|DebugType|生成するデバッグ情報のレベルを定義します。 有効な値は "full"、"pdbonly"、および "none" です。|  
|DelaySign|アセンブリに完全署名ではなく遅延署名するかどうかを示すブール値です。|  
|DisabledWarnings|指定された警告の出力を抑制します。 警告 ID の数値だけを指定してください。 複数の警告を指定するときは、セミコロン (;) で区切ります。 このパラメーターは、vbc.exe コンパイラの `/nowarn` スイッチに相当します。|  
|DisableFastUpToDateCheck|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のみに適用されるブール値です。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ビルド マネージャーは、FastUpToDateCheck と呼ばれるプロセスを使用して、プロジェクトをリビルドして最新の状態にする必要があるかどうかを判断します。 この判断を行う機能としては、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] より、このプロセスの方が高速です。 DisableFastUpToDateCheck プロパティを `true` に設定すると、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ビルド マネージャーをバイパスし、プロジェクトが最新の状態かどうかを判断するために [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] を使用するように強制できます。|  
|DocumentationFile|XML ドキュメント ファイルとして生成されるファイルの名前です。 この名前はファイル名のみを示し、パス情報は含んでいません。|  
|ErrorReport|コンパイラ タスクで内部コンパイル エラーを報告するかどうかを指定します。 有効な値は "prompt"、"send"、または "none" です。 このプロパティは、`/errorreport` コンパイラ スイッチに相当します。|  
|ExcludeDeploymentUrl|プロジェクト ファイルに次の要素が含まれている場合は、[GenerateDeploymentManifest Task](../msbuild/generatedeploymentmanifest-task.md) によって、deploymentProvider タグが配置マニフェストに追加されます。<br /><br /> -   UpdateUrl<br />-   InstallUrl<br />-   PublishUrl<br /><br /> ただし、ExcludeDeploymentUrl を使用すると、上記の URL が指定されている場合でも、配置マニフェストに deploymentProvider タグが追加されないようにすることができます。 これを行うには、次のプロパティをプロジェクト ファイルに追加します。<br /><br /> `<ExcludeDeploymentUrl>true</ExcludeDeploymentUrl>` **注意:** ExcludeDeploymentUrl は [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE では公開されていないため、プロジェクト ファイルを手動で編集する方法でのみ設定できます。 このプロパティを設定しても、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 内での発行には影響はありません。つまり、PublishUrl で指定された URL に deploymentProvider タグが追加されます。|  
|FileAlignment|出力ファイルでセクションをアラインするサイズをバイト単位で指定します。 有効値は 512、1024、2048、4096、および 8192 です。 このプロパティは、`/filealignment` コンパイラ スイッチに相当します。|  
|FrameworkPathOverride|mscorlib.dll および microsoft.visualbasic.dll の位置を指定します。 このパラメーターは、vbc.exe コンパイラの `/sdkpath` スイッチに相当します。|  
|GenerateDocumentation|ビルドによってドキュメントを生成するかどうかを示すブール値パラメーターです。 `true` に設定すると、ビルドによってドキュメント情報が生成され、ビルド タスクが作成した実行可能ファイルまたはライブラリの名前と共に .xml ファイルに格納されます。|  
|IntermediateOutputPath|中間出力ファイルの完全パスであり、パスが指定されていない場合に `BaseIntermediateOutputPath` を基に生成されます。 たとえば、\obj\debug\\ のようなパスが生成されます。 このプロパティがオーバーライドされた場合、`BaseIntermediateOutputPath` は無効になります。|  
|KeyContainerName|厳密名キーのコンテナー名です。|  
|KeyOriginatorFile|厳密名キー ファイルの名前です。|  
|NoWin32Manifest|コンパイル時に既定の Win32 マニフェストを生成して出力ファイルに含めるかどうかを決定します。 既定値の `false` では、すべてのアプリケーションに対して既定の Win32 マニフェストが生成されます。 このプロパティは、vbc.exe コンパイラの `/nowin32manifest` スイッチに相当します。|  
|ModuleAssemblyName|コンパイル済みモジュールを組み込むアセンブリの名前です。 このプロパティは、`/moduleassemblyname` コンパイラ スイッチに相当します。|  
|NoLogo|コンパイラ ロゴをオフにするかどうかを示すブール値です。 このプロパティは、`/nologo` コンパイラ スイッチに相当します。|  
|NoStdLib|標準ライブラリ (mscorlib.dll) の参照を回避するかどうかを示すブール値です。 既定値は `false` です。|  
|NoVBRuntimeReference|[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ランタイム (Microsoft.VisualBasic.dll) を参照としてプロジェクトに含めるかどうかを示すブール値です。|  
|NoWin32Manifest|ユーザー アカウント制御 (UAC) マニフェスト情報をアプリケーションの実行可能ファイルに埋め込むかどうかを示すブール値です。 [!INCLUDE[windowsver](../includes/windowsver-md.md)] を対象とする Visual Studio プロジェクトにのみ適用されます。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] および登録を必要としない COM を使用して配置されたプロジェクトでは、この要素無視されます。 `False` (既定値) は、ユーザー アカウント制御 (UAC: User Account Control) マニフェスト情報をアプリケーションの実行可能ファイルに埋め込むことを指定します。 `True`を指定すると、UAC マニフェスト情報は埋め込まれません。<br /><br /> このプロパティは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を対象とする [!INCLUDE[windowsver](../includes/windowsver-md.md)] プロジェクトにのみ適用されます。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] および登録を必要としない COM を使用して配置されたプロジェクトでは、このプロパティは無視されます。<br /><br /> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] でマニフェスト情報をアプリケーションの実行可能ファイルに埋め込まない場合に限り、NoWin32Manifest を追加してください。このプロセスは "*仮想化*" と呼ばれます。 仮想化を使用するには、次のように `<ApplicationManifest>` と共に `<NoWin32Manifest>` を設定します。<br /><br /> -   [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] プロジェクトの場合は、`<ApplicationManifest>` ノードを削除します  ([!INCLUDE[vbprvb](../includes/vbprvb-md.md)] プロジェクトでは、`<ApplicationManifest>` ノードが存在すると、`<NoWin32Manifest>` は無視されます)。<br />-   [!INCLUDE[csprcs](../includes/csprcs-md.md)] プロジェクトの場合は、`<ApplicationManifest>` を `False` に設定し、`<NoWin32Manifest>` を `True` に設定します  ([!INCLUDE[csprcs](../includes/csprcs-md.md)] プロジェクトでは、`<ApplicationManifest>` は `<NoWin32Manifest>` によりオーバーライドされます)。|  
|Optimize|`true` に設定された場合にコンパイラの最適化を有効にするブール値です。 このプロパティは、`/optimize` コンパイラ スイッチに相当します。|  
|OptionCompare|文字列比較の方法を指定します。 有効な値は "binary" または "text" です。 このプロパティは、vbc.exe コンパイラの `/optioncompare` スイッチに相当します。|  
|OptionExplicit|`true` に設定された場合にソース コードで変数が明示的に宣言されていることを要求するブール値です。 このプロパティは、`/optionexplicit` コンパイラ スイッチに相当します。|  
|OptionInfer|`true` に設定された場合に変数の型の推論を可能にするブール値です。 このプロパティは、`/optioninfer` コンパイラ スイッチに相当します。|  
|OptionStrict|`true` に設定された場合にビルド タスクで厳密な型のセマンティクスを適用して暗黙の型変換を制限するブール値です。 このプロパティは、vbc.exe コンパイラの `/optionstrict` スイッチに相当します。|  
|OutputPath|出力ディレクトリへのパスを、"bin\Debug" のようにプロジェクト ディレクトリを基準とする相対パスで指定します。|  
|OutputType|出力ファイルのファイル形式を指定します。 このパラメーターには、次のいずれかの値を指定できます。<br /><br /> -   Library。 コード ライブラリを作成します。 これは既定値です。<br />-   Exe。 コンソール アプリケーションを作成します。<br />-   Module。 モジュールを作成します。<br />-   Winexe。 Windows ベースのプログラムを作成します。<br /><br /> このプロパティは、vbc.exe コンパイラの `/target` スイッチに相当します。|  
|OverwriteReadOnlyFiles|ビルドにおいて読み取り専用ファイルを上書きするかエラーを発生させるかを示すブール値です。|  
|PdbFile|出力する .pdb ファイルの名前です。 このプロパティは、csc.exe コンパイラの `/pdb` スイッチに相当します。|  
|プラットフォーム|ビルドの対象とするオペレーティング システムです。 有効な値は "Any CPU"、"x86"、および "x64" です。|  
|RemoveIntegerChecks|整数オーバーフロー エラー チェックを無効にするかどうかを示すブール値です。 既定値は `false` です。 このプロパティは、vbc.exe コンパイラの `/removeintchecks` スイッチに相当します。|  
|SGenUseProxyTypes|SGen.exe によってプロキシ型を生成するかどうかを示すブール値です。<br /><br /> SGen ターゲットは、このプロパティを使用して UseProxyTypes フラグを設定します。 このプロパティの既定値は true で、これを変更するための UI はありません。 webservice 以外の型のシリアル化アセンブリを生成するには、Microsoft.Common.Targets または C#/VB.targets をインポートする前に、このプロパティをプロジェクト ファイルに追加し、その値を false に設定します。|  
|SGenToolPath|SGen.exe の現在のバージョンがオーバーライドされた場合に SGen.exe を取得する場所を示すツール パスです (省略可能)。|  
|StartupObject|Main メソッドまたは Sub Main プロシージャを含むクラスまたはモジュールを指定します。 このプロパティは、`/main` コンパイラ スイッチに相当します。|  
|ProcessorArchitecture|アセンブリ参照を解決するときに使用されるプロセッサ アーキテクチャです。 有効な値は "msil"、"x86"、"amd64"、または "ia64" です。|  
|RootNamespace|埋め込みリソースに名前を付けるときに使用するルート名前空間です。 この名前空間が埋め込みリソース マニフェスト名の一部になります。|  
|Satellite_AlgorithmId|サテライト アセンブリの作成時に使用する AL.exe ハッシュ アルゴリズムの ID です。|  
|Satellite_BaseAddress|`CreateSatelliteAssemblies` ターゲットを使用してカルチャ固有のサテライト アセンブリをビルドするときに使用するベース アドレスです。|  
|Satellite_CompanyName|サテライト アセンブリの生成時に AL.exe に渡す会社名です。|  
|Satellite_Configuration|サテライト アセンブリの生成時に AL.exe に渡す構成名です。|  
|Satellite_Description|サテライト アセンブリの生成時に AL.exe に渡す説明テキストです。|  
|Satellite_EvidenceFile|指定されたファイルをリソース名が "Security.Evidence" であるサテライト アセンブリに埋め込みます。|  
|Satellite_FileVersion|サテライト アセンブリの File Version フィールドに挿入する文字列を指定します。|  
|Satellite_Flags|サテライト アセンブリの Flags フィールドに挿入する値を指定します。|  
|Satellite_GenerateFullPaths|ビルド タスクがエラー メッセージで報告されるすべてのファイルについて絶対パスを使用します。|  
|Satellite_LinkResource|指定されたリソース ファイルをサテライト アセンブリにリンクします。|  
|Satellite_MainEntryPoint|サテライト アセンブリの生成においてモジュールを実行可能ファイルに変換するときにエントリ ポイントとして使用されるメソッドの完全修飾名 (class.method) を指定します。|  
|Satellite_ProductName|サテライト アセンブリの Product フィールドに挿入する文字列を指定します。|  
|Satellite_ProductVersion|サテライト アセンブリの ProductVersion フィールドに挿入する文字列を指定します。|  
|Satellite_TargetType|サテライト アセンブリの出力ファイルの形式として、"library"、"exe"、"win" のいずれかを指定します。 既定値は "library" です。|  
|Satellite_Title|サテライト アセンブリの Title フィールドに挿入する文字列を指定します。|  
|Satellite_Trademark|サテライト アセンブリの Trademark フィールドに挿入する文字列を指定します。|  
|Satellite_Version|サテライト アセンブリのバージョン情報を指定します。|  
|Satellite_Win32Icon|サテライト アセンブリに .ico アイコン ファイルを挿入します。|  
|Satellite_Win32Resource|サテライト アセンブリに Win32 リソース (.res ファイル) を挿入します。|  
|SubsystemVersion|生成された実行可能ファイルが使用できるサブシステムの最低限のバージョンを指定します。 このプロパティは、`/subsystemversion` コンパイラ スイッチに相当します。 このプロパティの既定値については、「[/subsystemversion (Visual Basic)](https://msdn.microsoft.com/library/08be22b2-f447-4cd3-8203-120b1b920b54)」または「[/subsystemversion (C# コンパイラ オプション)](https://msdn.microsoft.com/library/a99fce81-9d92-4813-9874-bee777041445)」を参照してください。|  
|TargetCompactFramework|ビルドするアプリケーションの実行に必要な .NET Compact Framework のバージョンです。 このプロパティを指定すると、通常は参照できない .NET Framework アセンブリを参照できます。|  
|TargetFrameworkVersion|ビルドするアプリケーションの実行に必要な [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] のバージョンです。 このプロパティを指定すると、通常は参照できない .NET Framework アセンブリを参照できます。|  
|TreatWarningsAsErrors|ブール値パラメーターであり、`true` に設定すると、すべての警告がエラーとして扱われます。 このパラメーターは、`/nowarn` コンパイラ スイッチに相当します。|  
|UseHostCompilerIfAvailable|ブール値パラメーターであり、`true` に設定すると、ビルド タスクはインプロセス コンパイラを使用します (インプロセス コンパイラが用意されている場合)。 このパラメーターは [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] でのみ使用されます。|  
|Utf8Output|ブール値パラメーターであり、`true` に設定すると、コンパイラ出力が UTF-8 エンコーディングでログに記録されます。 このパラメーターは、`/utf8Output` コンパイラ スイッチに相当します。|  
|VbcToolPath|vbc.exe の現在のバージョンがオーバーライドされた場合に vbc.exe の別の場所を示すパスです (省略可能)。|  
|VbcVerbosity|[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] コンパイラ出力の詳細度を指定します。 有効な値は "Quiet"、"Normal" (既定値)、または "Verbose" です。|  
|VisualStudioVersion|このプロジェクトが実行されている Visual Studio のバージョンを指定します。 このプロパティが指定されていない場合、MSBuild によって適切な既定値に設定されます。<br /><br /> このプロパティは複数の種類のプロジェクトで使用され、ビルドで利用されるターゲットのセットが指定されます。 `ToolsVersion` がプロジェクトに対して 4.0 以上に設定されている場合、`VisualStudioVersion` によって、使用するサブツールセットが指定されます。 詳細については、「[ツール セット (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)」を参照してください。|  
|WarningsAsErrors|エラーとして扱う警告の一覧を指定します。 このパラメーターは、`/warnaserror` コンパイラ スイッチに相当します。|  
|WarningsNotAsErrors|エラーとして扱わない警告の一覧を指定します。 このパラメーターは、`/warnaserror` コンパイラ スイッチに相当します。|  
|Win32Manifest|最終的なアセンブリに埋め込むマニフェスト ファイルの名前です。 このパラメーターは、`/win32Manifest` コンパイラ スイッチに相当します。|  
|Win32Resource|最終的なアセンブリに埋め込む Win32 リソースのファイル名です。 このパラメーターは、`/win32resource` コンパイラ スイッチに相当します。|  
  
## <a name="see-also"></a>関連項目
 [MSBuild プロジェクトの共通項目](../msbuild/common-msbuild-project-items.md)
