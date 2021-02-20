---
title: CL タスク | Microsoft Docs
description: Microsoft C++ コンパイラ ツールである cl.exe をラップする、MSBuild CL タスクの目的とパラメーターについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VC.Project.VCCLCompilerTool.UseUnicodeForAssemblerListing
- vc.task.cl
- VC.Project.VCCLCompilerTool.TreatSpecificWarningsAsErrors
- VC.Project.VCCLCompilerTool.CreateHotpatchableImage
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild (C++), CL task
- CL task (MSBuild (C++))
ms.assetid: 651ba971-b755-4f03-a549-4816beb3cc0d
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 542d84f4c0279c1f76fa1ea29a244e78c53b394d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99878436"
---
# <a name="cl-task"></a>CL タスク

Microsoft C++ コンパイラ ツール *cl.exe* をラップします。 コンパイラは、実行可能ファイル ( *.exe*)、ダイナミック リンク ライブラリ ( *.dll*) ファイル、またはコード モジュール ( *.netmodule*) ファイルを生成します。 詳細については、「[コンパイラ オプション](/cpp/build/reference/compiler-options)」、「[コマンド ラインから MSBuild を使用する](/cpp/build/msbuild-visual-cpp)」、「[コマンド ラインから Microsoft C++ ツールセットを使用する](/cpp/build/building-on-the-command-line)」を参照してください。

## <a name="parameters"></a>パラメーター

 次の一覧では、**CL** タスクのパラメーターを説明します。 タスク パラメーターの大部分とパラメーターのいくつかのセットは、コマンド ライン オプションに対応します。

- **AdditionalIncludeDirectories**

   省略可能な String[] 型のパラメーター。

   インクルード ファイルを検索するディレクトリのリストにディレクトリを追加します。

   詳細については、「[/I (追加インクルード ディレクトリ)](/cpp/build/reference/i-additional-include-directories)」を参照してください。

- **AdditionalOptions**

   省略可能な String 型のパラメーター。

   コマンド ライン オプションのリスト。 たとえば、"/\<option1> /\<option2> /\<option#>" のようになります。 他のタスク パラメーターでは表されないコマンド ライン オプションを指定する場合は、このパラメーターを使用します。

   詳細については、「[コンパイラ オプション](/cpp/build/reference/compiler-options)」を参照してください。

- **AdditionalUsingDirectories**

   省略可能な String[] 型のパラメーター。

   **#using** ディレクティブに渡されたファイル参照を解決するために、コンパイラによって検索されるディレクトリを指定します。

   詳細については、「[/AI (メタデータ ディレクトリの指定)](/cpp/build/reference/ai-specify-metadata-directories)」を参照してください。

- **AlwaysAppend**

   省略可能な String 型のパラメーター。

   コマンド ラインで常に出力される文字列。 既定値は " **/c**" です。

- **AssemblerListingLocation**

   アセンブリ コードを含むリスティング ファイルを作成します。

   詳細については、「[/FA、/Fa (リスティング ファイル)](/cpp/build/reference/fa-fa-listing-file)」の **/Fa** オプションに関する記述を参照してください。

- **AssemblerOutput**

   省略可能な String 型のパラメーター。

   アセンブリ コードを含むリスティング ファイルを作成します。

   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **NoListing** -  *\<none>*

  - **AssemblyCode** -  **/FA**

  - **AssemblyAndMachineCode** -  **/FAc**

  - **AssemblyAndSourceCode** -  **/FAs**

  - **All** -  **/FAcs**

    詳細については、「[/FA、/Fa (リスティング ファイル)](/cpp/build/reference/fa-fa-listing-file)」の **/FA**、 **/FAc**、 **/FAs**、および **/FAcs** の各オプションに関する記述を参照してください。

