---
title: Link タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VC.Project.VCLinkerTool.ForceFileOutput
- VC.Project.VCLinkerTool.LinkStatus
- VC.Project.VCLinkerTool.CLRUnmanagedCodeCheck
- VC.Project.VCLinkerTool.SpecifySectionAttributes
- VC.Project.VCLinkerTool.SupportNobindOfDelayLoadedDLL
- VC.Project.VCLinkerTool.MinimumRequiredVersion
- VC.Project.VCLinkerTool.PerUserRedirection
- VC.Project.VCLinkerTool.CreateHotPatchableImage
- VC.Project.VCLinkerTool.DataExecutionPrevention
- VC.Project.VCLinkerTool.TreatLinkerWarningsAsErrors
- vc.task.link
- VC.Project.VCLinkerTool.ImageHasSafeExceptionHandlers
- VC.Project.VCLinkerTool.CLRSupportLastError
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild (C++), Link task
- Link task (MSBuild (C++))
ms.assetid: 0a61f168-3113-4fa7-83a3-d9142e2a33f8
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0f954be3a77e42ea4323255f978f6602a70c9725
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/26/2020
ms.locfileid: "77633578"
---
# <a name="link-task"></a>Link タスク

Microsoft C++ リンカー ツール *link.exe* をラップします。 リンカー ツールは、COFF (Common Object File Format) オブジェクト ファイルとライブラリをリンクし、実行可能ファイル ( *.exe*) やダイナミック リンク ライブラリ (DLL) を生成します。 詳細については、「[リンカー オプション](/cpp/build/reference/linker-options)」を参照してください。

## <a name="parameters"></a>パラメーター

 次には、**Link** タスクのパラメーターを説明します。 タスク パラメーターの大部分とパラメーターのいくつかのセットは、コマンド ライン オプションに対応します。

- **AdditionalDependencies**

  省略可能な **String[]** 型のパラメーターです。

  コマンドに追加する入力ファイルのリストを指定します。

  詳細については、「[LINK 入力ファイル](/cpp/build/reference/link-input-files)」を参照してください。

- **AdditionalLibraryDirectories**

  省略可能な **String[]** 型のパラメーターです。

  環境ライブラリ パスをオーバーライドします。 ディレクトリ名を指定します。

  詳細については、「[/LIBPATH (追加ライブラリのパス)](/cpp/build/reference/libpath-additional-libpath)」を参照してください。

- **AdditionalManifestDependencies**

  省略可能な **String[]** 型のパラメーターです。

  マニフェスト ファイルの `dependency` セクションに置かれる属性を指定します。

  詳細については、「[/MANIFESTDEPENDENCY (マニフェストの依存関係を指定する)](/cpp/build/reference/manifestdependency-specify-manifest-dependencies)」を参照してください。 「[Publisher configuration files](/windows/desktop/SbsCs/publisher-configuration-files)」(パブリッシャー構成ファイル) も参照してください。

- **AdditionalOptions**

  省略可能な **String** 型のパラメーターです。

  コマンド ラインで指定するリンカー オプションのリストです。 例: /\<option1> /\<option2> /\<option#> 他の **Link** タスク パラメーターでは表されないリンカー オプションを指定する場合は、このパラメーターを使用します。

  詳細については、「[リンカー オプション](/cpp/build/reference/linker-options)」を参照してください。

- **AddModuleNamesToAssembly**

  省略可能な **String[]** 型のパラメーターです。

  アセンブリのモジュール参照を追加します。

  詳細については、「[/ASSEMBLYMODULE (MSIL モジュールのアセンブリへの追加)](/cpp/build/reference/assemblymodule-add-a-msil-module-to-the-assembly)」を参照してください。

- **AllowIsolation**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合、オペレーティング システムはマニフェストの検索と読み込みを行います。 `false` の場合は、あたかもマニフェストがないかのように DLL を読み込むことを示します。

  詳細については、「[/ALLOWISOLATION (マニフェスト検索)](/cpp/build/reference/allowisolation-manifest-lookup)」を参照してください。

- **AssemblyDebug**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、**DebuggableAttribute** 属性をデバッグ情報追跡と一緒に出力し、JIT 最適化を無効にします。 `false` の場合は、**DebuggableAttribute** 属性を出力しますが、デバッグ情報追跡を無効にし、JIT 最適化を有効にします。

  詳細については、「[/ASSEMBLYDEBUG (DebuggableAttribute の追加)](/cpp/build/reference/assemblydebug-add-debuggableattribute)」を参照してください。

