---
title: Link タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
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
- MSBuild (Visual C++), Link task
- Link task (MSBuild (Visual C++))
ms.assetid: 0a61f168-3113-4fa7-83a3-d9142e2a33f8
caps.latest.revision: 16
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 181c32017a84328037ea46d49698821fa3cb41ea
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295878"
---
# <a name="link-task"></a>Link タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual C++ リンカー ツール (link.exe) をラップします。 リンカー ツールは、COFF (Common Object File Format) オブジェクト ファイルとライブラリをリンクし、実行可能ファイル (.exe) やダイナミック リンク ライブラリ (DLL) を生成します。 詳細については、「[リンカー オプション](https://msdn.microsoft.com/library/c1d51b8a-bd23-416d-81e4-900e02b2c129)」を参照してください。  
  
## <a name="parameters"></a>パラメーター  
 **Link** タスクのパラメーターの説明を次の表に示します。 タスク パラメーターの大部分とパラメーターのいくつかのセットは、コマンド ライン オプションに対応します。  
  
- **AdditionalDependencies**  
  
   省略可能な **String[]** 型のパラメーターです。  
  
   コマンドに追加する入力ファイルのリストを指定します。  
  
   詳細については、「[LINK 入力ファイル](https://msdn.microsoft.com/library/bb26fcc5-509a-4620-bc3e-b6c6e603a412)」を参照してください。  
  
- **AdditionalLibraryDirectories**  
  
   省略可能な **String[]** 型のパラメーターです。  
  
   環境ライブラリ パスをオーバーライドします。 ディレクトリ名を指定します。  
  
   詳細については、「[/LIBPATH (追加ライブラリのパス)](https://msdn.microsoft.com/library/7240af0b-9a3d-4d53-8169-2a92cd6958ba)」を参照してください。  
  
- **AdditionalManifestDependencies**  
  
   省略可能な **String[]** 型のパラメーターです。  
  
   マニフェスト ファイルの `dependency` セクションに置かれる属性を指定します。  
  
   詳細については、「[/MANIFESTDEPENDENCY (マニフェストの依存関係を指定する)](https://msdn.microsoft.com/library/e4b68313-33a2-4c3e-908e-ac2b9f7d6a73)」を参照してください。 [MSDN](https://go.microsoft.com/fwlink/?LinkId=737) Web サイト上の「パブリッシャー構成ファイル」も参照してください。  
  
- **AdditionalOptions**  
  
   省略可能な **String** 型のパラメーターです。  
  
   コマンド ラインで指定するリンカー オプションのリストです。 たとえば、 **"** _/option1 /option2 /option#_ " のような形式です。 他の **Link** タスク パラメーターでは表されないリンカー オプションを指定する場合は、このパラメーターを使用します。  
  
   詳細については、「[リンカー オプション](https://msdn.microsoft.com/library/c1d51b8a-bd23-416d-81e4-900e02b2c129)」を参照してください。  
  
- **AddModuleNamesToAssembly**  
  
   省略可能な **String[]** 型のパラメーターです。  
  
   アセンブリのモジュール参照を追加します。  
  
   詳細については、「[/ASSEMBLYMODULE (MSIL モジュールのアセンブリへの追加)](https://msdn.microsoft.com/library/67357da8-e4b6-49fd-932c-329a5777f143)」を参照してください。  
  
- **AllowIsolation**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合、オペレーティング システムはマニフェストの検索と読み込みを行います。 `false` の場合は、あたかもマニフェストがないかのように DLL を読み込むことを示します。  
  
   詳細については、「[/ALLOWISOLATION (マニフェスト検索)](https://msdn.microsoft.com/library/6d41851e-b3c1-4bdf-beaa-031773089d6f)」を参照してください。  
  
- **AssemblyDebug**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、**DebuggableAttribute** 属性をデバッグ情報追跡と一緒に出力し、JIT 最適化を無効にします。 `false` の場合は、**DebuggableAttribute** 属性を出力しますが、デバッグ情報追跡を無効にし、JIT 最適化を有効にします。  
  
   詳細については、「[/ASSEMBLYDEBUG (DebuggableAttribute の追加)](https://msdn.microsoft.com/library/94443af3-470c-41d7-83a0-7434563d7982)」を参照してください。  
  
- **AssemblyLinkResource**  
  
   省略可能な **String[]** 型のパラメーターです。  
  
   出力ファイル内で .NET Framework リソースへのリンクを作成します。リソース ファイルは出力ファイル内に置かれません。 リソースの名前を指定します。  
  
   詳細については、「[/ASSEMBLYLINKRESOURCE (.NET Framework リソースへのリンク)](https://msdn.microsoft.com/library/8b6ad184-1b33-47a4-8513-4803cf915b64)」を参照してください。  
  
- **AttributeFileTracking**  
  
   暗黙的な**ブール値**のパラメーターです。  
  
   詳細なファイル追跡でリンク インクリメンタルの動作をキャプチャできるようにします。 常に `true` を返します。  
  
- **BaseAddress**  
  
   省略可能な **String** 型のパラメーターです。  
  
   ビルド対象のプログラムまたは DLL のベース アドレスを設定します。 `{address[,size] | @filename,key}`を指定します。  
  
   詳細については、「[/BASE (ベース アドレス)](https://msdn.microsoft.com/library/00b9f6fe-0bd2-4772-a69c-7365eb199069)」を参照してください。  
  
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
  
    詳細については、「[/CLRIMAGETYPE (CLR イメージのタイプの指定)](https://msdn.microsoft.com/library/04c60ee6-9dd7-4391-bc03-6926ad0fa116)」を参照してください。  
  
- **CLRSupportLastError**  
  
   省略可能な **String** 型のパラメーターです。  
  
   P/Invoke 機構を通じて呼び出された関数の最終エラー コードを保持します。  
  
   次のいずれかの値を指定します。各値はリンカー オプションに対応しています。  
  
  - **Enabled** -  **/CLRSupportLastError**  
  
  - **Disabled** -  **/CLRSupportLastError:NO**  
  
  - **SystemDlls** -  **/CLRSupportLastError:SYSTEMDLL**  
  
    詳細については、「[/CLRSUPPORTLASTERROR (PInvoke 呼び出しの最終エラー コードの保持)](https://msdn.microsoft.com/library/b7057990-4154-4b1d-9fc9-6236f7be7575)」を参照してください。  
  
- **CLRThreadAttribute**  
  
   省略可能な **String** 型のパラメーターです。  
  
   CLR プログラムのエントリ ポイントにスレッド属性を明示的に指定します。  
  
   次のいずれかの値を指定します。各値はリンカー オプションに対応しています。  
  
  - **DefaultThreadingAttribute** -  **/CLRTHREADATTRIBUTE:NONE**  
  
  - **MTAThreadingAttribute** -  **/CLRTHREADATTRIBUTE:MTA**  
  
  - **STAThreadingAttribute** -  **/CLRTHREADATTRIBUTE:STA**  
  
    詳細については、「[/CLRTHREADATTRIBUTE (CLR スレッド属性の設定)](https://msdn.microsoft.com/library/4907e9ef-5031-446c-aecf-0a0b32fae1e8)」を参照してください。  
  
- **CLRUnmanagedCodeCheck**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   マネージド コードからネイティブ DLL への、リンカーによって生成された P/Invoke 呼び出しに対して、**SuppressUnmanagedCodeSecurityAttribute** を適用するかどうかを指定します。  
  
   詳細については、「[/CLRUNMANAGEDCODECHECK (SuppressUnmanagedCodeSecurityAttribute の追加)](https://msdn.microsoft.com/library/73abc426-dab0-45e2-be85-0f9a14206cc2)」を参照してください。  
  
- **CreateHotPatchableImage**  
  
   省略可能な **String** 型のパラメーターです。  
  
   イメージをホットパッチできるようにします。  
  
   次のいずれかの値を指定します。値はリンカー オプションに対応しています。  
  
  - **Enabled** -  **/FUNCTIONPADMIN**  
  
  - **X86Image** -  **/FUNCTIONPADMIN:5**  
  
  - **X64Image** -  **/FUNCTIONPADMIN:6**  
  
  - **ItaniumImage** -  **/FUNCTIONPADMIN:16**  
  
    詳細については、「[/FUNCTIONPADMIN (ホットパッチ可能なイメージの作成)](https://msdn.microsoft.com/library/25b02c13-1add-4fbd-add9-fcb30eb2cae7)」を参照してください。  
  
- **DataExecutionPrevention**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、実行可能ファイルで Windows データ実行防止機能との互換性がテストされたことを示します。  
  
   詳細については、「[/NXCOMPAT (データ実行防止との互換性)](https://msdn.microsoft.com/library/5858e7ff-24d3-4ac3-9046-af2c9e220d9b)」を参照してください。  
  
- **DelayLoadDLLs**  
  
   省略可能な **String[]** 型のパラメーターです。  
  
   このパラメーターにより、DLL の*遅延読み込み*が行われます。 遅延読み込みする DLL の名前を指定します。  
  
   詳細については、「[/DELAYLOAD (遅延読み込みのインポート)](https://msdn.microsoft.com/library/39ea0f1e-5c01-450f-9c75-2d9761ff9b28)」を参照してください。  
  
- **DelaySign**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、アセンブリに部分署名します。 既定では、値は `false` です。  
  
   詳細については、「[/DELAYSIGN (アセンブリの部分署名)](https://msdn.microsoft.com/library/15244d30-3ecb-492f-a408-ffe81f38de20)」を参照してください。  
  
- **Driver**  
  
   省略可能な **String** 型のパラメーターです。  
  
   Windows NT カーネル モード ドライバーをビルドするには、このパラメーターを指定します。  
  
   次のいずれかの値を指定します。各値はリンカー オプションに対応しています。  
  
  - **NotSet** -  *\<none>*  
  
  - **Driver** -  **/Driver**  
  
  - **UpOnly** -  **/DRIVER:UPONLY**  
  
  - **WDM** -  **/DRIVER:WDM**  
  
    詳細については、「[/DRIVER (Windows NT カーネル モード ドライバー)](https://msdn.microsoft.com/library/aeee8e28-5d97-40f5-ba16-9f370fe8a1b8)」を参照してください。  
  
- **EmbedManagedResourceFile**  
  
   省略可能な **String[]** 型のパラメーターです。  
  
   リソース ファイルをアセンブリに埋め込みます。 必要なリソース ファイル名を指定します。 必要に応じて、論理名 (リソースの読み込みに使用される) および **PRIVATE** オプション (リソース ファイルがプライベートであることをアセンブリ マニフェストで示す) を指定します。  
  
   詳細については、「[/ASSEMBLYRESOURCE (マネージド リソースの埋め込み)](https://msdn.microsoft.com/library/0ce6e1fb-921b-4b1b-a59c-d35388d789f2)」を参照してください。  
  
- **EnableCOMDATFolding**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、同一の COMDAT が折りたたまれ (圧縮され) ます。  
  
   詳細については、「[/OPT (最適化)](https://msdn.microsoft.com/library/8f229863-5f53-48a8-9478-243a647093ac)」の `ICF[= iterations]` 引数を参照してください。  
  
- **EnableUAC**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、ユーザー アカウント制御 (UAC) 情報をプログラム マニフェストに組み込むことを指定します。  
  
   詳細については、「[/MANIFESTUAC (UAC 情報をマニフェストに組み込む)](https://msdn.microsoft.com/library/2d243c39-fa13-493c-b56f-d0d972a1603a)」を参照してください。  
  
- **EntryPointSymbol**  
  
   省略可能な **String** 型のパラメーターです。  
  
   .exe ファイルまたは DLL の開始アドレスとしてエントリ ポイント関数を指定します。 パラメーター値として関数名を指定します。  
  
   詳細については、「[/ENTRY (エントリ ポイント シンボル)](https://msdn.microsoft.com/library/26c62ba2-4f52-4882-a7bd-7046a0abf445)」を参照してください。  
  
- **FixedBaseAddress**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、指定のベース アドレスだけに読み込まれるプログラムまたは DLL を作成します。  
  
   詳細については、「[/FIXED (固定ベース アドレス)](https://msdn.microsoft.com/library/929bba5e-b7d8-40ed-943e-056aa3710fc5)」を参照してください。  
  
- **ForceFileOutput**  
  
   省略可能な **String** 型のパラメーターです。  
  
   未定義のシンボルが参照された場合や、シンボルが複数回定義された場合でも、有効な .exe ファイルまたは DLL を作成するようリンカーを設定します。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **Enabled** -  **/FORCE**  
  
  - **MultiplyDefinedSymbolOnly** -  **/FORCE:MULTIPLE**  
  
  - **UndefinedSymbolOnly** -  **/FORCE:UNRESOLVED**  
  
    詳細については、「[/FORCE (ファイルを強制的に出力)](https://msdn.microsoft.com/library/b1e9a218-a5eb-4e60-a4a4-65b4be15e5da)」を参照してください。  
  
- **ForceSymbolReferences**  
  
   省略可能な **String[]** 型のパラメーターです。  
  
   このパラメーターは、指定されたシンボルをシンボル テーブルに追加するようリンカーを設定します。  
  
   詳細については、「[/INCLUDE (シンボル参照の強制)](https://msdn.microsoft.com/library/4a039677-360a-480f-bd0b-448e239b449c)」を参照してください。  
  
- **FunctionOrder**  
  
   省略可能な **String** 型のパラメーターです。  
  
   このパラメーターは、指定されたパッケージ化関数 (COMDAT) をあらかじめ決められた順序でイメージに入れることによって、プログラムを最適化します。  
  
   詳細については、「[/ORDER (関数の順序)](https://msdn.microsoft.com/library/ecf5eb3e-e404-4e86-9a91-4e5ec157261a)」を参照してください。  
  
- **GenerateDebugInformation**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、.exe ファイルまたは DLL のデバッグ情報を生成します。  
  
   詳細については、「[/DEBUG (デバッグ情報の生成)](https://msdn.microsoft.com/library/1af389ae-3f8b-4d76-a087-1cdf861e9103)」を参照してください。  
  
- **GenerateManifest**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、side-by-side マニフェスト ファイルを作成します。  
  
   詳細については、「[/MANIFEST (side-by-side アセンブリ マニフェストを作成する)](https://msdn.microsoft.com/library/98c52e1e-712c-4f49-b149-4d0a3501b600)」を参照してください。  
  
- **GenerateMapFile**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、*マップ ファイル*を作成します。 マップ ファイルのファイル名拡張子は、.map です。  
  
   詳細については、「[/MAP (マップ ファイルの生成)](https://msdn.microsoft.com/library/9ccce53d-4e36-43da-87b0-7603ddfdea63)」を参照してください。  
  
- **HeapCommitSize**  
  
   省略可能な **String** 型のパラメーターです。  
  
   一度に割り当てるヒープの物理メモリ量を指定します。  
  
   詳細については、「[/HEAP (ヒープ サイズの設定)](https://msdn.microsoft.com/library/a3f71927-7f1d-492c-9fdb-dfccb1a043da)」の `commit` 引数を参照してください。 **HeapReserveSize** パラメーターも参照してください。  
  
- **HeapReserveSize**  
  
   省略可能な **String** 型のパラメーターです。  
  
   仮想メモリ内のヒープ割り当ての合計を指定します。  
  
   詳細については、「[/HEAP (ヒープ サイズの設定)](https://msdn.microsoft.com/library/a3f71927-7f1d-492c-9fdb-dfccb1a043da)」の `reserve` 引数を参照してください。 この表にある **HeapCommitSize** パラメーターも参照してください。  
  
- **IgnoreAllDefaultLibraries**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、外部参照の解決時に検索するライブラリ リストから 1 つ以上の既定のライブラリを削除するようリンカーを設定します。  
  
   詳細については、「[/NODEFAULTLIB (ライブラリを無視する)](https://msdn.microsoft.com/library/7270b673-6711-468e-97a7-c2925ac2be6e)」を参照してください。  
  
- **IgnoreEmbeddedIDL**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、ソース コード内の IDL 属性を .idl ファイルに処理しないことを指定します。  
  
   詳細については、「[/IGNOREIDL (属性を MIDL に挿入しない)](https://msdn.microsoft.com/library/29514098-6a1c-4317-af2f-1dc268972780)」を参照してください。  
  
- **IgnoreImportLibrary**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合、この構成で生成されるインポート ライブラリは、依存プロジェクトにインポートされません。  
  
   このパラメーターは、リンカー オプションに対応していません。  
  
- **IgnoreSpecificDefaultLibraries**  
  
   省略可能な **String[]** 型のパラメーターです。  
  
   無視する既定のライブラリの名前を 1 つ以上指定します。 複数のライブラリはセミコロンで区切ります。  
  
   詳細については、「[/NODEFAULTLIB (ライブラリを無視する)](https://msdn.microsoft.com/library/7270b673-6711-468e-97a7-c2925ac2be6e)」を参照してください。  
  
- **ImageHasSafeExceptionHandlers**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合、リンカーは、イメージの安全な例外ハンドラーのテーブルも生成できる場合のみ、イメージを生成します。  
  
   詳細については、「[/SAFESEH (安全な例外ハンドラーがあるイメージ)](https://msdn.microsoft.com/library/7722ff99-b833-4c65-a855-aaca902ffcb7)」を参照してください。  
  
- **ImportLibrary**  
  
   既定のライブラリ名と置き換わるユーザー指定のインポート ライブラリの名前です。  
  
   詳細については、「[/IMPLIB (インポート ライブラリ名の設定)](https://msdn.microsoft.com/library/fe8f71ab-7055-41b5-8ef8-2b97cfa4a432)」を参照してください。  
  
- **KeyContainer**  
  
   省略可能な **String** 型のパラメーターです。  
  
   署名付きアセンブリのキーを含むコンテナーです。  
  
   詳細については、「[/KEYCONTAINER (アセンブリに署名するためのキー コンテナーの指定)](https://msdn.microsoft.com/library/94882d12-b77a-49c7-96d0-18a31aee001e)」を参照してください。 この表にある **KeyFile** パラメーターも参照してください。  
  
- **KeyFile**  
  
   省略可能な **String** 型のパラメーターです。  
  
   署名付きアセンブリのキーを含むファイルを指定します。  
  
   詳細については、「[/KEYFILE (アセンブリに署名するためのキーまたはキー ペアの指定)](https://msdn.microsoft.com/library/9b71f8c0-541c-4fe5-a0c7-9364f42ecb06)」を参照してください。 **KeyContainer** パラメーターも参照してください。  
  
- **LargeAddressAware**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合、アプリケーションは 2 ギガバイトを超えるアドレスを処理できます。  
  
   詳細については、「[/LARGEADDRESSAWARE (大きいアドレスの処理)](https://msdn.microsoft.com/library/a29756c8-e893-47a9-9750-1f0d25359385)」を参照してください。  
  
- **LinkDLL**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、メイン出力ファイルとして DLL をビルドします。  
  
   詳細については、「[/DLL (DLL のビルド)](https://msdn.microsoft.com/library/c7685aec-31d0-490f-9503-fb5171a23609)」を参照してください。  
  
- **LinkErrorReporting**  
  
   省略可能な **String** 型のパラメーターです。  
  
   内部コンパイル エラー (ICE) 情報を Microsoft に直接報告できます。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **NoErrorReport** -  **/ERRORREPORT:NONE**  
  
  - **PromptImmediately** -  **/ERRORREPORT:PROMPT**  
  
  - **QueueForNextLogin** -  **/ERRORREPORT:QUEUE**  
  
  - **SendErrorReport** -  **/ERRORREPORT:SEND**  
  
    詳細については、「[/ERRORREPORT (内部リンカー エラーの報告)](https://msdn.microsoft.com/library/f5fab595-a2f1-4eb0-ab5c-1c0fbd3d8c28)」を参照してください。  
  
- **LinkIncremental**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、インクリメンタル リンクを有効にします。  
  
   詳細については、「[/INCREMENTAL (インクリメンタル リンクを行う)](https://msdn.microsoft.com/library/135656ff-94fa-4ad4-a613-22e1a2a5d16b)」を参照してください。  
  
- **LinkLibraryDependencies**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、プロジェクト依存関係からのライブラリ出力を自動的にリンクすることを指定します。  
  
   このパラメーターは、リンカー オプションに対応していません。  
  
- **LinkStatus**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、リンクの何パーセントが完了したかを示す進行状況のインジケーターをリンカーが表示することを指定します。  
  
   詳細については、「[/LTCG (リンク時のコード生成)](https://msdn.microsoft.com/library/788c6f52-fdb8-40c2-90af-4026ea2cf2e2)」の `STATUS` 引数を参照してください。  
  
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
  
    詳細については、「[/LTCG (リンク時のコード生成)](https://msdn.microsoft.com/library/788c6f52-fdb8-40c2-90af-4026ea2cf2e2)」を参照してください。  
  
- **ManifestFile**  
  
   省略可能な **String** 型のパラメーターです。  
  
   既定のマニフェスト ファイル名を、指定されたファイル名に変更します。  
  
   詳細については、「[/MANIFESTFILE (マニフェスト ファイルに名前を付ける)](https://msdn.microsoft.com/library/befa5ab2-a9cf-4c9b-969a-e7b4a930f08d)」を参照してください。  
  
- **MapExports**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、エクスポートされた関数をマップ ファイルに含めるようリンカーを設定します。  
  
   詳細については、「[/MAPINFO (マップ ファイルに含める情報)](https://msdn.microsoft.com/library/533d2bce-f9b7-4fea-ae1c-0b4864c9d10b)」の `EXPORTS` 引数を参照してください。  
  
- **MapFileName**  
  
   省略可能な **String** 型のパラメーターです。  
  
   既定のマップ ファイル名を、指定されたファイル名に変更します。  
  
- **MergedIDLBaseFileName**  
  
   省略可能な **String** 型のパラメーターです。  
  
   .idl ファイルのファイル名とファイル名拡張子を指定します。  
  
   詳細については、「[/IDLOUT (MIDL 出力ファイルの指定)](https://msdn.microsoft.com/library/10d00a6a-85b4-4de1-8732-e422c6931509)」を参照してください。  
  
- **MergeSections**  
  
   省略可能な **String** 型のパラメーターです。  
  
   イメージ内のセクションを結合します。 `from-section=to-section` を指定します。  
  
   詳細については、「[/MERGE (セクションの結合)](https://msdn.microsoft.com/library/10fb20c2-0b3f-4c8d-98a8-f69aedf03d52)」を参照してください。  
  
- **MidlCommandFile**  
  
   省略可能な **String** 型のパラメーターです。  
  
   MIDL コマンド ライン オプションを含むファイルの名前を指定します。  
  
   詳細については、「[/MIDL (MIDL コマンド ライン オプションの指定)](https://msdn.microsoft.com/library/22dc259e-b34c-4ed3-a380-4beb734482c1)」を参照してください。  
  
- **MinimumRequiredVersion**  
  
   省略可能な **String** 型のパラメーターです。  
  
   サブシステムの最低限必要なバージョンを指定します。 引数には、0 から 65535 までの範囲の 10 進数を指定します。  
  
- **ModuleDefinitionFile**  
  
   省略可能な **String** 型のパラメーターです。  
  
   [モジュール定義ファイル](https://msdn.microsoft.com/library/08c0bc28-c5d2-47aa-9624-7fc68bcaa4d8)の名前を指定します。  
  
   詳細については、「[/DEF (モジュール定義ファイルの指定)](https://msdn.microsoft.com/library/6497fa68-65f0-48ca-8f66-b87166fc631a)」を参照してください。  
  
- **MSDOSStubFileName**  
  
   省略可能な **String** 型のパラメーターです。  
  
   指定された MS-DOS スタブ プログラムを Win32 プログラムにアタッチします。  
  
   詳細については、「[/STUB (MS-DOS スタブ ファイル名)](https://msdn.microsoft.com/library/65221ffe-4f9a-4a14-ac69-3cfb79b40b5f)」を参照してください。  
  
- **NoEntryPoint**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、リソースのみの DLL を指定します。  
  
   詳細については、「[/NOENTRY (エントリ ポイントなし)](https://msdn.microsoft.com/library/0214dd41-35ad-43ab-b892-e636e038621a)」を参照してください。  
  
- **ObjectFiles**  
  
   暗黙的な **String[]** 型のパラメーターです。  
  
   リンクされるオブジェクト ファイルを指定します。  
  
- **OptimizeReferences**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、参照されることのない関数および/またはデータを削除します。  
  
   詳細については、「[/OPT (最適化)](https://msdn.microsoft.com/library/8f229863-5f53-48a8-9478-243a647093ac)」の `REF` 引数を参照してください。  
  
- **OutputFile**  
  
   省略可能な **String** 型のパラメーターです。  
  
   リンカーによって作成されるプログラムの既定の名前と場所をオーバーライドします。  
  
   詳細については、「[/OUT (出力ファイル名)](https://msdn.microsoft.com/library/976210a4-e51f-4cfb-af5e-c16344455834)」を参照してください。  
  
- **PerUserRedirection**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合、出力の登録が有効になっていれば、**HKEY_CLASSES_ROOT** へのレジストリ書き込みは強制的に **HKEY_CURRENT_USER** にリダイレクトされます。  
  
- **PreprocessOutput**  
  
   省略可能な `ITaskItem[]` 型のパラメーターです。  
  
   タスクで使用および生成できるプリプロセッサ出力項目の配列を定義します。  
  
- **PreventDllBinding**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、リンクされたイメージをバインドしないことを Bind.exe に指示します。  
  
   詳細については、「[/ALLOWBIND (DLL をバインドしない)](https://msdn.microsoft.com/library/30e37e24-12e4-407e-988a-39d357403598)」を参照してください。  
  
- **Profile**  
  
   省略可能な**ブール値**のパラメーターです。  
  
   `true` の場合は、**パフォーマンス ツール** プロファイラーで使用できる出力ファイルを生成します。  
  
   詳細については、「[/PROFILE (パフォーマンス ツール プロファイラー)](https://msdn.microsoft.com/library/e676baa1-5063-47a3-a357-ba0d1f0d1699)」を参照してください。  
  
- **ProfileGuidedDatabase**  
  
   省略可能な **String** 型のパラメーターです。  
  
   実行プログラムに関する情報を保持するために使用される .pgd ファイルの名前を指定します。  
  
   詳細については、「[/PGD (ガイド付き最適化のプロファイル用のデータベースの指定)](https://msdn.microsoft.com/library/9f312498-493b-461f-886f-92652257e443)」を参照してください。  
  
- **ProgramDatabaseFile**  
  
   省略可能な **String** 型のパラメーターです。  
  
   リンカーが作成するプログラム データベース (PDB) の名前を指定します。  
  
   詳細については、「[/PDB (プログラム データベースの使用)](https://msdn.microsoft.com/library/d23db0ce-10cb-427a-bc60-d6b2a852723d)」を参照してください。  
  
- **RandomizedBaseAddress**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、Windows の ASLR (*Address Space Layout Randomization*) 機能を使用してロード時にランダムに再ベースできる実行可能イメージを生成します。  
  
   詳細については、「[/DYNAMICBASE (ASLR (Address Space Layout Randomization) の使用)](https://msdn.microsoft.com/library/6c0ced8e-fe9c-4b63-b956-eb8a55fbceb2)」を参照してください。  
  
- **RegisterOutput**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、このビルドのプライマリ出力を登録します。  
  
- **SectionAlignment**  
  
   省略可能な **Integer** 型のパラメーターです。  
  
   プログラムのリニア アドレス空間内の各セクションの配置を指定します。 パラメーター値はバイト数単位で、2 の累乗です。  
  
   詳細については、「[/ALIGN (セクションの配置)](https://msdn.microsoft.com/library/f2f8ac24-e90e-4bea-8205-f2960a3b1740)」を参照してください。  
  
- **SetChecksum**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、.exe ファイルのヘッダー内にチェックサムを設定します。  
  
   詳細については、「[/RELEASE (チェックサムの設定)](https://msdn.microsoft.com/library/93bcadf4-29ac-4824-914b-6997e3751d22)」を参照してください。  
  
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
  
    詳細については、「[/VERBOSE (進行状況メッセージの出力)](https://msdn.microsoft.com/library/9c347d98-4c37-4724-a39e-0983934693ab)」を参照してください。  
  
- **Sources**  
  
   必須の `ITaskItem[]` 型のパラメーターです。  
  
   タスクで使用および生成できる MSBuild ソース ファイル アイテムの配列を定義します。  
  
- **SpecifySectionAttributes**  
  
   省略可能な **String** 型のパラメーターです。  
  
   セクションの属性を指定します。 これは、セクションの .obj ファイルがコンパイルされるときに設定された属性をオーバーライドします。  
  
   詳細については、「[/SECTION (セクション属性の指定)](https://msdn.microsoft.com/library/92b69d81-e421-462e-b46f-7d0dff9b9d16)」を参照してください。  
  
- **StackCommitSize**  
  
   省略可能な **String** 型のパラメーターです。  
  
   追加のメモリが割り当てられるときに各割り当ての物理メモリ量を指定します。  
  
   詳細については、「[/STACK (スタック割り当て)](https://msdn.microsoft.com/library/73283660-e4bd-47cc-b5ca-04c5d739034c)」の `commit` 引数を参照してください。  
  
- **StackReserveSize**  
  
   省略可能な **String** 型のパラメーターです。  
  
   仮想メモリ内のスタック割り当て合計サイズを指定します。  
  
   詳細については、「[/STACK (スタック割り当て)](https://msdn.microsoft.com/library/73283660-e4bd-47cc-b5ca-04c5d739034c)」の `reserve` 引数を参照してください。  
  
- **StripPrivateSymbols**  
  
   省略可能な **String** 型のパラメーターです。  
  
   顧客に配布したくないシンボルが省略されたもう一つのプログラム データベース (PDB) ファイルを作成します。 もう一つの PDB ファイルの名前を指定します。  
  
   詳細については、「[/PDBSTRIPPED (プライベート シンボルの除去)](https://msdn.microsoft.com/library/9b9e0070-6a13-4142-8180-19c003fbbd55)」を参照してください。  
  
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
  
    詳細については、「[/SUBSYSTEM (サブシステムの指定)](https://msdn.microsoft.com/library/d7b133cf-cf22-4da8-ab46-6552702c0b9b)」を参照してください。  
  
- **SupportNobindOfDelayLoadedDLL**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、バインドできるインポート アドレス テーブル (IAT) を最終イメージに含めないようリンカーを設定します。  
  
   詳細については、「[/DELAY (遅延読み込みのインポート設定)](https://msdn.microsoft.com/library/9334b332-cc58-4dae-b10f-a4c75972d50c)」の `NOBIND` 引数を参照してください。  
  
- **SupportUnloadOfDelayLoadedDLL**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、DLL の明示的なアンロードをサポートするよう遅延読み込みヘルパー関数を設定します。  
  
   詳細については、「[/DELAY (遅延読み込みのインポート設定)](https://msdn.microsoft.com/library/9334b332-cc58-4dae-b10f-a4c75972d50c)」の `UNLOAD` 引数を参照してください。  
  
- **SuppressStartupBanner**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合、タスクの開始時に著作権およびバージョン番号のメッセージが表示されないようにします。  
  
   詳細については、「[/NOLOGO (著作権情報の非表示) (リンカー)](https://msdn.microsoft.com/library/3b20dddd-eca6-4545-a331-9f70bf720197)」を参照してください。  
  
- **SwapRunFromCD**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、まずスワップ ファイルにリンカー出力をコピーして、そこからイメージを実行するようオペレーティング システムを設定します。  
  
   詳細については、「[/SWAPRUN (リンカー出力をスワップ ファイルに読み込む)](https://msdn.microsoft.com/library/4a1e7f46-4399-4161-8dfc-d6a71beaf683)」の `CD` 引数を参照してください。 **SwapRunFromNET** パラメーターも参照してください。  
  
- **SwapRunFromNET**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、まずスワップ ファイルにリンカー出力をコピーして、そこからイメージを実行するようオペレーティング システムを設定します。  
  
   詳細については、「[/SWAPRUN (リンカー出力をスワップ ファイルに読み込む)](https://msdn.microsoft.com/library/4a1e7f46-4399-4161-8dfc-d6a71beaf683)」の `NET` 引数を参照してください。 この表にある **SwapRunFromCD** パラメーターも参照してください。  
  
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
  
    詳細については、「[/MACHINE (ターゲット プラットフォームの指定)](https://msdn.microsoft.com/library/8d41bf4b-7e53-4ab9-9085-d852b08d31c2)」を参照してください。  
  
- **TerminalServerAware**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、プログラム イメージのオプション ヘッダー内の IMAGE_OPTIONAL_HEADER DllCharacteristics フィールドにフラグを設定します。 このフラグが設定されると、ターミナル サーバーはアプリケーションに特定の変更を加えなくなります。  
  
   詳細については、「[/TSAWARE (ターミナル サーバーに対応したアプリケーションの作成)](https://msdn.microsoft.com/library/fe1c1846-de5b-4839-b562-93fbfe36cd29)」を参照してください。  
  
- **TrackerLogDirectory**  
  
   省略可能な **String** 型のパラメーターです。  
  
   トラッカー ログのディレクトリを指定します。  
  
- **TreatLinkerWarningAsErrors**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合、リンカーが警告を生成したら出力ファイルは生成されません。  
  
   詳細については、「[/WX (リンカー警告をエラーとして扱う)](https://msdn.microsoft.com/library/e4ba97c7-93f7-43ae-a4bb-d866790926c9)」を参照してください。  
  
- **TurnOffAssemblyGeneration**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合は、現在の出力ファイルのイメージを .NET Framework アセンブリなしで作成します。  
  
   詳細については、「[/NOASSEMBLY (MSIL モジュールの作成)](https://msdn.microsoft.com/library/3cea4e70-f451-4395-a626-1930b1b127fe)」を参照してください。  
  
- **TypeLibraryFile**  
  
   省略可能な **String** 型のパラメーターです。  
  
   .tlb ファイルのファイル名とファイル名拡張子を指定します。 ファイル名、またはパスとファイル名を指定します。  
  
   詳細については、「[/TLBOUT (.TLB ファイル名の指定)](https://msdn.microsoft.com/library/0df6d078-2e48-46c9-a1a5-02674d85dce8)」を参照してください。  
  
- **TypeLibraryResourceID**  
  
   省略可能な **Integer** 型のパラメーターです。  
  
   リンカーによって作成されたタイプ ライブラリのユーザー指定値を指定します。 1 から 65535 までの範囲の値を指定します。  
  
   詳細については、「[/TLBID (TypeLib のリソース ID の指定)](https://msdn.microsoft.com/library/434b28a2-4656-4d52-ac82-8b18bf486fb2)」を参照してください。  
  
- **UACExecutionLevel**  
  
   省略可能な **String** 型のパラメーターです。  
  
   ユーザー アカウント制御を使用してアプリケーションが実行されるときにアプリケーションに対する要求実行レベルを指定します。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **AsInvoker** - `level='asInvoker'`  
  
  - **HighestAvailable** - `level='highestAvailable'`  
  
  - **RequireAdministrator** - `level='requireAdministrator'`  
  
    詳細については、「[/MANIFESTUAC (UAC 情報をマニフェストに組み込む)](https://msdn.microsoft.com/library/2d243c39-fa13-493c-b56f-d0d972a1603a)」の `level` 引数を参照してください。  
  
- **UACUIAccess**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合、アプリケーションはユーザー インターフェイスの保護レベルをバイパスし、デスクトップ上のアクセス許可がより高位のウィンドウに入力を配置します。それ以外の場合は `false` です。  
  
   詳細については、「[/MANIFESTUAC (UAC 情報をマニフェストに組み込む)](https://msdn.microsoft.com/library/2d243c39-fa13-493c-b56f-d0d972a1603a)」の `uiAccess` 引数を参照してください。  
  
- **UseLibraryDependencyInputs**  
  
   省略可能な **Boolean** 型のパラメーターです。  
  
   `true` の場合、プロジェクト依存関係のライブラリ出力にリンクされる時に、ライブラリ ファイル自体ではなく、ライブラリアン ツールへの入力が使用されます。  
  
- **Version**  
  
   省略可能な **String** 型のパラメーターです。  
  
   .exe または .dll ファイルのヘッダーにバージョン番号を入れます。 "`major[.minor]`" を指定します。 `major` および `minor` 引数には、0 から 65535 までの範囲の 10 進数を指定します。  
  
   詳細については、「[/VERSION (バージョン情報)](https://msdn.microsoft.com/library/b86d0e86-dca6-4316-aee2-d863ccb9f223)」を参照してください。  
  
## <a name="see-also"></a>関連項目
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)