- **BasicRuntimeChecks**

   省略可能な String 型のパラメーター。

   [runtime_checks](/cpp/preprocessor/runtime-checks) プラグマと組み合わせて使用し、ランタイム エラー チェック機能を有効および無効にします。

   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **Default** -                           *\<none>*

  - **StackFrameRuntimeCheck** -  **/RTCs**

  - **UninitializedLocalUsageCheck** -  **/RTCu**

  - **EnableFastChecks** -                           **/RTC1**

    詳細については、「[/RTC (ランタイム エラー チェック)](/cpp/build/reference/rtc-run-time-error-checks)」を参照してください。

- **BrowseInformation**

   省略可能な Boolean 型のパラメーター。

   `true` の場合は、ブラウザー情報ファイルが作成されます。

   詳細については、「[/FR、/Fr (.sbr ファイルの作成)](/cpp/build/reference/fr-fr-create-dot-sbr-file)」の **/FR** オプションに関する記述を参照してください。

- **BrowseInformationFile**

   省略可能な String 型のパラメーター。

   ブラウザー情報ファイルのファイル名を指定します。

   詳細については、この表の **BrowseInformation** パラメーターを参照してください。また、「[/FR、/Fr (.sbr ファイルの作成)](/cpp/build/reference/fr-fr-create-dot-sbr-file)」も参照してください。

- **BufferSecurityCheck**

   省略可能な Boolean 型のパラメーター。

   `true` の場合は、リターン アドレス (バッファー サイズの制限を適用しないコードを利用するための一般的な方法) を上書きするいくつかのバッファー オーバーランが検出されます。

   詳細については、「[/GS (バッファーのセキュリティ チェック)](/cpp/build/reference/gs-buffer-security-check)」を参照してください。

- **BuildingInIDE**

   省略可能な Boolean 型のパラメーター。

   `true` の場合は、IDE によって **MSBuild** が呼び出されることを示します。 それ以外の場合は、コマンドラインで **MSBuild** が呼び出されます。

- **CallingConvention**

   省略可能な String 型のパラメーター。

   関数の引数をスタックにプッシュする順序、呼び出し元と呼び出し先のどちらの関数が呼び出しの最後にスタックから引数を削除するか、および個々の関数を識別するためにコンパイラが使用する名前装飾規約を決定する、呼び出し規則を指定します。

   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **Cdecl** -  **/Gd**

  - **FastCall** -                           **/Gr**

  - **StdCall** -                           **/Gz**

    詳細については、「[/Gd、/Gr、/Gv、/Gz (呼び出し規則)](/cpp/build/reference/gd-gr-gv-gz-calling-convention)」を参照してください。

- **CompileAs**

   省略可能な String 型のパラメーター。

   入力ファイルを C と C++ のどちらのソース ファイルとしてコンパイルするかを指定します。

   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **Default** -  *\<none>*

  - **CompileAsC** -  **/TC**

  - **CompileAsCpp** -  **/TP**

    詳細については、「[/Tc、/Tp、/TC、/TP (ソース ファイル タイプの指定)](/cpp/build/reference/tc-tp-tc-tp-specify-source-file-type)」を参照してください。

- **CompileAsManaged**

   省略可能な String 型のパラメーター。

   アプリケーションおよびコンポーネントで、共通言語ランタイム (CLR) の機能を使用できるようにします。

   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **false** -  *\<none>*

  - **true** -  **/clr**

  - **Pure** -  **/clr:pure**

  - **Safe** -  **/clr:safe**

  - **OldSyntax** -  **/clr:oldSyntax**

    詳細については、「[/clr (共通言語ランタイムのコンパイル)](/cpp/build/reference/clr-common-language-runtime-compilation)」を参照してください。

- **CreateHotpatchableImage**

   省略可能な Boolean 型のパラメーター。

   `true` の場合は、*ホット パッチ* 用のイメージを準備するようにコンパイラに指示します。 このパラメーターを使用することで、各関数の最初の命令が確実にホットパッチに必要な 2 バイトになります。

   詳細については、「[/hotpatch (ホットパッチ可能なイメージの作成)](/cpp/build/reference/hotpatch-create-hotpatchable-image)」を参照してください。

