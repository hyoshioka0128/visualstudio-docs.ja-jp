---
title: MSBuild プロジェクトの共通プロパティ | Microsoft Docs
ms.date: 01/18/2018
ms.topic: reference
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
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b4fd82cee49c698c9244a2851d4e671ae6a94508
ms.sourcegitcommit: bf2e9d4ff38bf5b62b8af3da1e6a183beb899809
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2020
ms.locfileid: "77557885"
---
# <a name="common-msbuild-project-properties"></a>MSBuild プロジェクトの共通プロパティ
次の表は、Visual Studio プロジェクト ファイルで定義される、または MSBuild に用意されている *.targets* ファイルに含まれている、使用頻度の高いプロパティを示しています。

 Visual Studio のプロジェクト ファイル ( *.csproj*、 *.vbproj*、 *.vcxproj* など) には、IDE を使用してプロジェクトをビルドするときに実行される MSBuild XML コードが含まれています。 通常、プロジェクトでは、ビルド プロセスを定義するために、1 つ以上の *.targets* ファイルをインポートします。 詳しくは、「[MSBuild .Targets ファイル](../msbuild/msbuild-dot-targets-files.md)」をご覧ください。

## <a name="list-of-common-properties-and-parameters"></a>共通のプロパティおよびパラメーター一覧