- **AssemblyLinkResource**

  省略可能な **String[]** 型のパラメーターです。

  出力ファイル内で .NET Framework リソースへのリンクを作成します。リソース ファイルは出力ファイル内に置かれません。 リソースの名前を指定します。

  詳細については、「[/ASSEMBLYLINKRESOURCE (.NET Framework リソースへのリンク)](/cpp/build/reference/assemblylinkresource-link-to-dotnet-framework-resource)」を参照してください。

- **AttributeFileTracking**

  暗黙的な**ブール値**のパラメーターです。

  詳細なファイル追跡でリンク インクリメンタルの動作をキャプチャできるようにします。 常に `true` を返します。

- **BaseAddress**

  省略可能な **String** 型のパラメーターです。

  ビルド対象のプログラムまたは DLL のベース アドレスを設定します。 `{address[,size] | @filename,key}`を指定します。

  詳細については、「[/BASE (ベース アドレス)](/cpp/build/reference/base-base-address)」を参照してください。

- **BuildingInIDE**

  省略可能な **Boolean** 型のパラメーターです。

  true の場合は、IDE から MSBuild が呼び出されることを示します。 それ以外の場合は、コマンド ラインから MSBuild が呼び出されることを示します。

  このパラメーターに相当するリンカー オプションはありません。

- **CLRImageType**

  省略可能な **String** 型のパラメーターです。

  共通言語ランタイム (CLR) イメージのタイプを設定します。

  次のいずれかの値を指定します。各値はリンカー オプションに対応しています。

  - **Default** -  *\<none>*

  - **ForceIJWImage** -  **/CLRIMAGETYPE:IJW**

  - **ForcePureILImage** -  **/CLRIMAGETYPE:PURE**

  - **ForceSafeILImage** -  **/CLRIMAGETYPE:SAFE**

  詳細については、「[/CLRIMAGETYPE (CLR イメージのタイプの指定)](/cpp/build/reference/clrimagetype-specify-type-of-clr-image)」を参照してください。

- **CLRSupportLastError**

  省略可能な **String** 型のパラメーターです。

  P/Invoke 機構を通じて呼び出された関数の最終エラー コードを保持します。

  次のいずれかの値を指定します。各値はリンカー オプションに対応しています。

  - **Enabled** -  **/CLRSupportLastError**

  - **Disabled** -  **/CLRSupportLastError:NO**

  - **SystemDlls** -  **/CLRSupportLastError:SYSTEMDLL**

  詳細については、「[/CLRSUPPORTLASTERROR (PInvoke 呼び出しの最終エラー コードの保持)](/cpp/build/reference/clrsupportlasterror-preserve-last-error-code-for-pinvoke-calls)」を参照してください。

- **CLRThreadAttribute**

  省略可能な **String** 型のパラメーターです。

  CLR プログラムのエントリ ポイントにスレッド属性を明示的に指定します。

  次のいずれかの値を指定します。各値はリンカー オプションに対応しています。

  - **DefaultThreadingAttribute** -  **/CLRTHREADATTRIBUTE:NONE**

  - **MTAThreadingAttribute** -  **/CLRTHREADATTRIBUTE:MTA**

  - **STAThreadingAttribute** -  **/CLRTHREADATTRIBUTE:STA**

  詳細については、「[/CLRTHREADATTRIBUTE (CLR スレッド属性の設定)](/cpp/build/reference/clrthreadattribute-set-clr-thread-attribute)」を参照してください。

- **CLRUnmanagedCodeCheck**

  省略可能な **Boolean** 型のパラメーターです。

  マネージド コードからネイティブ DLL への、リンカーによって生成された P/Invoke 呼び出しに対して、**SuppressUnmanagedCodeSecurityAttribute** を適用するかどうかを指定します。

  詳細については、「[/CLRUNMANAGEDCODECHECK (SuppressUnmanagedCodeSecurityAttribute の追加)](/cpp/build/reference/clrunmanagedcodecheck-add-suppressunmanagedcodesecurityattribute)」を参照してください。

- **CreateHotPatchableImage**

  省略可能な **String** 型のパラメーターです。

  イメージをホットパッチできるようにします。

  次のいずれかの値を指定します。値はリンカー オプションに対応しています。

  - **Enabled** -  **/FUNCTIONPADMIN**

  - **X86Image** -  **/FUNCTIONPADMIN:5**

  - **X64Image** -  **/FUNCTIONPADMIN:6**

  - **ItaniumImage** -  **/FUNCTIONPADMIN:16**

  詳細については、「[/FUNCTIONPADMIN (ホットパッチ可能なイメージの作成)](/cpp/build/reference/functionpadmin-create-hotpatchable-image)」を参照してください。