- **DebugInformationFormat**

   省略可能な String 型のパラメーター。

   プログラムに対して作成するデバッグ情報の種類を選択し、デバッグ情報をオブジェクト ( *.obj*) ファイルに保存するのかプログラム データベース (PDB) に保存するのかを選択します。

   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **OldStyle** -  **/Z7**

  - **ProgramDatabase** -  **/Zi**

  - **EditAndContinue** -  **/ZI**

    詳細については、「[/Z7、/Zi、/ZI (デバッグ情報の形式)](/cpp/build/reference/z7-zi-zi-debug-information-format)」を参照してください。

- **DisableLanguageExtensions**

   省略可能な Boolean 型のパラメーター。

   **true** の場合は、ANSI C や ANSI C++ と互換性のない言語コンストラクトに対してエラーを出力するようコンパイラに指示します。

   詳細については、「[/Za、/Ze (言語拡張機能の無効化)](/cpp/build/reference/za-ze-disable-language-extensions)」の **/Za** オプションに関する記述を参照してください。

- **DisableSpecificWarnings**

   省略可能な String[] 型のパラメーター。

   セミコロン区切りリストで指定されている警告番号を無効にします。

   詳細については、「[/w, /W0, /W1, /W2, /W3, /W4, /w1, /w2, /w3, /w4, /Wall, /wd, /we, /wo, /Wv, /WX (Warning Level)](/cpp/build/reference/compiler-option-warning-level)」(/w、/W0、/W1、/W2、/W3、/W4、/w1、/w2、/w3、/w4、/Wall、/wd、/we、/wo、/Wv、/WX (警告レベル)) の `/wd` オプションをご覧ください。

- **EnableEnhancedInstructionSet**

   省略可能な String 型のパラメーター。

   ストリーミング SIMD 拡張命令 (SSE) およびストリーミング SIMD 拡張命令 2 (SSE2) の命令を使用するコード生成のアーキテクチャを指定します。

   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **StreamingSIMDExtensions** -  **/arch:SSE**

  - **StreamingSIMDExtensions2** -  **/arch:SSE2**

    詳細については、「[/arch (x86)](/cpp/build/reference/arch-x86)」を参照してください。

- **EnableFiberSafeOptimizations**

   省略可能な Boolean 型のパラメーター。

   `true` の場合、静的スレッド ローカル ストレージを使用して割り当てられたデータ (つまり、`__declspec(thread)` を使用して割り当てられたデータ) に対して、ファイバー保護をサポートします。

   詳細については、「[/GT (スレッド ローカル ストレージを使用したファイバー保護のサポート)](/cpp/build/reference/gt-support-fiber-safe-thread-local-storage)」を参照してください。

- **EnablePREfast**

   省略可能な Boolean 型のパラメーター。

   `true` の場合、コード分析が有効になります。

   詳細については、「[/analyze (コード分析)](/cpp/build/reference/analyze-code-analysis)」を参照してください。

- **ErrorReporting**

   省略可能な String 型のパラメーター。

   内部コンパイル エラー (ICE) 情報を Microsoft に直接報告できます。 既定では、IDE ビルドの設定は **Prompt**、コマンド ライン ビルドの設定は **Queue** になります。

   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **None** -  **/errorReport:none**

  - **Prompt** -  **/errorReport:prompt**

  - **Queue** -  **/errorReport:queue**

  - **Send** -  **/errorReport:send**

    詳細については、「[/errorReport (内部コンパイラ エラーの報告)](/cpp/build/reference/errorreport-report-internal-compiler-errors)」を参照してください。

- **ExceptionHandling**

   省略可能な String 型のパラメーター。

   コンパイラで使用する例外処理のモデルを指定します。

   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **false** -  *\<none>*

  - **Async** -  **/EHa**

  - **Sync** -  **/EHsc**

  - **SyncCThrow** -  **/EHs**

    詳細については、「[/EH (例外処理モデル)](/cpp/build/reference/eh-exception-handling-model)」を参照してください。

