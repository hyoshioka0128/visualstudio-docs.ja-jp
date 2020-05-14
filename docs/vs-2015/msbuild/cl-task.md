---
title: CL タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
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
- MSBuild (Visual C++), CL task
- CL task (MSBuild (Visual C++))
ms.assetid: 651ba971-b755-4f03-a549-4816beb3cc0d
caps.latest.revision: 21
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8307bc2c9efcbbab531754cd2d49fa18b04cc48a
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65698637"
---
# <a name="cl-task"></a>CL タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual C++ コンパイラ ツール (cl.exe) をラップします。 コンパイラは、実行可能ファイル (.exe)、ダイナミック リンク ライブラリ (.dll) ファイル、またはコード モジュール (.netmodule) ファイルを生成します。 詳細については、「[コンパイラ オプション](https://msdn.microsoft.com/library/ed3376c8-bef4-4c9a-80e9-3b5da232644c)」を参照してください。  
  
## <a name="parameters"></a>パラメーター  
 **CL** タスクのパラメーターの説明を次の表に示します。 タスク パラメーターの大部分とパラメーターのいくつかのセットは、コマンド ライン オプションに対応します。  
  
- **AdditionalIncludeDirectories**  
  
   省略可能な String[] 型のパラメーター。  
  
   インクルード ファイルを検索するディレクトリのリストにディレクトリを追加します。  
  
   詳細については、「[/I (追加インクルード ディレクトリ)](https://msdn.microsoft.com/library/3e9add2a-5ed8-4d15-ad79-5b411e313a49)」を参照してください。  
  
- **AdditionalOptions**  
  
   省略可能な String 型のパラメーター。  
  
   コマンド ライン オプションのリスト。 "/*option1* /*option2* /*option#*" のようになります。 他のタスク パラメーターでは表されないコマンド ライン オプションを指定する場合は、このパラメーターを使用します。  
  
   詳細については、「[コンパイラ オプション](https://msdn.microsoft.com/library/ed3376c8-bef4-4c9a-80e9-3b5da232644c)」を参照してください。  
  
- **AdditionalUsingDirectories** 省略可能な String[] 型のパラメーター。  
  
   **#using** ディレクティブに渡されたファイル参照を解決するために、コンパイラによって検索されるディレクトリを指定します。  
  
   詳細については、「[/AI (メタデータ ディレクトリの指定)](https://msdn.microsoft.com/library/fb9c1846-504c-4a3b-bb39-c8696de32f6f)」を参照してください。  
  
- **AlwaysAppend**  
  
   省略可能な String 型のパラメーター。  
  
   コマンド ラインで常に出力される文字列。 既定値は "**/c**" です。  
  
- **AssemblerListingLocation**  
  
   アセンブリ コードを含むリスティング ファイルを作成します。  
  
   詳細については、「[/FA、/Fa (リスティング ファイル)](https://msdn.microsoft.com/library/c7507d0e-c69d-44f9-b8e2-d2c398697402)」の **/Fa** オプションに関する記述を参照してください。  
  
- **AssemblerOutput**  
  
   省略可能な String 型のパラメーター。  
  
   アセンブリ コードを含むリスティング ファイルを作成します。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **NoListing** - *\<なし>*  
  
  - **AssemblyCode** - **/FA**  
  
  - **AssemblyAndMachineCode** - **/FAc**  
  
  - **AssemblyAndSourceCode** - **/FAs**  
  
  - **All** - **/FAcs**  
  
    詳細については、「[/FA、/Fa (リスティング ファイル)](https://msdn.microsoft.com/library/c7507d0e-c69d-44f9-b8e2-d2c398697402)」の **/FA**、**/FAc**、**/FAs**、および **/FAcs** の各オプションに関する記述を参照してください。  
  
- **BasicRuntimeChecks**  
  
   省略可能な String 型のパラメーター。  
  
   [runtime_checks](https://msdn.microsoft.com/library/ae50b43f-f88d-47ad-a2db-3389e9e7df5b) プラグマと組み合わせて使用し、ランタイム エラー チェック機能を有効および無効にします。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **Default** -                          *\<none>*  
  
  - **StackFrameRuntimeCheck** - **/RTCs**  
  
  - **UninitializedLocalUsageCheck** - **/RTCu**  
  
  - **EnableFastChecks** -                          **/RTC1**  
  
    詳細については、「[/RTC (ランタイム エラー チェック)](https://msdn.microsoft.com/library/9702c558-412c-4004-acd5-80761f589368)」を参照してください。  
  
- **BrowseInformation**  
  
   省略可能な Boolean 型のパラメーター。  
  
   `true` の場合は、ブラウザー情報ファイルが作成されます。  
  
   詳細については、「[/FR、/Fr (.sbr ファイルの作成)](https://msdn.microsoft.com/library/3fd8f88b-3924-4feb-9393-287036a28896)」の **/FR** オプションに関する記述を参照してください。  
  
- **BrowseInformationFile**  
  
   省略可能な String 型のパラメーター。  
  
   ブラウザー情報ファイルのファイル名を指定します。  
  
   詳細については、この表の **BrowseInformation** パラメーターを参照してください。また、「[/FR、/Fr (.sbr ファイルの作成)](https://msdn.microsoft.com/library/3fd8f88b-3924-4feb-9393-287036a28896)」も参照してください。  
  
- **BufferSecurityCheck**  
  
   省略可能な Boolean 型のパラメーター。  
  
   `true` の場合は、リターン アドレス (バッファー サイズの制限を適用しないコードを利用するための一般的な方法) を上書きするいくつかのバッファー オーバーランが検出されます。  
  
   詳細については、「[/GS (バッファーのセキュリティ チェック)](https://msdn.microsoft.com/library/8d8a5ea1-cd5e-42e1-bc36-66e1cd7e731e)」を参照してください。  
  
- **BuildingInIDE**  
  
   省略可能な Boolean 型のパラメーター。  
  
   `true` の場合は、IDE によって **MSBuild** が呼び出されることを示します。 それ以外の場合は、コマンドラインで **MSBuild** が呼び出されます。  
  
- **CallingConvention**  
  
   省略可能な String 型のパラメーター。  
  
   関数の引数をスタックにプッシュする順序、呼び出し元と呼び出し先のどちらの関数が呼び出しの最後にスタックから引数を削除するか、および個々の関数を識別するためにコンパイラが使用する名前装飾規約を決定する、呼び出し規則を指定します。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **Cdecl** - **/Gd**  
  
  - **FastCall** -                          **/Gr**  
  
  - **StdCall** -                          **/Gz**  
  
    詳細については、「[/Gd、/Gr、/Gv、/Gz (呼び出し規則)](https://msdn.microsoft.com/library/fd3110cb-2d77-49f2-99cf-a03f9ead00a3)」を参照してください。  
  
- **CompileAs**  
  
   省略可能な String 型のパラメーター。  
  
   入力ファイルを C と C++ のどちらのソース ファイルとしてコンパイルするかを指定します。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **Default** - *\<none>*  
  
  - **CompileAsC** - **/TC**  
  
  - **CompileAsCpp** - **/TP**  
  
    詳細については、「[/Tc、/Tp、/TC、/TP (ソース ファイル タイプの指定)](https://msdn.microsoft.com/library/7d9d0a65-338b-427c-8b48-fff30e2f9d2b)」を参照してください。  
  
- **CompileAsManaged**  
  
   省略可能な String 型のパラメーター。  
  
   アプリケーションおよびコンポーネントで、共通言語ランタイム (CLR) の機能を使用できるようにします。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **false** - *\<なし>*  
  
  - **true** - **/clr**  
  
  - **Pure** - **/clr:pure**  
  
  - **Safe** - **/clr:safe**  
  
  - **OldSyntax** - **/clr:oldSyntax**  
  
    詳細については、「[/clr (共通言語ランタイムのコンパイル)](https://msdn.microsoft.com/library/fec5a8c0-40ec-484c-a213-8dec918c1d6c)」を参照してください。  
  
- **CreateHotpatchableImage**  
  
   省略可能な Boolean 型のパラメーター。  
  
   `true` の場合は、*ホット パッチ*用のイメージを準備するようにコンパイラに指示します。 このパラメーターを使用することで、各関数の最初の命令が確実にホットパッチに必要な 2 バイトになります。  
  
   詳細については、「[/hotpatch (ホットパッチ可能なイメージの作成)](https://msdn.microsoft.com/library/aad539b6-c053-4c78-8682-853d98327798)」を参照してください。  
  
- **DebugInformationFormat**  
  
   省略可能な String 型のパラメーター。  
  
   プログラムに対して作成するデバッグ情報の種類を選択し、デバッグ情報をオブジェクト (.obj) ファイルに保存するのかプログラム データベース (PDB) に保存するのかを選択します。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **OldStyle** - **/Z7**  
  
  - **ProgramDatabase** - **/Zi**  
  
  - **EditAndContinue** - **/ZI**  
  
    詳細については、「[/Z7、/Zi、/ZI (デバッグ情報の形式)](https://msdn.microsoft.com/library/ce9fa7e1-0c9b-47e3-98ea-26d1a16257c8)」を参照してください。  
  
- **DisableLanguageExtensions**  
  
   省略可能な Boolean 型のパラメーター。  
  
   **true** の場合は、ANSI C や ANSI C++ と互換性のない言語コンストラクトに対してエラーを出力するようコンパイラに指示します。  
  
   詳細については、「[/Za、/Ze (言語拡張機能の無効化)](https://msdn.microsoft.com/library/65e49258-7161-4289-a176-7c5c0656b1a2)」の **/Za** オプションに関する記述を参照してください。  
  
- **DisableSpecificWarnings**  
  
   省略可能な String[] 型のパラメーター。  
  
   セミコロン区切りリストで指定されている警告番号を無効にします。  
  
   詳細については、「[/w、/Wn、/WX、/Wall、/wln、/wdn、/wen、/won (警告レベル)](https://msdn.microsoft.com/library/d6bc7bf5-c754-4879-909c-8e3a67e2629f)」の `/wd` オプションに関する記述を参照してください。  
  
- **EnableEnhancedInstructionSet**  
  
   省略可能な String 型のパラメーター。  
  
   ストリーミング SIMD 拡張命令 (SSE) およびストリーミング SIMD 拡張命令 2 (SSE2) の命令を使用するコード生成のアーキテクチャを指定します。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **StreamingSIMDExtensions** - **/arch:SSE**  
  
  - **StreamingSIMDExtensions2** - **/arch:SSE2**  
  
    詳細については、「[/arch (x86)](https://msdn.microsoft.com/library/9dd5a75d-06e4-4674-aade-33228486078d)」を参照してください。  
  
- **EnableFiberSafeOptimizations**  
  
   省略可能な Boolean 型のパラメーター。  
  
   `true` の場合、静的スレッド ローカル ストレージを使用して割り当てられたデータ (つまり、`__declspec(thread)` を使用して割り当てられたデータ) に対して、ファイバー保護をサポートします。  
  
   詳細については、「[/GT (スレッド ローカル ストレージを使用したファイバー保護のサポート)](https://msdn.microsoft.com/library/071fec79-c701-432b-9970-457344133159)」を参照してください。  
  
- **EnablePREfast**  
  
   省略可能な Boolean 型のパラメーター。  
  
   `true` の場合、コード分析が有効になります。  
  
   詳細については、「[/analyze (コード分析)](https://msdn.microsoft.com/library/81da536a-e030-4bd4-be18-383927597d08)」を参照してください。  
  
- **ErrorReporting**  
  
   省略可能な String 型のパラメーター。  
  
   内部コンパイル エラー (ICE) 情報を Microsoft に直接報告できます。 既定では、IDE ビルドの設定は **Prompt**、コマンド ライン ビルドの設定は **Queue** になります。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **None** - **/errorReport:none**  
  
  - **Prompt** - **/errorReport:prompt**  
  
  - **Queue** - **/errorReport:queue**  
  
  - **Send** - **/errorReport:send**  
  
    詳細については、「[/errorReport (内部コンパイラ エラーの報告)](https://msdn.microsoft.com/library/819828f8-b0a5-412c-9c57-bf822f17e667)」を参照してください。  
  
- **ExceptionHandling**  
  
   省略可能な String 型のパラメーター。  
  
   コンパイラで使用する例外処理のモデルを指定します。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **false** - *\<なし>*  
  
  - **Async** - **/EHa**  
  
  - **Sync** - **/EHsc**  
  
  - **SyncCThrow** - **/EHs**  
  
    詳細については、「[/EH (例外処理モデル)](https://msdn.microsoft.com/library/754b916f-d206-4472-b55a-b6f1b0f2cb4d)」を参照してください。  
  
- **ExpandAttributedSource**  
  
   省略可能な Boolean 型のパラメーター。  
  
   `true` の場合、ソース ファイルに拡張された属性を挿入したリスティング ファイルが作成されます。  
  
   詳細については、「[/Fx (挿入されたコードのマージ)](https://msdn.microsoft.com/library/14f0e301-3bab-45a3-bbdf-e7ce66f20560)」を参照してください。  
  
- **FavorSizeOrSpeed**  
  
   省略可能な String 型のパラメーター。  
  
   コードのサイズとコードの速度のどちらを優先するかを指定します。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **Neither** - *\<なし>*  
  
  - **Size** - **/Os**  
  
  - **Speed** - **/Ot**  
  
    詳細については、「[/Os、/Ot (実行可能ファイルのサイズの優先、実行速度の優先)](https://msdn.microsoft.com/library/9a340806-fa15-4308-892c-355d83cac0f2)」を参照してください。  
  
- **FloatingPointExceptions**  
  
   省略可能な Boolean 型のパラメーター。  
  
   `true` の場合は、信頼性の高い浮動小数点例外モデルが有効になります。 例外は発生直後にスローされます。  
  
   詳細については、「[/fp (浮動小数点の動作の指定)](https://msdn.microsoft.com/library/10469d6b-e68b-4268-8075-d073f4f5d57e)」の /**fp:except** オプションに関する記述を参照してください。  
  
- **FloatingPointModel**  
  
   省略可能な String 型のパラメーター。  
  
   浮動小数点モデルを設定します。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **Precise** - **/fp:precise**  
  
  - **Strict** - **/fp:strict**  
  
  - **Fast** - **/fp:fast**  
  
    詳細については、「[/fp (浮動小数点の動作の指定)](https://msdn.microsoft.com/library/10469d6b-e68b-4268-8075-d073f4f5d57e)」を参照してください。  
  
- **ForceConformanceInForLoopScope**  
  
   省略可能な Boolean 型のパラメーター。  
  
   `true` の場合は、Microsoft の拡張機能 ([/Ze](https://msdn.microsoft.com/library/65e49258-7161-4289-a176-7c5c0656b1a2)) を使用する [for](https://msdn.microsoft.com/library/6c7d01b3-c4c1-4c6a-aa58-e2d198f33d4a) ループの標準 C++ 動作が実装されます。  
  
   詳細については、「[/Zc:forScope (for ループのスコープの強制準拠)](https://msdn.microsoft.com/library/3031f02d-3b14-4ad0-869e-22b0110c3aed)」を参照してください。  
  
- **ForcedIncludeFiles**  
  
   省略可能な `String[]` 型のパラメーターです。  
  
   プリプロセッサで、指定された 1 つ以上のヘッダー ファイルが処理されます。  
  
   詳細については、「[/FI (強制インクルード ファイルの名前の指定)](https://msdn.microsoft.com/library/07e79577-8152-4df9-a64c-aae08c603397)」を参照してください。  
  
- **ForcedUsingFiles**  
  
   省略可能な **String[]** 型のパラメーターです。  
  
   プリプロセッサで、指定された 1 つ以上の **#using** ファイルが処理されます。  
  
   詳細については、「[/FU (強制 #using ファイルの名前の指定)](https://msdn.microsoft.com/library/698f8603-457f-435a-baff-5ac9243d6ca1)」を参照してください。  
  
- **FunctionLevelLinking**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合は、コンパイラで、パッケージ化された関数の形式 (COMDATs) で個別の関数をパッケージ化できるようにします。  
  
   詳細については、「[/Gy (関数レベルのリンクの有効化)](https://msdn.microsoft.com/library/0d3cf14c-ed7d-4ad3-b4b6-104e56f61046)」を参照してください。  
  
- **GenerateXMLDocumentationFiles**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合は、コンパイラでソース コード ファイルのドキュメント コメントが処理され、ドキュメント コメントを含むソース コード ファイルごとに .xdc ファイルが作成されます。  
  
   詳細については、「[/doc (ドキュメント コメントの処理) (C/C++)](https://msdn.microsoft.com/library/b54f7e2c-f28f-4f46-9ed6-0db09be2cc63)」を参照してください。 この表の **XMLDocumentationFileName** パラメーターも参照してください。  
  
- **IgnoreStandardIncludePath**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合は、コンパイラが、PATH および INCLUDE 環境変数で指定されているディレクトリ内のインクルード ファイルを検索しないようにします。  
  
   詳細については、「[/X (標準インクルード パスの無視)](https://msdn.microsoft.com/library/16bdf2cc-c8dc-46e4-bdcc-f3caeba5e1ef)」を参照してください。  
  
- **InlineFunctionExpansion**  
  
   省略可能な **String** 型のパラメーターです。  
  
   ビルドのインライン関数の拡張レベルを指定します。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **Default** - *\<none>*  
  
  - **Disabled** - **/Ob0**  
  
  - **OnlyExplicitInline** - **/Ob1**  
  
  - **AnySuitable** - **/Ob2**  
  
    詳細については、「[/Ob (関数のインライン展開)](https://msdn.microsoft.com/library/f134e6df-e939-4980-a01d-47425dbc562a)」を参照してください。  
  
- **IntrinsicFunctions**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合は、一部の関数呼び出しが組み込み関数に置き換えられます。それ以外の場合は、特殊な形式の関数が使用されます。これは、アプリケーションの実行時間を短縮するのに役立ちます。  
  
   詳細については、「[/Oi (組み込み関数の生成)](https://msdn.microsoft.com/library/fa4a3bf6-0ed8-481b-91c0-add7636132b4)」を参照してください。  
  
- **MinimalRebuild**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合は、最小リビルドが有効になります。これにより、(ヘッダー (.h) ファイルに格納されている) 変更された C++ クラス定義を含む C++ ソース ファイルを再コンパイルする必要があるかどうかが決定されます。  
  
   詳細については、「[/Gm (簡易リビルドの有効化)](https://msdn.microsoft.com/library/d8869ce0-d2ea-40eb-8dae-6d2cdb61dd59)」を参照してください。  
  
- **MultiProcessorCompilation**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合は、複数のプロセッサを使用してコンパイルします。 このパラメーターでは、コンピューター上の有効なプロセッサごとにプロセスが作成されます。  
  
   詳細については、「[/MP (複数のプロセスを使用したビルド)](https://msdn.microsoft.com/library/a932b14a-74fe-4b45-84e4-6bf53f0f5e07)」を参照してください。 この表にある **ProcessorNumber** パラメーターも参照してください。  
  
- **ObjectFileName**  
  
   省略可能な **String** 型のパラメーターです。  
  
   既定値の代わりに使用する、オブジェクト (.obj) ファイルの名前またはディレクトリを指定します。  
  
   詳細については、「[/Fo (オブジェクト ファイルの名前の指定)](https://msdn.microsoft.com/library/0e6d593e-4e7f-4990-9e6e-92e1dcbcf6e6)」を参照してください。  
  
- **ObjectFiles**  
  
   省略可能な **String[]** 型のパラメーターです。  
  
   オブジェクト ファイルのリスト。  
  
- **OmitDefaultLibName**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合は、オブジェクト (.obj) ファイルの既定の C ランタイム ライブラリ名が省略されます。 既定では、コンパイラでライブラリ名が .obj ファイルにプッシュされ、リンカーに適切なライブラリが示されます。  
  
   詳細については、「[/Zl (既定のライブラリ名の省略)](https://msdn.microsoft.com/library/b27d39d0-44d6-498c-84ae-27c1326fee59)」を参照してください。  
  
- **OmitFramePointers**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合は、呼び出し履歴にフレーム ポインターが作成されなくなります。  
  
   詳細については、「[/Oy (フレーム ポインターの省略)](https://msdn.microsoft.com/library/c451da86-5297-4c5a-92bc-561d41379853)」を参照してください。  
  
- **OpenMPSupport**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合は、コンパイラで OpenMP 句とディレクティブが処理されます。  
  
   詳細については、「[/openmp (OpenMP 2.0 サポートの有効化)](https://msdn.microsoft.com/library/9082b175-18d3-4378-86a7-c0eb95664e13)」を参照してください。  
  
- **Optimization**  
  
   省略可能な **String** 型のパラメーターです。  
  
   速度とサイズに関するさまざまなコードの最適化を指定します。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **Disabled** - **/Od**  
  
  - **MinSpace** - **/O1**  
  
  - **MaxSpeed** - **/O2**  
  
  - **Full** - **/Ox**  
  
    詳細については、「[/O オプション (コードの最適化)](https://msdn.microsoft.com/library/77997af9-5555-4b3d-aa57-6615b27d4d5d)」を参照してください。  
  
- **PrecompiledHeader**  
  
   省略可能な **String** 型のパラメーターです。  
  
   ビルド時にプリコンパイル済みヘッダー (.pch) ファイルを作成または使用します。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **NotUsing** - *\<なし>*  
  
  - **Create** - **/Yc**  
  
  - **Use** - **/Yu**  
  
    詳細については、「[/Yc (プリコンパイル済みヘッダー ファイルの作成)](https://msdn.microsoft.com/library/47c2e555-b4f5-46e6-906e-ab5cf21f0678)」と「[/Yu (プリコンパイル済みヘッダー ファイルの使用)](https://msdn.microsoft.com/library/24f1bd0e-b624-4296-a17e-d4b53e374e1f)」を参照してください。 この表にある **PrecompiledHeaderFile** および **PrecompiledHeaderOutputFile** パラメーターも参照してください。  
  
- **PrecompiledHeaderFile**  
  
   省略可能な **String** 型のパラメーターです。  
  
   作成または使用するプリコンパイル済みヘッダー ファイルの名前を指定します。  
  
   詳細については、「[/Yc (プリコンパイル済みヘッダー ファイルの作成)](https://msdn.microsoft.com/library/47c2e555-b4f5-46e6-906e-ab5cf21f0678)」と「[/Yu (プリコンパイル済みヘッダー ファイルの使用)](https://msdn.microsoft.com/library/24f1bd0e-b624-4296-a17e-d4b53e374e1f)」を参照してください。  
  
- **PrecompiledHeaderOutputFile**  
  
   省略可能な **String** 型のパラメーターです。  
  
   既定のパス名を使用する代わりにプリコンパイル済みヘッダーのパス名を指定します。  
  
   詳細については、「[/Fp (.pch ファイルの名前の指定)](https://msdn.microsoft.com/library/0fcd9cbd-e09f-44d3-9715-b41efb5d0be2)」を参照してください。  
  
- **PreprocessKeepComments**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合は、プリプロセス時にコメントが保持されます。  
  
   詳細については、「[/C (プリプロセス時のコメントの保持)](https://msdn.microsoft.com/library/944567ca-16bc-4728-befe-d414a7787f26)」を参照してください。  
  
- **PreprocessorDefinitions**  
  
   省略可能な `String[]` 型のパラメーターです。  
  
   ソース ファイルの前処理シンボルを定義します。  
  
   詳細については、「 [/D (Preprocessor Definitions)](https://msdn.microsoft.com/library/b53fdda7-8da1-474f-8811-ba7cdcc66dba)」を参照してください。  
  
- **PreprocessOutput**  
  
   省略可能な `ITaskItem[]` 型のパラメーターです。  
  
   タスクで使用および生成できるプリプロセッサ出力項目の配列を定義します。  
  
- **PreprocessOutputPath**  
  
   省略可能な `String` 型のパラメーターです。  
  
   **PreprocessToFile** パラメーターで前処理済みの出力を書き込む出力ファイルの名前を指定します。  
  
   詳細については、「[/Fi (出力ファイル名のプリプロセス)](https://msdn.microsoft.com/library/6d0ba983-a8b7-41ec-84f5-b4688ef8efee)」を参照してください。  
  
- **PreprocessSuppressLineNumbers**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合、C および C++ ソース ファイルが前処理され、前処理されたファイルが標準出力デバイスにコピーされます。  
  
   詳細については、「[/EP (#line ディレクティブを挿入しない stdout へのプリプロセス)](https://msdn.microsoft.com/library/6ec411ae-e33d-4ef5-956e-0054635eabea)」を参照してください。  
  
- **PreprocessToFile**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合、C および C++ ソース ファイルが前処理され、前処理済みの出力がファイルに書き込まれます。  
  
   詳細については、「[/P (プリプロセス出力のファイルへの書き込み)](https://msdn.microsoft.com/library/123ee54f-8219-4a6f-9876-4227023d83fc)」を参照してください。  
  
- **ProcessorNumber**  
  
   省略可能な `Integer` 型のパラメーターです。  
  
   マルチプロセッサ コンパイル時に使用するプロセッサの最大数を指定します。 このパラメーターは、**MultiProcessorCompilation** パラメーターと組み合わせて使用します。  
  
- **ProgramDataBaseFileName**  
  
   省略可能な `String` 型のパラメーターです。  
  
   プログラム データベース (PDB) ファイルの名前を指定します。  
  
   詳細については、「[/Fd (プログラム データベース ファイル名)](https://msdn.microsoft.com/library/3977a9ed-f0ac-45df-bf06-01cedd2ba85a)」を参照してください。  
  
- **RuntimeLibrary**  
  
   省略可能な `String` 型のパラメーターです。  
  
   マルチスレッド モジュールが DLL であるかどうかを指定し、ランタイム ライブラリのリテール バージョンまたはデバッグ バージョンを選択します。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **MultiThreaded** - **/MT**  
  
  - **MultiThreadedDebug** - **/MTd**  
  
  - **MultiThreadedDLL** - **/MD**  
  
  - **MultiThreadedDebugDLL** - **/MDd**  
  
    詳細については、「[/MD、/MT、/LD (ランタイム ライブラリの使用)](https://msdn.microsoft.com/library/cf7ed652-dc3a-49b3-aab9-ad60e5395579)」を参照してください。  
  
- **RuntimeTypeInfo**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合、実行時に C++ のオブジェクト型をチェックするコードが追加されます (ランタイム型情報)。  
  
   詳細については、「[/GR (ランタイム型情報の有効化)](https://msdn.microsoft.com/library/d1f9f850-dcec-49fd-96ef-e72d01148906)」を参照してください。  
  
- **ShowIncludes**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合、コンパイラでインクルード ファイルの一覧が出力されます。  
  
   詳細については、「[/showIncludes (インクルード ファイル一覧)](https://msdn.microsoft.com/library/0b74b052-f594-45a6-a7c7-09e1a319547d)」を参照してください。  
  
- **SmallerTypeCheck**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合、値がより小さいデータ型に割り当てられ、データ損失が発生したときに、ランタイム エラーが報告されます。  
  
   詳細については、「[/RTC (ランタイム エラー チェック)](https://msdn.microsoft.com/library/9702c558-412c-4004-acd5-80761f589368)」の **/RTCc** オプションに関する記述を参照してください。  
  
- **Sources**  
  
   必須の `ITaskItem[]` 型のパラメーターです。  
  
   スペースで区切られたソース ファイルのリストを指定します。  
  
- **StringPooling**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合、コンパイラで、プログラム イメージに同一文字列の 1 つのコピーを作成できます。  
  
   詳細については、「[/GF (同一文字列の削除)](https://msdn.microsoft.com/library/bb7b5d1c-8e1f-453b-9298-8fcebf37d16c)」を参照してください。  
  
- **StructMemberAlignment**  
  
   省略可能な `String` 型のパラメーターです。  
  
   構造体のすべてのメンバーのバイト配置を指定します。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **既定** - **/Zp1**  
  
  - **1Byte** - **/Zp1**  
  
  - **2Bytes** - **/Zp2**  
  
  - **4Bytes** - **/Zp4**  
  
  - **8Bytes** - **/Zp8**  
  
  - **16Bytes** - **/Zp16**  
  
    詳細については、「[/Zp (構造体メンバーの配置)](https://msdn.microsoft.com/library/5242f656-ed9b-48a3-bc73-cfcf3ed2520f)」を参照してください。  
  
- **SuppressStartupBanner**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合、タスクの開始時に著作権およびバージョン番号のメッセージが表示されないようにします。  
  
   詳細については、「[/nologo (著作権情報の非表示) (C/C++)](https://msdn.microsoft.com/library/75930d8b-b11c-4db8-99e5-b52f97da0693)」を参照してください。  
  
- **TrackerLogDirectory**  
  
   省略可能な `String` 型のパラメーターです。  
  
   このタスクの追跡ログの格納先となる中間ディレクトリを指定します。  
  
   詳細については、この表にある **TLogReadFiles** および **TLogWriteFiles** パラメーターを参照してください。  
  
- **TreatSpecificWarningsAsErrors**  
  
   省略可能な **String[]** 型のパラメーターです。  
  
   指定したコンパイラ警告の一覧をエラーとして扱います。  
  
   詳細については、「[/w、/Wn、/WX、/Wall、/wln、/wdn、/wen、/won (警告レベル)](https://msdn.microsoft.com/library/d6bc7bf5-c754-4879-909c-8e3a67e2629f)」の **/we**`n` オプションに関する記述を参照してください。  
  
- **TreatWarningAsError**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合、コンパイラが生成する警告がすべてエラーとして扱われます。  
  
   詳細については、「[/w、/Wn、/WX、/Wall、/wln、/wdn、/wen、/won (警告レベル)](https://msdn.microsoft.com/library/d6bc7bf5-c754-4879-909c-8e3a67e2629f)」の **/WX** オプションに関する記述を参照してください。  
  
- **TreatWChar_tAsBuiltInType**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合、`wchar_t` 型はネイティブ型として扱われます。  
  
   「[/Zc:wchar_t (wchar_t をネイティブ型として認識)](https://msdn.microsoft.com/library/b0de5a84-da72-4e5a-9a4e-541099f939e0)」を参照してください。  
  
- **UndefineAllPreprocessorDefinitions**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合、コンパイラで定義されている Microsoft 固有のシンボルの定義が解除されます。  
  
   詳細については、「[/U、/u (定義済みマクロ シンボルの未定義化)](https://msdn.microsoft.com/library/7bc0474f-6d1f-419b-807d-0d8816763b2a)」の **/u** オプションに関する記述を参照してください。  
  
- **UndefinePreprocessorDefinitions**  
  
   省略可能な `String[]` 型のパラメーターです。  
  
   定義を解除する 1 つ以上のプリプロセッサ シンボルの一覧を指定します。  
  
   詳細については、「[/U、/u (定義済みマクロ シンボルの未定義化)](https://msdn.microsoft.com/library/7bc0474f-6d1f-419b-807d-0d8816763b2a)」の **/U** オプションに関する記述を参照してください。  
  
- **UseFullPaths**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合、診断時にコンパイラに渡されるソース コード ファイルの完全パスが表示されます。  
  
   詳細については、「[/FC (診断時のソース コード ファイルの完全パス)](https://msdn.microsoft.com/library/1f11414e-cb42-421b-be68-9d369aab036b)」を参照してください。  
  
- **UseUnicodeForAssemblerListing**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合、出力ファイルが UTF-8 形式で作成されます。  
  
   詳細については、「[/FA、/Fa (リスティング ファイル)](https://msdn.microsoft.com/library/c7507d0e-c69d-44f9-b8e2-d2c398697402)」の **/FAu** オプションに関する記述を参照してください。  
  
- **WarningLevel**  
  
   省略可能な `String` 型のパラメーターです。  
  
   コンパイラによって生成される警告の最高レベルを指定します。  
  
   次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
  - **TurnOffAllWarnings** - **/W0**  
  
  - **Level1** - **/W1**  
  
  - **Level2** - **/W2**  
  
  - **Level3** - **/W3**  
  
  - **Level4** - **/W4**  
  
  - **EnableAllWarnings** - **/Wall**  
  
    詳細については、「[/w、/Wn、/WX、/Wall、/wln、/wdn、/wen、/won (警告レベル)](https://msdn.microsoft.com/library/d6bc7bf5-c754-4879-909c-8e3a67e2629f)」の **/W**_n_ オプションに関する記述を参照してください。  
  
- **WholeProgramOptimization**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合、プログラム全体の最適化が有効になります。  
  
   詳細については、「[/GL (プログラム全体の最適化)](https://msdn.microsoft.com/library/09d51e2d-9728-4bd0-b5dc-3b8284aca1d1)」を参照してください。  
  
- **XMLDocumentationFileName**  
  
   省略可能な `String` 型のパラメーターです。  
  
   生成される XML ドキュメント ファイルの名前を指定します。 このパラメーターには、ファイルまたはディレクトリ名を指定できます。  
  
   詳細については、「[/doc (ドキュメント コメントの処理) (C/C++)](https://msdn.microsoft.com/library/b54f7e2c-f28f-4f46-9ed6-0db09be2cc63)」の `name` 引数に関する記述を参照してください。 この表の **GenerateXMLDocumentationFiles** パラメーターも参照してください。  
  
- **MinimalRebuildFromTracking**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合、追跡対象のインクリメンタル ビルドが実行され、`false` の場合は、リビルドが実行されます。  
  
- **TLogReadFiles**  
  
   省略可能な `ITaskItem[]` 型のパラメーターです。  
  
   *ファイルの読み取り追跡ログ*を表す項目の配列を指定します。  
  
   ファイルの読み取り追跡ログ (.tlog) には、タスクによって読み取られ、プロジェクト ビルド システムによってインクリメンタル ビルドをサポートするために使用される入力ファイルの名前が含まれています。 詳細については、この表の **TrackerLogDirectory** および **TrackFileAccess** パラメーターを参照してください。  
  
- **TLogWriteFiles**  
  
   省略可能な `ITaskItem[]` 型のパラメーターです。  
  
   *ファイルの書き込み追跡ログ*を表す項目の配列を指定します。  
  
   ファイルの書き込み追跡ログ (.tlog) には、タスクによって読み取られ、プロジェクト ビルド システムによってインクリメンタル ビルドをサポートするために使用される出力ファイルの名前が含まれています。 詳細については、この表の **TrackerLogDirectory** および **TrackFileAccess** パラメーターを参照してください。  
  
- **TrackFileAccess**  
  
   省略可能な `Boolean` 型のパラメーターです。  
  
   `true` の場合、ファイル アクセス パターンが追跡されます。  
  
   詳細については、この表にある **TLogReadFiles** および **TLogWriteFiles** パラメーターを参照してください。  
  
## <a name="remarks"></a>解説  
  
## <a name="see-also"></a>関連項目
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)