- **DataExecutionPrevention**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、実行可能ファイルで Windows データ実行防止機能との互換性がテストされたことを示します。

  詳細については、「[/NXCOMPAT (データ実行防止との互換性)](/cpp/build/reference/nxcompat-compatible-with-data-execution-prevention)」を参照してください。

- **DelayLoadDLLs**

  省略可能な **String[]** 型のパラメーターです。

  このパラメーターにより、DLL の*遅延読み込み*が行われます。 遅延読み込みする DLL の名前を指定します。

  詳細については、「[/DELAYLOAD (遅延読み込みのインポート)](/cpp/build/reference/delayload-delay-load-import)」を参照してください。

- **DelaySign**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、アセンブリに部分署名します。 既定では、値は `false` です。

  詳細については、「[/DELAYSIGN (アセンブリの部分署名)](/cpp/build/reference/delaysign-partially-sign-an-assembly)」を参照してください。

- **Driver**

  省略可能な **String** 型のパラメーターです。

  Windows NT カーネル モード ドライバーをビルドするには、このパラメーターを指定します。

  次のいずれかの値を指定します。各値はリンカー オプションに対応しています。

  - **NotSet** -  *\<none>*

  - **Driver** -  **/Driver**

  - **UpOnly** -  **/DRIVER:UPONLY**

  - **WDM** -  **/DRIVER:WDM**

  詳細については、「[/DRIVER (Windows NT カーネル モード ドライバー)](/cpp/build/reference/driver-windows-nt-kernel-mode-driver)」を参照してください。

- **EmbedManagedResourceFile**

  省略可能な **String[]** 型のパラメーターです。

  リソース ファイルをアセンブリに埋め込みます。 必要なリソース ファイル名を指定します。 必要に応じて、論理名 (リソースの読み込みに使用される) および **PRIVATE** オプション (リソース ファイルがプライベートであることをアセンブリ マニフェストで示す) を指定します。

  詳細については、「[/ASSEMBLYRESOURCE (マネージド リソースの埋め込み)](/cpp/build/reference/assemblyresource-embed-a-managed-resource)」を参照してください。

- **EnableCOMDATFolding**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、同一の COMDAT が折りたたまれ (圧縮され) ます。

  詳細については、「[/OPT (最適化)](/cpp/build/reference/opt-optimizations)」の `ICF[= iterations]` 引数を参照してください。

- **EnableUAC**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、ユーザー アカウント制御 (UAC) 情報をプログラム マニフェストに組み込むことを指定します。

  詳細については、「[/MANIFESTUAC (UAC 情報をマニフェストに組み込む)](/cpp/build/reference/manifestuac-embeds-uac-information-in-manifest)」を参照してください。

- **EntryPointSymbol**

  省略可能な **String** 型のパラメーターです。

  *.exe* ファイルまたは DLL の開始アドレスとしてエントリ ポイント関数を指定します。 パラメーター値として関数名を指定します。

  詳細については、「[/ENTRY (エントリ ポイント シンボル)](/cpp/build/reference/entry-entry-point-symbol)」を参照してください。

- **FixedBaseAddress**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、指定のベース アドレスだけに読み込まれるプログラムまたは DLL を作成します。

  詳細については、「[/FIXED (固定ベース アドレス)](/cpp/build/reference/fixed-fixed-base-address)」を参照してください。

- **ForceFileOutput**

  省略可能な **String** 型のパラメーターです。

  未定義のシンボルが参照された場合や、シンボルが複数回定義された場合でも、有効な *.exe* ファイルまたは DLL を作成するようリンカーを設定します。

  次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **Enabled** -  **/FORCE**

  - **MultiplyDefinedSymbolOnly** -  **/FORCE:MULTIPLE**

  - **UndefinedSymbolOnly** -  **/FORCE:UNRESOLVED**

  詳細については、「[/FORCE (ファイルを強制的に出力)](/cpp/build/reference/force-force-file-output)」を参照してください。

- **ForceSymbolReferences**

  省略可能な **String[]** 型のパラメーターです。

  このパラメーターは、指定されたシンボルをシンボル テーブルに追加するようリンカーを設定します。

  詳細については、「[/INCLUDE (シンボル参照の強制)](/cpp/build/reference/include-force-symbol-references)」を参照してください。

- **FunctionOrder**

  省略可能な **String** 型のパラメーターです。

  このパラメーターは、指定されたパッケージ化関数 (COMDAT) をあらかじめ決められた順序でイメージに入れることによって、プログラムを最適化します。

  詳細については、「[/ORDER (関数の順序)](/cpp/build/reference/order-put-functions-in-order)」を参照してください。