- **ExpandAttributedSource**

   省略可能な Boolean 型のパラメーター。

   `true` の場合、ソース ファイルに拡張された属性を挿入したリスティング ファイルが作成されます。

   詳細については、「[/Fx (挿入されたコードのマージ)](/cpp/build/reference/fx-merge-injected-code)」を参照してください。

- **FavorSizeOrSpeed**

   省略可能な String 型のパラメーター。

   コードのサイズとコードの速度のどちらを優先するかを指定します。

   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **Neither** -  *\<none>*

  - **Size** -  **/Os**

  - **Speed** -  **/Ot**

    詳細については、「[/Os、/Ot (実行可能ファイルのサイズの優先、実行速度の優先)](/cpp/build/reference/os-ot-favor-small-code-favor-fast-code)」を参照してください。

- **FloatingPointExceptions**

   省略可能な Boolean 型のパラメーター。

   `true` の場合は、信頼性の高い浮動小数点例外モデルが有効になります。 例外は発生直後にスローされます。

   詳細については、「[/fp (浮動小数点の動作の指定)](/cpp/build/reference/fp-specify-floating-point-behavior)」の /**fp:except** オプションに関する記述を参照してください。

- **FloatingPointModel**

   省略可能な String 型のパラメーター。

   浮動小数点モデルを設定します。

   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **Precise** -  **/fp:precise**

  - **Strict** -  **/fp:strict**

  - **Fast** -  **/fp:fast**

    詳細については、「[/fp (浮動小数点の動作の指定)](/cpp/build/reference/fp-specify-floating-point-behavior)」を参照してください。

- **ForceConformanceInForLoopScope**

   省略可能な Boolean 型のパラメーター。

   `true` の場合は、Microsoft の拡張機能 ([/Ze](/cpp/build/reference/za-ze-disable-language-extensions)) を使用する [for](/cpp/cpp/for-statement-cpp) ループの標準 C++ 動作が実装されます。

   詳細については、「[/Zc:forScope (for ループのスコープの強制準拠)](/cpp/build/reference/zc-forscope-force-conformance-in-for-loop-scope)」を参照してください。

- **ForcedIncludeFiles**

   省略可能な `String[]` 型のパラメーターです。

   プリプロセッサで、指定された 1 つ以上のヘッダー ファイルが処理されます。

   詳細については、「[/FI (強制インクルード ファイルの名前の指定)](/cpp/build/reference/fi-name-forced-include-file)」を参照してください。