| プロパティ名またはパラメーター名 | 説明 |
|------------------------------------| - |
| AdditionalLibPaths | コンパイラが参照アセンブリを検索する追加のフォルダーを指定します。 |
| AddModules | 指定ファイル内のすべての型情報をコンパイル対象のプロジェクトで使用できるようにします。 このプロパティは、`/addModules` コンパイラ スイッチに相当します。 |
| ALToolPath | *AL.exe* の保存先のパスです。 このプロパティによって、*AL.exe* の現在のバージョンをオーバーライドし、別のバージョンを使用できます。 |
| ApplicationIcon | Win32 アイコンとして埋め込むためにコンパイラに渡す *.ico* アイコン ファイルです。 このプロパティは、`/win32icon` コンパイラ スイッチに相当します。 |
| ApplicationManifest | 外部のユーザー アカウント制御 (UAC: User Account Control) マニフェスト情報を生成するのに使用するファイルのパスを指定します。 [!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)] を対象とする Visual Studio プロジェクトにのみ適用されます。<br /><br /> ほとんどの場合、マニフェストは埋め込まれます。 ただし、登録を必要としない COM 配置または [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置を使用する場合は、アプリケーション アセンブリと共にインストールされる外部ファイルをマニフェストとして使用できます。 詳細については、このトピックの NoWin32Manifest プロパティを参照してください。 |
| AssemblyOriginatorKeyFile | アセンブリ ( *.snk* または *.pfx*) に署名するために使用されるファイルを指定します。また、このファイルは [ResolveKeySource タスク](../msbuild/resolvekeysource-task.md)に渡され、アセンブリの署名に使用される実際のキーが生成されます。 |
| AssemblySearchPaths | ビルド時に参照アセンブリを解決するときに検索する場所のリストです。 このリストでは、先頭から順に優先度が低くなるため、パスを指定する順序が意味を持ちます。 |
| AssemblyName | プロジェクトのビルド後に生成される最終的な出力アセンブリの名前です。 |
| BaseAddress | メイン出力アセンブリのベース アドレスを指定します。‎ このプロパティは、`/baseaddress` コンパイラ スイッチに相当します。 |
| BaseIntermediateOutputPath | すべての構成固有の中間出力ファイルが作成されるトップレベル フォルダーです。 既定値は `obj\` です。 次にコード例を示します。`<BaseIntermediateOutputPath>c:\xyz\obj\</BaseIntermediateOutputPath>` |
| BaseOutputPath | 出力ファイルのベース パスを指定します。 設定されている場合、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] は `OutputPath = $(BaseOutputPath)\$(Configuration)\` を使用します。 構文例: `<BaseOutputPath>c:\xyz\bin\</BaseOutputPath>` |
| BuildInParallel | Multi-Proc [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] の使用時に複数のプロジェクト参照を同時にビルドまたはクリーンするかどうかを示すブール値です。 既定値は `true` です。システムに複数のコアまたはプロセッサがある場合に既定値を使用すると、複数のプロジェクトが同時にビルドされます。 |
| BuildProjectReferences | [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] によってプロジェクト参照をビルドするかどうかを示すブール値です。 プロジェクトを [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE: Integrated Development Environment) でビルドしている場合は `false` に自動的に設定され、それ以外の場合は `true` に設定されます。 `-p:BuildProjectReferences=false` をコマンド ラインで指定して、参照先のプロジェクトが最新かどうかのチェックを回避できます。 |
| CleanFile | "クリーン キャッシュ" として使用されるファイルの名前です。 クリーン キャッシュとは、クリーン操作の実行中に削除される対象の生成されたファイルのリストです。 このファイルは、ビルド プロセスによって中間出力パスに追加されます。<br /><br /> このプロパティでは、パス情報を含まないファイル名だけを指定します。 |
| CodePage | コンパイルですべてのソース コード ファイルに使用するコード ページを指定します。 このプロパティは、`/codepage` コンパイラ スイッチに相当します。 |
| CompilerResponseFile | コンパイラ タスクに渡すことができる応答ファイルです (省略可能)。 |
| 構成 | ビルドする構成です。"Debug" と "Release" のいずれかを指定します。 |
| CscToolPath | [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] コンパイラ *csc.exe* のパスです。 |
| CustomBeforeMicrosoftCommonTargets | 共通ターゲットのインポートの前に自動的にインポートされるプロジェクト ファイルまたは targets ファイルの名前です。 |
| DebugSymbols | ビルド時にシンボルを生成するかどうかを示すブール値です。<br /><br /> コマンド ラインで **-p:DebugSymbols=false** と設定すると、プログラム データベース ( *.pdb*) シンボル ファイルの生成が無効になります。 |
| DebugType | 生成するデバッグ情報のレベルを定義します。 有効な値は "full"、"pdbonly"、"portable"、"embedded、"および "none" です。 |
| DefineConstants | 条件付きコンパイル定数を定義します。 次の構文に従い、シンボルと値のペアをセミコロン (;) で区切って指定します。<br /><br /> *symbol1 = value1 ; symbol2 = value2*<br /><br /> このプロパティは、`/define` コンパイラ スイッチに相当します。 |
| DefineDebug | 定数 DEBUG を定義するかどうかを示すブール値です。 |
| DefineTrace | 定数 TRACE を定義するかどうかを示すブール値です。 |
| DelaySign | アセンブリに完全署名ではなく遅延署名するかどうかを示すブール値です。 |
| Deterministic | コンパイラが同じ入力に対して同じアセンブリを生成するかどうかを指示するブール値。 このパラメーターは、*vbc.exe* および *csc.exe* コンパイラの `/deterministic` スイッチに相当します。 |
| DisabledWarnings | 指定された警告の出力を抑制します。 警告 ID の数値だけを指定してください。 複数の警告を指定するときは、セミコロン (;) で区切ります。 このパラメーターは、*vbc.exe* コンパイラの `/nowarn` スイッチに相当します。 |
| DisableFastUpToDateCheck | [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のみに適用されるブール値です。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ビルド マネージャーは、FastUpToDateCheck と呼ばれるプロセスを使用して、プロジェクトをリビルドして最新の状態にする必要があるかどうかを判断します。 この判断を行う機能としては、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] より、このプロセスの方が高速です。 DisableFastUpToDateCheck プロパティを `true` に設定すると、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ビルド マネージャーをバイパスし、プロジェクトが最新の状態かどうかを判断するために [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] を使用するように強制できます。 |
| DocumentationFile | XML ドキュメント ファイルとして生成されるファイルの名前です。 この名前はファイル名のみを示し、パス情報は含んでいません。 |
| ErrorReport | コンパイラ タスクで内部コンパイル エラーを報告するかどうかを指定します。 有効な値は "prompt"、"send"、または "none" です。 このプロパティは、`/errorreport` コンパイラ スイッチに相当します。 |
| ExcludeDeploymentUrl | プロジェクト ファイルに次の要素が含まれている場合は、[GenerateDeploymentManifest タスク](../msbuild/generatedeploymentmanifest-task.md)によって、deploymentProvider タグが配置マニフェストに追加されます。<br /><br /> -   UpdateUrl<br />-   InstallUrl<br />-   PublishUrl<br /><br /> ただし、ExcludeDeploymentUrl を使用すると、上記の URL が指定されている場合でも、配置マニフェストに deploymentProvider タグが追加されないようにすることができます。 これを行うには、次のプロパティをプロジェクト ファイルに追加します。<br /><br /> `<ExcludeDeploymentUrl>true</ExcludeDeploymentUrl>` <br /><br />**注:** ExcludeDeploymentUrl は [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE では公開されていないため、プロジェクト ファイルを手動で編集する方法でのみ設定できます。 このプロパティを設定しても、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 内での発行には影響はありません。つまり、PublishUrl で指定された URL に deploymentProvider タグが追加されます。 |
| FileAlignment | 出力ファイルでセクションをアラインするサイズをバイト単位で指定します。 有効値は 512、1024、2048、4096、および 8192 です。 このプロパティは、`/filealignment` コンパイラ スイッチに相当します。 |
| FrameworkPathOverride | *mscorlib.dll* および *microsoft.visualbasic.dll* の位置を指定します。 このパラメーターは、*vbc.exe* コンパイラの `/sdkpath` スイッチに相当します。 |
| GenerateDocumentation | (C#、Visual Basic) ビルドによってドキュメントを生成するかどうかを示すブール値パラメーターです。 `true` に設定すると、ビルドによってドキュメント情報が生成され、ビルド タスクが作成した実行可能ファイルまたはライブラリの名前と共に *.xml* ファイルに格納されます。 |
| GenerateFullPaths | (C#) [-fullpaths](/dotnet/csharp/language-reference/compiler-options/fullpaths-compiler-option) コンパイラ オプションの使用により、出力内のファイル名の完全なパスが生成されます。 |
| GenerateSerializationAssemblies | XML シリアル化アセンブリを *SGen.exe* で生成するかどうかを示します。これはオン、自動、オフに設定できます。 このプロパティは、.NET Framework のみを対象とするアセンブリに使用されます。 .NET Standard アセンブリまたは .NET Core アセンブリに XML シリアル化アセンブリを生成するには、*Microsoft.XmlSerializer.Generator* パッケージを参照します。 |
| IntermediateOutputPath | 中間出力ファイルの完全パスであり、パスが指定されていない場合に `BaseIntermediateOutputPath` を基に生成されます。 たとえば、 *\obj\debug\\* のようなパスが生成されます。 |
| KeyContainerName | 厳密名キーのコンテナー名です。 |
| KeyOriginatorFile | 厳密名キー ファイルの名前です。 |
| ModuleAssemblyName | コンパイル済みモジュールを組み込むアセンブリの名前です。 このプロパティは、`/moduleassemblyname` コンパイラ スイッチに相当します。 |
| MSBuildProjectExtensionsPath | プロジェクト拡張機能が配置されるパスを指定します。 既定では、`BaseIntermediateOutputPath` と同じ値が使用されます。 |
| NoLogo | コンパイラ ロゴをオフにするかどうかを示すブール値です。 このプロパティは、`/nologo` コンパイラ スイッチに相当します。 |
| NoStdLib | 標準ライブラリ (*mscorlib.dll*) の参照を回避するかどうかを示すブール値です。 既定値は `false` です。 |
| NoVBRuntimeReference | [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] ランタイム (*Microsoft.VisualBasic.dll*) を参照としてプロジェクトに含めるかどうかを示すブール値です。 |
| NoWin32Manifest | ユーザー アカウント制御 (UAC) マニフェスト情報をアプリケーションの実行可能ファイルに埋め込むかどうかを示すブール値です。 [!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)] を対象とする Visual Studio プロジェクトにのみ適用されます。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] および登録を必要としない COM を使用して配置されたプロジェクトでは、この要素無視されます。 `False` (既定値) は、ユーザー アカウント制御 (UAC: User Account Control) マニフェスト情報をアプリケーションの実行可能ファイルに埋め込むことを指定します。 `True`を指定すると、UAC マニフェスト情報は埋め込まれません。<br /><br /> このプロパティは、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を対象とする [!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)] プロジェクトにのみ適用されます。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] および登録を必要としない COM を使用して配置されたプロジェクトでは、このプロパティは無視されます。<br /><br /> [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] でマニフェスト情報をアプリケーションの実行可能ファイルに埋め込まない場合に限り、NoWin32Manifest を追加してください。このプロセスは "*仮想化*" と呼ばれます。 仮想化を使用するには、次のように `<ApplicationManifest>` と共に `<NoWin32Manifest>` を設定します。<br /><br /> -   [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] プロジェクトの場合は、`<ApplicationManifest>` ノードを削除します ([!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] プロジェクトでは、`<ApplicationManifest>` ノードが存在すると、`<NoWin32Manifest>` は無視されます)。<br />-   [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] プロジェクトの場合は、`<ApplicationManifest>` を `False` に設定し、`<NoWin32Manifest>` を `True` に設定します ([!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] プロジェクトでは、`<ApplicationManifest>` は `<NoWin32Manifest>` によりオーバーライドされます)。<br /> このプロパティは、*vbc.exe* コンパイラの `/nowin32manifest` スイッチに相当します。 |
| Optimize | `true` に設定された場合にコンパイラの最適化を有効にするブール値です。 このプロパティは、`/optimize` コンパイラ スイッチに相当します。 |
| OptionCompare | 文字列比較の方法を指定します。 有効な値は "binary" または "text" です。 このプロパティは、*vbc.exe* コンパイラの `/optioncompare` スイッチに相当します。 |
| OptionExplicit | `true` に設定された場合にソース コードで変数が明示的に宣言されていることを要求するブール値です。 このプロパティは、`/optionexplicit` コンパイラ スイッチに相当します。 |
| OptionInfer | `true` に設定された場合に変数の型の推論を可能にするブール値です。 このプロパティは、`/optioninfer` コンパイラ スイッチに相当します。 |
| OptionStrict | `true` に設定された場合にビルド タスクで厳密な型のセマンティクスを適用して暗黙の型変換を制限するブール値です。 このプロパティは、*vbc.exe* コンパイラの `/optionstrict` スイッチに相当します。 |
| OutDir | プロジェクトまたはソリューションの最終的な出力場所を示します。 ソリューションをビルドする場合、OutDir を使用すれば、複数のプロジェクト出力を 1 つの場所で収集できます。 さらに、OutDir は、参照を解決する場合に使用される AssemblySearchPaths に取り込まれます。 たとえば、*bin\Debug* です。 |
| OutputPath | 出力ディレクトリへのパスを、*bin\Debug* のようにプロジェクト ディレクトリを基準とする相対パスで指定します。 |
| OutputType | 出力ファイルのファイル形式を指定します。 このパラメーターには、次のいずれかの値を指定できます。<br /><br /> -   Library。 コード ライブラリを作成します。 これは既定値です。<br />-   Exe。 コンソール アプリケーションを作成します。<br />-   Module。 モジュールを作成します。<br />-   Winexe。 Windows ベースのプログラムを作成します。<br /><br /> このプロパティは、*vbc.exe* コンパイラの `/target` スイッチに相当します。 |
| OverwriteReadOnlyFiles | ビルドにおいて読み取り専用ファイルを上書きするかエラーを発生させるかを示すブール値です。 |
| PathMap | コンパイラによるソース パス名出力への物理パスのマップ方法を指定します。 このプロパティは、*csc.exe* コンパイラの `/pathmap` スイッチに相当します。 |
| PdbFile | 出力する *.pdb* ファイルの名前です。 このプロパティは、*csc.exe* コンパイラの `/pdb` スイッチに相当します。 |
| プラットフォーム | ビルドの対象とするオペレーティング システムです。 有効な値は "Any CPU"、"x86"、および "x64" です。 |
| ProcessorArchitecture | アセンブリ参照を解決するときに使用されるプロセッサ アーキテクチャです。 有効な値は "msil"、"x86"、"amd64"、または "ia64" です。 |
| ProduceOnlyReferenceAssembly | コンパイル済みコードではなく参照アセンブリのみを発行するようにコンパイラに指示するブール値。 `ProduceReferenceAssembly` と同時に使用することはできません。  このプロパティは、*vbc.exe* コンパイラと *csc.exe* コンパイラの `/refonly` スイッチに対応します。 |
| ProduceReferenceAssembly | `true` に設定すると、現在のアセンブリに対して[参照アセンブリ](/dotnet/standard/assembly/reference-assemblies)の生成が可能になるブール値。 この機能の利用時、`Deterministic` を `true` にする必要があります。 このプロパティは、*vbc.exe* コンパイラと *csc.exe* コンパイラの `/refout` スイッチに対応します。 |
| RemoveIntegerChecks | 整数オーバーフロー エラー チェックを無効にするかどうかを示すブール値です。 既定値は `false` です。 このプロパティは、*vbc.exe* コンパイラの `/removeintchecks` スイッチに相当します。 |
| RootNamespace | 埋め込みリソースに名前を付けるときに使用するルート名前空間です。 この名前空間が埋め込みリソース マニフェスト名の一部になります。 |
| Satellite_AlgorithmId | サテライト アセンブリの作成時に使用する *AL.exe* ハッシュ アルゴリズムの ID です。 |
| Satellite_BaseAddress | `CreateSatelliteAssemblies` ターゲットを使用してカルチャ固有のサテライト アセンブリをビルドするときに使用するベース アドレスです。 |
| Satellite_CompanyName | サテライト アセンブリの生成時に *AL.exe* に渡す会社名です。 |
| Satellite_Configuration | サテライト アセンブリの生成時に *AL.exe* に渡す構成名です。 |
| Satellite_Description | サテライト アセンブリの生成時に *AL.exe* に渡す説明テキストです。 |
| Satellite_EvidenceFile | 指定されたファイルをリソース名が "Security.Evidence" であるサテライト アセンブリに埋め込みます。 |
| Satellite_FileVersion | サテライト アセンブリの File Version フィールドに挿入する文字列を指定します。 |
| Satellite_Flags | サテライト アセンブリの Flags フィールドに挿入する値を指定します。 |
| Satellite_GenerateFullPaths | ビルド タスクがエラー メッセージで報告されるすべてのファイルについて絶対パスを使用します。 |
| Satellite_LinkResource | 指定されたリソース ファイルをサテライト アセンブリにリンクします。 |
| Satellite_MainEntryPoint | サテライト アセンブリの生成においてモジュールを実行可能ファイルに変換するときにエントリ ポイントとして使用されるメソッドの完全修飾名 (class.method) を指定します。 |
| Satellite_ProductName | サテライト アセンブリの Product フィールドに挿入する文字列を指定します。 |
| Satellite_ProductVersion | サテライト アセンブリの ProductVersion フィールドに挿入する文字列を指定します。 |
| Satellite_TargetType | サテライト アセンブリの出力ファイルの形式として、"library"、"exe"、"win" のいずれかを指定します。 既定値は "library" です。 |
| Satellite_Title | サテライト アセンブリの Title フィールドに挿入する文字列を指定します。 |
| Satellite_Trademark | サテライト アセンブリの Trademark フィールドに挿入する文字列を指定します。 |
| Satellite_Version | サテライト アセンブリのバージョン情報を指定します。 |
| Satellite_Win32Icon | サテライト アセンブリに *.ico* アイコン ファイルを挿入します。 |
| Satellite_Win32Resource | サテライト アセンブリに Win32 リソース ( *.res* ファイル) を挿入します。 |
| SGenToolPath | *SGen.exe* の現在のバージョンがオーバーライドされた場合に *SGen.exe* を取得する場所を示すツール パスです (省略可能)。 このプロパティは .NET Framework にのみ使用されます。|
| SGenUseProxyTypes | *SGen.exe* によってプロキシ型を生成するかどうかを示すブール値です。 これは、*GenerateSerializationAssemblies* がオンに設定されているときにのみに適用されます。また、.NET Framework 専用です。<br /><br /> SGen ターゲットは、このプロパティを使用して UseProxyTypes フラグを設定します。 このプロパティの既定値は true で、これを変更するための UI はありません。 webservice 以外の型のシリアル化アセンブリを生成するには、*Microsoft.Common.Targets* または *C#/VB.targets* をインポートする前に、このプロパティをプロジェクト ファイルに追加し、その値を false に設定します。 |
| StartupObject | Main メソッドまたは Sub Main プロシージャを含むクラスまたはモジュールを指定します。 このプロパティは、`/main` コンパイラ スイッチに相当します。 |
| SubsystemVersion | 生成された実行可能ファイルが使用できるサブシステムの最低限のバージョンを指定します。 このプロパティは、`/subsystemversion` コンパイラ スイッチに相当します。 このプロパティの既定値については、「[/subsystemversion (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/subsystemversion)」または「[/subsystemversion (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/subsystemversion-compiler-option)」を参照してください。 |
| TargetCompactFramework | ビルドするアプリケーションの実行に必要な .NET Compact Framework のバージョンです。 このプロパティを指定すると、通常は参照できない .NET Framework アセンブリを参照できます。 |
| TargetFrameworkVersion | ビルドするアプリケーションの実行に必要な .NET Framework のバージョンです。 このプロパティを指定すると、通常は参照できない .NET Framework アセンブリを参照できます。 |
| TreatWarningsAsErrors | ブール値パラメーターであり、`true` に設定すると、すべての警告がエラーとして扱われます。 このパラメーターは、`/nowarn` コンパイラ スイッチに相当します。 |
| UseHostCompilerIfAvailable | ブール値パラメーターであり、`true` に設定すると、ビルド タスクはインプロセス コンパイラを使用します (インプロセス コンパイラが用意されている場合)。 このパラメーターは [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] でのみ使用されます。 |
| Utf8Output | ブール値パラメーターであり、`true` に設定すると、コンパイラ出力が UTF-8 エンコーディングでログに記録されます。 このパラメーターは、`/utf8Output` コンパイラ スイッチに相当します。 |
| VbcToolPath | *vbc.exe* の現在のバージョンがオーバーライドされた場合に *vbc.exe* の別の場所を示すパスです (省略可能)。 |
| VbcVerbosity | [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] コンパイラ出力の詳細度を指定します。 有効な値は "Quiet"、"Normal" (既定値)、または "Verbose" です。 |
| VisualStudioVersion | このプロジェクトが実行されている Visual Studio のバージョンを指定します。 このプロパティが指定されていない場合、MSBuild によって適切な既定値に設定されます。<br /><br /> このプロパティは複数の種類のプロジェクトで使用され、ビルドで利用されるターゲットのセットが指定されます。 `ToolsVersion` がプロジェクトに対して 4.0 以上に設定されている場合、`VisualStudioVersion` によって、使用するサブツールセットが指定されます。 詳細については、「[ツール セット (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)」を参照してください。 |
| WarningsAsErrors | エラーとして扱う警告の一覧を指定します。 このパラメーターは、`/warnaserror` コンパイラ スイッチに相当します。 |
| WarningsNotAsErrors | エラーとして扱わない警告の一覧を指定します。 このパラメーターは、`/warnaserror` コンパイラ スイッチに相当します。 |
| Win32Manifest | 最終的なアセンブリに埋め込むマニフェスト ファイルの名前です。 このパラメーターは、`/win32Manifest` コンパイラ スイッチに相当します。 |
| Win32Resource | 最終的なアセンブリに埋め込む Win32 リソースのファイル名です。 このパラメーターは、`/win32resource` コンパイラ スイッチに相当します。 |

## <a name="see-also"></a>関連項目
- [MSBuild プロジェクトの共通項目](../msbuild/common-msbuild-project-items.md)