- **GenerateDebugInformation**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、 *.exe* ファイルまたは DLL のデバッグ情報を生成します。

  詳細については、「[/DEBUG (デバッグ情報の生成)](/cpp/build/reference/debug-generate-debug-info)」を参照してください。

- **GenerateManifest**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、side-by-side マニフェスト ファイルを作成します。

  詳細については、「[/MANIFEST (side-by-side アセンブリ マニフェストを作成する)](/cpp/build/reference/manifest-create-side-by-side-assembly-manifest)」を参照してください。

- **GenerateMapFile**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、*マップ ファイル*を作成します。 マップ ファイルのファイル名拡張子は、 *.map* です。

  詳細については、「[/MAP (マップ ファイルの生成)](/cpp/build/reference/map-generate-mapfile)」を参照してください。

- **HeapCommitSize**

  省略可能な **String** 型のパラメーターです。

  一度に割り当てるヒープの物理メモリ量を指定します。

  詳細については、「[/HEAP (ヒープ サイズの設定)](/cpp/build/reference/heap-set-heap-size)」の `commit` 引数を参照してください。 **HeapReserveSize** パラメーターも参照してください。

- **HeapReserveSize**

  省略可能な **String** 型のパラメーターです。

  仮想メモリ内のヒープ割り当ての合計を指定します。

  詳細については、「[/HEAP (ヒープ サイズの設定)](/cpp/build/reference/heap-set-heap-size)」の `reserve` 引数を参照してください。 この表にある **HeapCommitSize** パラメーターも参照してください。

- **IgnoreAllDefaultLibraries**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、外部参照の解決時に検索するライブラリ リストから 1 つ以上の既定のライブラリを削除するようリンカーを設定します。

  詳細については、「[/NODEFAULTLIB (ライブラリを無視する)](/cpp/build/reference/nodefaultlib-ignore-libraries)」を参照してください。

- **IgnoreEmbeddedIDL**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、ソース コード内の IDL 属性を *.idl* ファイルに処理しないことを指定します。

  詳細については、「[/IGNOREIDL (属性を MIDL に挿入しない)](/cpp/build/reference/ignoreidl-don-t-process-attributes-into-midl)」を参照してください。

- **IgnoreImportLibrary**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合、この構成で生成されるインポート ライブラリは、依存プロジェクトにインポートされません。

  このパラメーターは、リンカー オプションに対応していません。

- **IgnoreSpecificDefaultLibraries**

  省略可能な **String[]** 型のパラメーターです。

  無視する既定のライブラリの名前を 1 つ以上指定します。 複数のライブラリはセミコロンで区切ります。

  詳細については、「[/NODEFAULTLIB (ライブラリを無視する)](/cpp/build/reference/nodefaultlib-ignore-libraries)」を参照してください。

- **ImageHasSafeExceptionHandlers**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合、リンカーは、イメージの安全な例外ハンドラーのテーブルも生成できる場合のみ、イメージを生成します。

  詳細については、「[/SAFESEH (安全な例外ハンドラーがあるイメージ)](/cpp/build/reference/safeseh-image-has-safe-exception-handlers)」を参照してください。

- **ImportLibrary**

  既定のライブラリ名と置き換わるユーザー指定のインポート ライブラリの名前です。

  詳細については、「[/IMPLIB (インポート ライブラリ名の設定)](/cpp/build/reference/implib-name-import-library)」を参照してください。

- **KeyContainer**

  省略可能な **String** 型のパラメーターです。

  署名付きアセンブリのキーを含むコンテナーです。

  詳細については、「[/KEYCONTAINER (アセンブリに署名するためのキー コンテナーの指定)](/cpp/build/reference/keycontainer-specify-a-key-container-to-sign-an-assembly)」を参照してください。 この表にある **KeyFile** パラメーターも参照してください。

- **KeyFile**

  省略可能な **String** 型のパラメーターです。

  署名付きアセンブリのキーを含むファイルを指定します。

  詳細については、「[/KEYFILE (アセンブリに署名するためのキーまたはキー ペアの指定)](/cpp/build/reference/keyfile-specify-key-or-key-pair-to-sign-an-assembly)」を参照してください。 **KeyContainer** パラメーターも参照してください。

- **LargeAddressAware**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合、アプリケーションは 2 ギガバイトを超えるアドレスを処理できます。

  詳細については、「[/LARGEADDRESSAWARE (大きいアドレスの処理)](/cpp/build/reference/largeaddressaware-handle-large-addresses)」を参照してください。