- **ForcedUsingFiles**

   省略可能な **String[]** 型のパラメーターです。

   プリプロセッサで、指定された 1 つ以上の **#using** ファイルが処理されます。

   詳細については、「[/FU (強制 #using ファイルの名前の指定)](/cpp/build/reference/fu-name-forced-hash-using-file)」を参照してください。

- **FunctionLevelLinking**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合は、コンパイラで、パッケージ化された関数の形式 (COMDATs) で個別の関数をパッケージ化できるようにします。

   詳細については、「[/Gy (関数レベルのリンクの有効化)](/cpp/build/reference/gy-enable-function-level-linking)」を参照してください。

- **GenerateXMLDocumentationFiles**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合は、コンパイラでソース コード ファイルのドキュメント コメントが処理され、ドキュメント コメントを含むソース コード ファイルごとに *.xdc* ファイルが作成されます。

   詳細については、「[/doc (ドキュメント コメントの処理) (C/C++)](/cpp/build/reference/doc-process-documentation-comments-c-cpp)」を参照してください。 この表の **XMLDocumentationFileName** パラメーターも参照してください。

- **IgnoreStandardIncludePath**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合は、コンパイラが、PATH および INCLUDE 環境変数で指定されているディレクトリ内のインクルード ファイルを検索しないようにします。

   詳細については、「[/X (標準インクルード パスの無視)](/cpp/build/reference/x-ignore-standard-include-paths)」を参照してください。

- **InlineFunctionExpansion**

   省略可能な **String** 型のパラメーターです。

   ビルドのインライン関数の拡張レベルを指定します。

   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **Default** -  *\<none>*

  - **Disabled** -  **/Ob0**

  - **OnlyExplicitInline** -  **/Ob1**

  - **AnySuitable** -  **/Ob2**

    詳細については、「[/Ob (関数のインライン展開)](/cpp/build/reference/ob-inline-function-expansion)」を参照してください。

- **IntrinsicFunctions**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合は、一部の関数呼び出しが組み込み関数に置き換えられます。それ以外の場合は、特殊な形式の関数が使用されます。これは、アプリケーションの実行時間を短縮するのに役立ちます。

   詳細については、「[/Oi (組み込み関数の生成)](/cpp/build/reference/oi-generate-intrinsic-functions)」を参照してください。

- **MinimalRebuild**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合は、最小リビルドが有効になります。これにより、(ヘッダー (.h) ファイルに格納されている) 変更された C++ クラス定義を含む C++ ソース ファイルを再コンパイルする必要があるかどうかが決定されます。

   詳細については、「[/Gm (簡易リビルドの有効化)](/cpp/build/reference/gm-enable-minimal-rebuild)」を参照してください。

- **MultiProcessorCompilation**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合は、複数のプロセッサを使用してコンパイルします。 このパラメーターでは、コンピューター上の有効なプロセッサごとにプロセスが作成されます。

   詳細については、「[/MP (複数のプロセスを使用したビルド)](/cpp/build/reference/mp-build-with-multiple-processes)」を参照してください。 この表にある **ProcessorNumber** パラメーターも参照してください。

- **ObjectFileName**

   省略可能な **String** 型のパラメーターです。

   既定値の代わりに使用する、オブジェクト (.obj) ファイルの名前またはディレクトリを指定します。

   詳細については、「[/Fo (オブジェクト ファイルの名前の指定)](/cpp/build/reference/fo-object-file-name)」を参照してください。

- **ObjectFiles**

   省略可能な **String[]** 型のパラメーターです。

   オブジェクト ファイルのリスト。

- **OmitDefaultLibName**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合は、オブジェクト ( *.obj*) ファイルの既定の C ランタイム ライブラリ名が省略されます。 既定では、コンパイラでライブラリ名が *.obj* ファイルにプッシュされ、リンカーに適切なライブラリが示されます。

   詳細については、「[/Zl (既定のライブラリ名の省略)](/cpp/build/reference/zl-omit-default-library-name)」を参照してください。

- **OmitFramePointers**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合は、呼び出し履歴にフレーム ポインターが作成されなくなります。

   詳細については、「[/Oy (フレーム ポインターの省略)](/cpp/build/reference/oy-frame-pointer-omission)」を参照してください。

- **OpenMPSupport**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合は、コンパイラで OpenMP 句とディレクティブが処理されます。

   詳細については、「[/openmp (OpenMP 2.0 サポートの有効化)](/cpp/build/reference/openmp-enable-openmp-2-0-support)」を参照してください。

- **Optimization**

   省略可能な **String** 型のパラメーターです。

   速度とサイズに関するさまざまなコードの最適化を指定します。

   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **Disabled** -  **/Od**

  - **MinSpace** -  **/O1**

  - **MaxSpeed** -  **/O2**

  - **Full** -  **/Ox**

    詳細については、「[/O オプション (コードの最適化)](/cpp/build/reference/o-options-optimize-code)」を参照してください。

- **PrecompiledHeader**

   省略可能な **String** 型のパラメーターです。

   ビルド時にプリコンパイル済みヘッダー ( *.pch*) ファイルを作成または使用します。

   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **NotUsing** -  *\<none>*

  - **Create** -  **/Yc**

  - **Use** -  **/Yu**

    詳細については、「[/Yc (プリコンパイル済みヘッダー ファイルの作成)](/cpp/build/reference/yc-create-precompiled-header-file)」と「[/Yu (プリコンパイル済みヘッダー ファイルの使用)](/cpp/build/reference/yu-use-precompiled-header-file)」を参照してください。 この表にある **PrecompiledHeaderFile** および **PrecompiledHeaderOutputFile** パラメーターも参照してください。

- **PrecompiledHeaderFile**

   省略可能な **String** 型のパラメーターです。

   作成または使用するプリコンパイル済みヘッダー ファイルの名前を指定します。

   詳細については、「[/Yc (プリコンパイル済みヘッダー ファイルの作成)](/cpp/build/reference/yc-create-precompiled-header-file)」と「[/Yu (プリコンパイル済みヘッダー ファイルの使用)](/cpp/build/reference/yu-use-precompiled-header-file)」を参照してください。

- **PrecompiledHeaderOutputFile**

   省略可能な **String** 型のパラメーターです。

   既定のパス名を使用する代わりにプリコンパイル済みヘッダーのパス名を指定します。

   詳細については、「[/Fp (.pch ファイルの名前の指定)](/cpp/build/reference/fp-name-dot-pch-file)」を参照してください。

- **PreprocessKeepComments**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合は、プリプロセス時にコメントが保持されます。

   詳細については、「[/C (プリプロセス時のコメントの保持)](/cpp/build/reference/c-preserve-comments-during-preprocessing)」を参照してください。

- **PreprocessorDefinitions**

   省略可能な `String[]` 型のパラメーターです。

   ソース ファイルの前処理シンボルを定義します。

   詳細については、「[/D (プリプロセッサ定義)](/cpp/build/reference/d-preprocessor-definitions)」を参照してください。

- **PreprocessOutput**

   省略可能な `ITaskItem[]` 型のパラメーターです。

   タスクで使用および生成できるプリプロセッサ出力項目の配列を定義します。

- **PreprocessOutputPath**

   省略可能な `String` 型のパラメーターです。

   **PreprocessToFile** パラメーターで前処理済みの出力を書き込む出力ファイルの名前を指定します。

   詳細については、「[/Fi (出力ファイル名のプリプロセス)](/cpp/build/reference/fi-preprocess-output-file-name)」を参照してください。

- **PreprocessSuppressLineNumbers**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合、C および C++ ソース ファイルが前処理され、前処理されたファイルが標準出力デバイスにコピーされます。

   詳細については、「[/EP (#line ディレクティブを挿入しない stdout へのプリプロセス)](/cpp/build/reference/ep-preprocess-to-stdout-without-hash-line-directives)」を参照してください。

- **PreprocessToFile**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合、C および C++ ソース ファイルが前処理され、前処理済みの出力がファイルに書き込まれます。

   詳細については、「[/P (プリプロセス出力のファイルへの書き込み)](/cpp/build/reference/p-preprocess-to-a-file)」を参照してください。

- **ProcessorNumber**

   省略可能な `Integer` 型のパラメーターです。

   マルチプロセッサ コンパイル時に使用するプロセッサの最大数を指定します。 このパラメーターは、**MultiProcessorCompilation** パラメーターと組み合わせて使用します。

- **ProgramDataBaseFileName**

   省略可能な `String` 型のパラメーターです。

   プログラム データベース (PDB) ファイルの名前を指定します。

   詳細については、「[/Fd (プログラム データベース ファイル名)](/cpp/build/reference/fd-program-database-file-name)」を参照してください。

- **RuntimeLibrary**

   省略可能な `String` 型のパラメーターです。

   マルチスレッド モジュールが DLL であるかどうかを指定し、ランタイム ライブラリのリテール バージョンまたはデバッグ バージョンを選択します。

   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **MultiThreaded** -  **/MT**

  - **MultiThreadedDebug** -  **/MTd**

  - **MultiThreadedDLL** -  **/MD**

  - **MultiThreadedDebugDLL** -  **/MDd**

    詳細については、「[/MD、/MT、/LD (ランタイム ライブラリの使用)](/cpp/build/reference/md-mt-ld-use-run-time-library)」を参照してください。

- **RuntimeTypeInfo**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合、実行時に C++ のオブジェクト型をチェックするコードが追加されます (ランタイム型情報)。

   詳細については、「[/GR (ランタイム型情報の有効化)](/cpp/build/reference/gr-enable-run-time-type-information)」を参照してください。

- **ShowIncludes**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合、コンパイラでインクルード ファイルの一覧が出力されます。

   詳細については、「[/showIncludes (インクルード ファイル一覧)](/cpp/build/reference/showincludes-list-include-files)」を参照してください。

- **SmallerTypeCheck**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合、値がより小さいデータ型に割り当てられ、データ損失が発生したときに、ランタイム エラーが報告されます。

   詳細については、「[/RTC (ランタイム エラー チェック)](/cpp/build/reference/rtc-run-time-error-checks)」の **/RTCc** オプションに関する記述を参照してください。

- **Sources**

   必須の `ITaskItem[]` 型のパラメーターです。

   スペースで区切られたソース ファイルのリストを指定します。

- **StringPooling**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合、コンパイラで、プログラム イメージに同一文字列の 1 つのコピーを作成できます。

   詳細については、「[/GF (同一文字列の削除)](/cpp/build/reference/gf-eliminate-duplicate-strings)」を参照してください。

- **StructMemberAlignment**

   省略可能な `String` 型のパラメーターです。

   構造体のすべてのメンバーのバイト配置を指定します。

   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **既定** -  **/Zp1**

  - **1Byte** -  **/Zp1**

  - **2Bytes** -  **/Zp2**

  - **4Bytes** -  **/Zp4**

  - **8Bytes** -  **/Zp8**

  - **16Bytes** -  **/Zp16**

    詳細については、「[/Zp (構造体メンバーの配置)](/cpp/build/reference/zp-struct-member-alignment)」を参照してください。

- **SuppressStartupBanner**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合、タスクの開始時に著作権およびバージョン番号のメッセージが表示されないようにします。

   詳細については、「[/nologo (著作権情報の非表示) (C/C++)](/cpp/build/reference/nologo-suppress-startup-banner-c-cpp)」を参照してください。

- **TrackerLogDirectory**

   省略可能な `String` 型のパラメーターです。

   このタスクの追跡ログの格納先となる中間ディレクトリを指定します。

   詳細については、この表にある **TLogReadFiles** および **TLogWriteFiles** パラメーターを参照してください。

- **TreatSpecificWarningsAsErrors**

   省略可能な **String[]** 型のパラメーターです。

   指定したコンパイラ警告の一覧をエラーとして扱います。

   詳細については、「[/w, /W0, /W1, /W2, /W3, /W4, /w1, /w2, /w3, /w4, /Wall, /wd, /we, /wo, /Wv, /WX (Warning Level)](/cpp/build/reference/compiler-option-warning-level)」(/w、/W0、/W1、/W2、/W3、/W4、/w1、/w2、/w3、/w4、/Wall、/wd、/we、/wo、/Wv、/WX (警告レベル)) の **/we**`n` オプションをご覧ください。

- **TreatWarningAsError**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合、コンパイラが生成する警告がすべてエラーとして扱われます。

   詳細については、「[/w, /W0, /W1, /W2, /W3, /W4, /w1, /w2, /w3, /w4, /Wall, /wd, /we, /wo, /Wv, /WX (Warning Level)](/cpp/build/reference/compiler-option-warning-level)」(/w、/W0、/W1、/W2、/W3、/W4、/w1、/w2、/w3、/w4、/Wall、/wd、/we、/wo、/Wv、/WX (警告レベル)) の **/WX** オプションをご覧ください。

- **TreatWChar_tAsBuiltInType**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合、`wchar_t` 型はネイティブ型として扱われます。

   詳細については、「[/Zc:wchar_t (wchar_t をネイティブ型として認識)](/cpp/build/reference/zc-wchar-t-wchar-t-is-native-type)」を参照してください。

- **UndefineAllPreprocessorDefinitions**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合、コンパイラで定義されている Microsoft 固有のシンボルの定義が解除されます。

   詳細については、「[/U、/u (定義済みマクロ シンボルの未定義化)](/cpp/build/reference/u-u-undefine-symbols)」の **/u** オプションに関する記述を参照してください。

- **UndefinePreprocessorDefinitions**

   省略可能な `String[]` 型のパラメーターです。

   定義を解除する 1 つ以上のプリプロセッサ シンボルの一覧を指定します。

   詳細については、「[/U、/u (定義済みマクロ シンボルの未定義化)](/cpp/build/reference/u-u-undefine-symbols)」の **/U** オプションに関する記述を参照してください。

- **UseFullPaths**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合、診断時にコンパイラに渡されるソース コード ファイルの完全パスが表示されます。

   詳細については、「[/FC (診断時のソース コード ファイルの完全パス)](/cpp/build/reference/fc-full-path-of-source-code-file-in-diagnostics)」を参照してください。

- **UseUnicodeForAssemblerListing**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合、出力ファイルが UTF-8 形式で作成されます。

   詳細については、「[/FA、/Fa (リスティング ファイル)](/cpp/build/reference/fa-fa-listing-file)」の **/FAu** オプションに関する記述を参照してください。

- **WarningLevel**

   省略可能な `String` 型のパラメーターです。

   コンパイラによって生成される警告の最高レベルを指定します。

   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。

  - **TurnOffAllWarnings** -  **/W0**

  - **Level1** -  **/W1**

  - **Level2** -  **/W2**

  - **Level3** -  **/W3**

  - **Level4** -  **/W4**

  - **EnableAllWarnings** -  **/Wall**

    詳細については、「[/w, /W0, /W1, /W2, /W3, /W4, /w1, /w2, /w3, /w4, /Wall, /wd, /we, /wo, /Wv, /WX (Warning Level)](/cpp/build/reference/compiler-option-warning-level)」(/w、/W0、/W1、/W2、/W3、/W4、/w1、/w2、/w3、/w4、/Wall、/wd、/we、/wo、/Wv、/WX (警告レベル)) の **/W**_n_ オプションをご覧ください。

- **WholeProgramOptimization**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合、プログラム全体の最適化が有効になります。

   詳細については、「[/GL (プログラム全体の最適化)](/cpp/build/reference/gl-whole-program-optimization)」を参照してください。

- **XMLDocumentationFileName**

   省略可能な `String` 型のパラメーターです。

   生成される XML ドキュメント ファイルの名前を指定します。 このパラメーターには、ファイルまたはディレクトリ名を指定できます。

   詳細については、「[/doc (ドキュメント コメントの処理) (C/C++)](/cpp/build/reference/doc-process-documentation-comments-c-cpp)」の `name` 引数に関する記述を参照してください。 この表の **GenerateXMLDocumentationFiles** パラメーターも参照してください。

- **MinimalRebuildFromTracking**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合、追跡対象のインクリメンタル ビルドが実行され、`false` の場合は、リビルドが実行されます。

- **TLogReadFiles**

   省略可能な `ITaskItem[]` 型のパラメーターです。

   *ファイルの読み取り追跡ログ* を表す項目の配列を指定します。

   ファイルの読み取り追跡ログ ( *.tlog*) には、タスクによって読み取られ、プロジェクト ビルド システムによってインクリメンタル ビルドをサポートするために使用される入力ファイルの名前が含まれています。 詳細については、この表の **TrackerLogDirectory** および **TrackFileAccess** パラメーターを参照してください。

- **TLogWriteFiles**

   省略可能な `ITaskItem[]` 型のパラメーターです。

   *ファイルの書き込み追跡ログ* を表す項目の配列を指定します。

   ファイルの書き込み追跡ログ ( *.tlog*) には、タスクによって読み取られ、プロジェクト ビルド システムによってインクリメンタル ビルドをサポートするために使用される出力ファイルの名前が含まれています。 詳細については、この表の **TrackerLogDirectory** および **TrackFileAccess** パラメーターを参照してください。

- **TrackFileAccess**

   省略可能な `Boolean` 型のパラメーターです。

   `true` の場合、ファイル アクセス パターンが追跡されます。

   詳細については、この表にある **TLogReadFiles** および **TLogWriteFiles** パラメーターを参照してください。

## <a name="see-also"></a>関連項目

- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