- **LinkDLL**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、メイン出力ファイルとして DLL をビルドします。

  詳細については、「[/DLL (DLL のビルド)](/cpp/build/reference/dll-build-a-dll)」を参照してください。

- **LinkErrorReporting**

  省略可能な **String** 型のパラメーターです。

  内部コンパイル エラー (ICE) 情報を Microsoft に直接報告できます。

  次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **NoErrorReport** -  **/ERRORREPORT:NONE**

  - **PromptImmediately** -  **/ERRORREPORT:PROMPT**

  - **QueueForNextLogin** -  **/ERRORREPORT:QUEUE**

  - **SendErrorReport** -  **/ERRORREPORT:SEND**

  詳細については、「[/ERRORREPORT (内部リンカー エラーの報告)](/cpp/build/reference/errorreport-report-internal-linker-errors)」を参照してください。

- **LinkIncremental**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、インクリメンタル リンクを有効にします。

  詳細については、「[/INCREMENTAL (インクリメンタル リンクを行う)](/cpp/build/reference/incremental-link-incrementally)」を参照してください。

- **LinkLibraryDependencies**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、プロジェクト依存関係からのライブラリ出力を自動的にリンクすることを指定します。

  このパラメーターは、リンカー オプションに対応していません。

- **LinkStatus**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、リンクの何パーセントが完了したかを示す進行状況のインジケーターをリンカーが表示することを指定します。

  詳細については、「[/LTCG (リンク時のコード生成)](/cpp/build/reference/ltcg-link-time-code-generation)」の `STATUS` 引数を参照してください。

- **LinkTimeCodeGeneration**

  省略可能な **String** 型のパラメーターです。

  ガイド付き最適化のプロファイルのオプションを指定します。

  次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **Default** -  *\<none>*

  - **UseLinkTimeCodeGeneration** -  **/LTCG**

  - **PGInstrument** -  **/LTCG:PGInstrument**

  - **PGOptimization** -  **/LTCG:PGOptimize**

  - **PGUpdate**

    \- **/LTCG:PGUpdate**

  詳細については、「[/LTCG (リンク時のコード生成)](/cpp/build/reference/ltcg-link-time-code-generation)」を参照してください。

- **ManifestFile**

  省略可能な **String** 型のパラメーターです。

  既定のマニフェスト ファイル名を、指定されたファイル名に変更します。

  詳細については、「[/MANIFESTFILE (マニフェスト ファイルに名前を付ける)](/cpp/build/reference/manifestfile-name-manifest-file)」を参照してください。

- **MapExports**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、エクスポートされた関数をマップ ファイルに含めるようリンカーを設定します。

  詳細については、「[/MAPINFO (マップ ファイルに含める情報)](/cpp/build/reference/mapinfo-include-information-in-mapfile)」の `EXPORTS` 引数を参照してください。

- **MapFileName**

  省略可能な **String** 型のパラメーターです。

  既定のマップ ファイル名を、指定されたファイル名に変更します。

- **MergedIDLBaseFileName**

  省略可能な **String** 型のパラメーターです。

  *.idl* ファイルのファイル名とファイル名拡張子を指定します。

  詳細については、「[/IDLOUT (MIDL 出力ファイルの指定)](/cpp/build/reference/idlout-name-midl-output-files)」を参照してください。

- **MergeSections**

  省略可能な **String** 型のパラメーターです。

  イメージ内のセクションを結合します。 `from-section=to-section`を指定します。

  詳細については、「[/MERGE (セクションの結合)](/cpp/build/reference/merge-combine-sections)」を参照してください。

- **MidlCommandFile**

  省略可能な **String** 型のパラメーターです。

  MIDL コマンド ライン オプションを含むファイルの名前を指定します。

  詳細については、「[/MIDL (MIDL コマンド ライン オプションの指定)](/cpp/build/reference/midl-specify-midl-command-line-options)」を参照してください。

- **MinimumRequiredVersion**

  省略可能な **String** 型のパラメーターです。

  サブシステムの最低限必要なバージョンを指定します。 引数には、0 から 65535 までの範囲の 10 進数を指定します。

- **ModuleDefinitionFile**

  省略可能な **String** 型のパラメーターです。

  [モジュール定義ファイル](/cpp/build/reference/module-definition-dot-def-files)の名前を指定します。

  詳細については、「[/DEF (モジュール定義ファイルの指定)](/cpp/build/reference/def-specify-module-definition-file)」を参照してください。

- **MSDOSStubFileName**

  省略可能な **String** 型のパラメーターです。

  指定された MS-DOS スタブ プログラムを Win32 プログラムにアタッチします。

  詳細については、「[/STUB (MS-DOS スタブ ファイル名)](/cpp/build/reference/stub-ms-dos-stub-file-name)」を参照してください。

- **NoEntryPoint**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、リソースのみの DLL を指定します。

  詳細については、「[/NOENTRY (エントリ ポイントなし)](/cpp/build/reference/noentry-no-entry-point)」を参照してください。

- **ObjectFiles**

  暗黙的な **String[]** 型のパラメーターです。

  リンクされるオブジェクト ファイルを指定します。

- **OptimizeReferences**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、参照されることのない関数および/またはデータを削除します。

  詳細については、「[/OPT (最適化)](/cpp/build/reference/opt-optimizations)」の `REF` 引数を参照してください。

- **OutputFile**

  省略可能な **String** 型のパラメーターです。

  リンカーによって作成されるプログラムの既定の名前と場所をオーバーライドします。

  詳細については、「[/OUT (出力ファイル名)](/cpp/build/reference/out-output-file-name)」を参照してください。

- **PerUserRedirection**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合、出力の登録が有効になっていれば、**HKEY_CLASSES_ROOT** へのレジストリ書き込みは強制的に **HKEY_CURRENT_USER** にリダイレクトされます。

- **PreprocessOutput**

  省略可能な `ITaskItem[]` 型のパラメーターです。

  タスクで使用および生成できるプリプロセッサ出力項目の配列を定義します。

- **PreventDllBinding**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、リンクされたイメージをバインドしないことを *Bind.exe* に指示します。

  詳細については、「[/ALLOWBIND (DLL をバインドしない)](/cpp/build/reference/allowbind-prevent-dll-binding)」を参照してください。

- **Profile**

  省略可能な**ブール値**のパラメーターです。

  `true` の場合は、**パフォーマンス ツール** プロファイラーで使用できる出力ファイルを生成します。

  詳細については、「[/PROFILE (パフォーマンス ツール プロファイラー)](/cpp/build/reference/profile-performance-tools-profiler)」を参照してください。

- **ProfileGuidedDatabase**

  省略可能な **String** 型のパラメーターです。

  実行プログラムに関する情報を保持するために使用される *.pgd* ファイルの名前を指定します。

  詳細については、「[/PGD (ガイド付き最適化のプロファイル用のデータベースの指定)](/cpp/build/reference/pgd-specify-database-for-profile-guided-optimizations)」を参照してください。

- **ProgramDatabaseFile**

  省略可能な **String** 型のパラメーターです。

  リンカーが作成するプログラム データベース (PDB) の名前を指定します。

  詳細については、「[/PDB (プログラム データベースの使用)](/cpp/build/reference/pdb-use-program-database)」を参照してください。

- **RandomizedBaseAddress**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、Windows の ASLR (*Address Space Layout Randomization*) 機能を使用してロード時にランダムに再ベースできる実行可能イメージを生成します。

  詳細については、「[/DYNAMICBASE (ASLR (Address Space Layout Randomization) の使用)](/cpp/build/reference/dynamicbase-use-address-space-layout-randomization)」を参照してください。

- **RegisterOutput**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、このビルドのプライマリ出力を登録します。

- **SectionAlignment**

  省略可能な **Integer** 型のパラメーターです。

  プログラムのリニア アドレス空間内の各セクションの配置を指定します。 パラメーター値はバイト数単位で、2 の累乗です。

  詳細については、「[/ALIGN (セクションの配置)](/cpp/build/reference/align-section-alignment)」を参照してください。

- **SetChecksum**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、 *.exe* ファイルのヘッダー内にチェックサムを設定します。

  詳細については、「[/RELEASE (チェックサムの設定)](/cpp/build/reference/release-set-the-checksum)」を参照してください。

- **ShowProgress**

  省略可能な **String** 型のパラメーターです。

  リンク操作の進行状況レポートの詳細度を指定します。

  次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **NotSet** -  *\<none>*

  - **LinkVerbose** -  **/VERBOSE**

  - **LinkVerboseLib** -  **/VERBOSE:Lib**

  - **LinkVerboseICF** -  **/VERBOSE:ICF**

  - **LinkVerboseREF** -  **/VERBOSE:REF**

  - **LinkVerboseSAFESEH** -  **/VERBOSE:SAFESEH**

  - **LinkVerboseCLR** -  **/VERBOSE:CLR**

  詳細については、「[/VERBOSE (進行状況メッセージの出力)](/cpp/build/reference/verbose-print-progress-messages)」を参照してください。

- **Sources**

  必須の `ITaskItem[]` 型のパラメーターです。

  タスクで使用および生成できる MSBuild ソース ファイル アイテムの配列を定義します。

- **SpecifySectionAttributes**

  省略可能な **String** 型のパラメーターです。

  セクションの属性を指定します。 これは、セクションの *.obj* ファイルがコンパイルされるときに設定された属性をオーバーライドします。

  詳細については、「[/SECTION (セクション属性の指定)](/cpp/build/reference/section-specify-section-attributes)」を参照してください。

- **StackCommitSize**

  省略可能な **String** 型のパラメーターです。

  追加のメモリが割り当てられるときに各割り当ての物理メモリ量を指定します。

  詳細については、「[/STACK (スタック割り当て)](/cpp/build/reference/stack-stack-allocations)」の `commit` 引数を参照してください。

- **StackReserveSize**

  省略可能な **String** 型のパラメーターです。

  仮想メモリ内のスタック割り当て合計サイズを指定します。

  詳細については、「[/STACK (スタック割り当て)](/cpp/build/reference/stack-stack-allocations)」の `reserve` 引数を参照してください。

- **StripPrivateSymbols**

  省略可能な **String** 型のパラメーターです。

  顧客に配布したくないシンボルが省略されたもう一つのプログラム データベース (PDB) ファイルを作成します。 もう一つの PDB ファイルの名前を指定します。

  詳細については、「[/PDBSTRIPPED (プライベート シンボルの除去)](/cpp/build/reference/pdbstripped-strip-private-symbols)」を参照してください。

- **SubSystem**

  省略可能な **String** 型のパラメーターです。

  実行可能ファイルの環境を指定します。

  次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **NotSet** -  *\<none>*

  - **コンソール** -  **/SUBSYSTEM:CONSOLE**

  - **Windows** -  **/SUBSYSTEM:WINDOWS**

  - **ネイティブ** -  **/SUBSYSTEM:NATIVE**

  - **EFI アプリケーション** -  **/SUBSYSTEM:EFI_APPLICATION**

  - **EFI ブート サービス ドライバー** -  **/SUBSYSTEM:EFI_BOOT_SERVICE_DRIVER**

  - **EFI ROM** -  **/SUBSYSTEM:EFI_ROM**

  - **EFI ランタイム** -  **/SUBSYSTEM:EFI_RUNTIME_DRIVER**

  - **WindowsCE** -  **/SUBSYSTEM:WINDOWSCE**

  - **POSIX** -  **/SUBSYSTEM:POSIX**

  詳細については、「[/SUBSYSTEM (サブシステムの指定)](/cpp/build/reference/subsystem-specify-subsystem)」を参照してください。

- **SupportNobindOfDelayLoadedDLL**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、バインドできるインポート アドレス テーブル (IAT) を最終イメージに含めないようリンカーを設定します。

  詳細については、「[/DELAY (遅延読み込みのインポート設定)](/cpp/build/reference/delay-delay-load-import-settings)」の `NOBIND` 引数を参照してください。

- **SupportUnloadOfDelayLoadedDLL**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、DLL の明示的なアンロードをサポートするよう遅延読み込みヘルパー関数を設定します。

  詳細については、「[/DELAY (遅延読み込みのインポート設定)](/cpp/build/reference/delay-delay-load-import-settings)」の `UNLOAD` 引数を参照してください。

- **SuppressStartupBanner**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合、タスクの開始時に著作権およびバージョン番号のメッセージが表示されないようにします。

  詳細については、「[/NOLOGO (著作権情報の非表示) (リンカー)](/cpp/build/reference/nologo-suppress-startup-banner-linker)」を参照してください。

- **SwapRunFromCD**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、まずスワップ ファイルにリンカー出力をコピーして、そこからイメージを実行するようオペレーティング システムを設定します。

  詳細については、「[/SWAPRUN (リンカー出力をスワップ ファイルに読み込む)](/cpp/build/reference/swaprun-load-linker-output-to-swap-file)」の `CD` 引数を参照してください。 **SwapRunFromNET** パラメーターも参照してください。

- **SwapRunFromNET**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、まずスワップ ファイルにリンカー出力をコピーして、そこからイメージを実行するようオペレーティング システムを設定します。

  詳細については、「[/SWAPRUN (リンカー出力をスワップ ファイルに読み込む)](/cpp/build/reference/swaprun-load-linker-output-to-swap-file)」の `NET` 引数を参照してください。 この表にある **SwapRunFromCD** パラメーターも参照してください。

- **TargetMachine**

  省略可能な **String** 型のパラメーターです。

  プログラムまたは DLL のターゲット プラットフォームを指定します。

  次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **NotSet** -  *\<none>*

  - **MachineARM** -  **/MACHINE:ARM**

  - **MachineEBC** -  **/MACHINE:EBC**

  - **MachineIA64** -  **/MACHINE:IA64**

  - **MachineMIPS** -  **/MACHINE:MIPS**

  - **MachineMIPS16** -  **/MACHINE:MIPS16**

  - **MachineMIPSFPU** -  **/MACHINE:MIPSFPU**

  - **MachineMIPSFPU16** -  **/MACHINE:MIPSFPU16**

  - **MachineSH4** -  **/MACHINE:SH4**

  - **MachineTHUMB** -  **/MACHINE:THUMB**

  - **MachineX64** -  **/MACHINE:X64**

  - **MachineX86** -  **/MACHINE:X86**

  詳細については、「[/MACHINE (ターゲット プラットフォームの指定)](/cpp/build/reference/machine-specify-target-platform)」を参照してください。

- **TerminalServerAware**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、プログラム イメージのオプション ヘッダー内の IMAGE_OPTIONAL_HEADER DllCharacteristics フィールドにフラグを設定します。 このフラグが設定されると、ターミナル サーバーはアプリケーションに特定の変更を加えなくなります。

  詳細については、「[/TSAWARE (ターミナル サーバーに対応したアプリケーションの作成)](/cpp/build/reference/tsaware-create-terminal-server-aware-application)」を参照してください。

- **TrackerLogDirectory**

  省略可能な **String** 型のパラメーターです。

  トラッカー ログのディレクトリを指定します。

- **TreatLinkerWarningAsErrors**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合、リンカーが警告を生成したら出力ファイルは生成されません。

  詳細については、「[/WX (リンカー警告をエラーとして扱う)](/cpp/build/reference/wx-treat-linker-warnings-as-errors)」を参照してください。

- **TurnOffAssemblyGeneration**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合は、現在の出力ファイルのイメージを .NET Framework アセンブリなしで作成します。

  詳細については、「[/NOASSEMBLY (MSIL モジュールの作成)](/cpp/build/reference/noassembly-create-a-msil-module)」を参照してください。

- **TypeLibraryFile**

  省略可能な **String** 型のパラメーターです。

  *.tlb* ファイルのファイル名とファイル名拡張子を指定します。 ファイル名、またはパスとファイル名を指定します。

  詳細については、「[/TLBOUT (.tlb ファイル名の指定)](/cpp/build/reference/tlbout-name-dot-tlb-file)」を参照してください。

- **TypeLibraryResourceID**

  省略可能な **Integer** 型のパラメーターです。

  リンカーによって作成されたタイプ ライブラリのユーザー指定値を指定します。 1 から 65535 までの範囲の値を指定します。

  詳細については、「[/TLBID (TypeLib のリソース ID の指定)](/cpp/build/reference/tlbid-specify-resource-id-for-typelib)」を参照してください。

- **UACExecutionLevel**

  省略可能な **String** 型のパラメーターです。

  ユーザー アカウント制御を使用してアプリケーションが実行されるときにアプリケーションに対する要求実行レベルを指定します。

  次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **AsInvoker** - `level='asInvoker'`

  - **HighestAvailable** - `level='highestAvailable'`

  - **RequireAdministrator** - `level='requireAdministrator'`

  詳細については、「[/MANIFESTUAC (UAC 情報をマニフェストに組み込む)](/cpp/build/reference/manifestuac-embeds-uac-information-in-manifest)」の `level` 引数を参照してください。

- **UACUIAccess**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合、アプリケーションはユーザー インターフェイスの保護レベルをバイパスし、デスクトップ上のアクセス許可がより高位のウィンドウに入力を配置します。それ以外の場合は `false` です。

  詳細については、「[/MANIFESTUAC (UAC 情報をマニフェストに組み込む)](/cpp/build/reference/manifestuac-embeds-uac-information-in-manifest)」の `uiAccess` 引数を参照してください。

- **UseLibraryDependencyInputs**

  省略可能な **Boolean** 型のパラメーターです。

  `true` の場合、プロジェクト依存関係のライブラリ出力にリンクされる時に、ライブラリ ファイル自体ではなく、ライブラリアン ツールへの入力が使用されます。

- **Version**

  省略可能な **String** 型のパラメーターです。

  *.exe* または *.dll* ファイルのヘッダーにバージョン番号を入れます。 "`major[.minor]`" を指定します。 `major` および `minor` 引数には、0 から 65535 までの範囲の 10 進数を指定します。

  詳細については、「[/VERSION (バージョン情報)](/cpp/build/reference/version-version-information)」を参照してください。

## <a name="see-also"></a>関連項目

- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
