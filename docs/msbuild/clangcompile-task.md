---
title: ClangCompile タスク | Microsoft Docs
ms.date: 03/10/2019
ms.topic: reference
f1_keywords:
- vc.task.clangcompile
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (C++), ClangCompile task
- ClangCompile task (MSBuild (C++))
author: corob-msft
ms.author: corob
ms.workload:
- multiple
ms.openlocfilehash: c1526fbd3c2c0822781f0e011999ddcb9c679170
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77275464"
---
# <a name="clangcompile-task"></a>ClangCompile タスク

Microsoft C++ コンパイラ ツール clang.exe をラップします。

## <a name="parameters"></a>パラメーター

**ClangCompile** タスクのパラメーターの説明を次の表に示します。

|パラメーター|[説明]|
|---------------|-----------------|
|**AdditionalIncludeDirectories**|省略可能な **string[]** 型のパラメーターです。<br/><br/>インクルード パスに追加するディレクトリを 1 つ以上指定します。複数指定する場合には、セミコロンで区切ってください。<br/><br/>`-I[path]`を使用します。|
|**AdditionalOptions**|省略可能な **string** 型のパラメーターです。|
|**BufferSecurityCheck**|省略可能な **string** 型のパラメーターです。<br/><br/>セキュリティ チェックでは、プログラムのセキュリティに対する一般的な攻撃であるスタックバッファー オーバーランを検出できます。 <br/><br/>`fstack-protector`を使用します。|
|**BuildingInIde**|省略可能な **bool** 型のパラメーターです。|
|**CLanguageStandard**|省略可能な **string** 型のパラメーターです。<br/><br/>C 言語標準を決定します。<br/><br/>**c89**、**c99**、**c11**、**gnu99**、または **gnu11** の値と共に `std=[value]` を使います。|
|**ClangVersion**|省略可能な **string** 型のパラメーターです。|
|**CompileAs**|省略可能な **string** 型のパラメーターです。<br/><br/>.c および .cpp ファイルのコンパイル言語オプションを選択します。 既定では .c または .cpp 拡張に基づいて検出します。<br/><br/>`-x c`、`-x c++` を使います。|
|**CppLanguageStandard**|省略可能な **string** 型のパラメーターです。<br/><br/>C++ 言語標準を決定します。<br/><br/>**c++98**、**c++11**、**c++1y**、**gnu++98**、**gnu++11**、または **gnu++1y** の値と共に `std=[value]` を使います。|
|**DataLevelLinking**|省略可能な **bool** 型のパラメーターです。<br/><br/>データ項目ごとにセクションを別にすることで、未使用データを削除するリンカー最適化を有効にします。|
|**DebugInformationFormat**|省略可能な **string** 型のパラメーターです。<br/><br/>コンパイラによって生成されるデバッグ情報の種類を指定します。<br/><br/>**None**: デバッグ情報が生成されないため、コンパイルが高速になる可能性があります (`g0` を使います)。<br/>**FullDebug**: DWARF2 のデバッグ情報を生成します (`g2 -gdwarf-2` を使います)。<br/>**LineNumber**: 行番号情報のみを生成します (`gline-tables-only`を使います)。|
|**EnableNeonCodegen**|省略可能な **bool** 型のパラメーターです。<br/><br/>NEON の浮動小数点演算ハードウェアのコード生成を有効にします。 これは、arm アーキテクチャにのみ適用されます。|
|**ExceptionHandling**|省略可能な **string** 型のパラメーターです。<br/><br/>コンパイラで使用する例外処理のモデルを指定します。<br/><br/>**Disabled**: 例外処理を無効にします (`fno-exceptions` を使います)。<br/>**Enabled**: 例外処理を有効にします (`fexceptions` を使います)。<br/>**UnwindTables**: 必要な静的データが生成されますが、生成されるコードには影響しません (`funwind-tables` を使います)。|
|**FloatABI**|省略可能な **string** 型のパラメーターです。<br/><br/>ABI の浮動小数点を選ぶ選択肢。<br/><br/>**soft**: 浮動小数点演算のライブラリ呼び出しを含む出力をコンパイラに生成させます (`mfloat-abi=soft` を使います)。<br/>**softfp**: ハードウェアの浮動小数点命令を使用したコード生成が可能になりますが、引き続き soft-float 呼び出し規約が使用されます (`mfloat-abi=softfp` を使います)。<br/>**hard**: 浮動小数点命令の生成が可能になり、FPU 固有の呼び出し規約が使用されます (`mfloat-abi=hard` を使います)。|
|**ForcedIncludeFiles**|省略可能な **string[]** 型のパラメーターです。<br/><br/>1 つ以上の強制インクルード ファイルです。<br/><br/>`-include [name]`を使用します。|
|**FunctionLevelLinking**|省略可能な **bool** 型のパラメーターです。<br/><br/>コンパイラが個々の関数をパッケージ関数 (COMDAT) の形式でパッケージ化できるようになります。 エディット コンティニュの機能に必要です。<br/><br/>`ffunction-sections`を使用します。|
|**GccToolChain**|省略可能な **string** 型のパラメーターです。<br/><br/>Gcc ツール チェーンのフォルダー パス。|
|**GNUMode**|省略可能な **bool** 型のパラメーターです。<br/><br/>|
|**MSCompatibility**|省略可能な **bool** 型のパラメーターです。<br/><br/>Microsoft C++ の完全互換性を有効にします。|
|**MSCompatibilityVersion**|省略可能な **string** 型のパラメーターです。<br/><br/>_MSC_VER にレポートする Microsoft コンパイラのバージョン番号を表す、ドットで区切られた値 (0 = 定義しない (既定値))。|
|**MSExtensions**|省略可能な **bool** 型のパラメーターです。<br/><br/>Microsoft コンパイラでサポートされている非標準のコンストラクトの一部を受け入れます。|
|**MSCompilerVersion**|省略可能な **string** 型のパラメーターです。<br/><br/>MSC_VER にレポートする Microsoft コンパイラのバージョン番号 (0 = 定義しない (既定値))。|
|**MSVCErrorReport**|省略可能な **bool** 型のパラメーターです。<br/><br/>ファイルと行の情報を分析するために Visual Studio が使用できるエラーを報告します。|
|**ObjectFileName**|省略可能な **string** 型のパラメーターです。<br/><br/>既定のオブジェクト ファイル名をオーバーライドする名前を指定します。ファイル名またはディレクトリ名を指定できます。<br/><br/>`/Fo[name]`を使用します。|
|**OmitFramePointers**|省略可能な **bool** 型のパラメーターです。<br/><br/>呼び出し履歴にフレーム ポインターが作成されなくなります。|
|**Optimization**|省略可能な **string** 型のパラメーターです。<br/><br/>アプリケーションの最適化レベルを指定します。<br/><br/>**Custom**: カスタムの最適化。<br/>**Disabled**: 最適化を無効にします (`O0` を使います)。<br/>**MinSize**: サイズを最適化します (`Os` を使います)。<br/>**MaxSpeed**: 速度を最適化します (`O2` を使います)。<br/>**Full**: 高価な最適化 (`O3` を使います)。|
|**PositionIndependentCode**|省略可能な **bool** 型のパラメーターです。<br/><br/>共有ライブラリで使用する位置独立コード (PIC) を生成します。|
|**PrecompiledHeader**|省略可能な **string** 型のパラメーターです。<br/><br/>プリコンパイル済みヘッダーをビルド中に作成または使用できるようになります。|
|**PrecompiledHeaderFile**|省略可能な **string** 型のパラメーターです。<br/><br/>プリコンパイル済みヘッダー ファイルに使用するヘッダー ファイル名を指定します。 このファイルは、ビルド中に **[必ず使用されるインクルード ファイル]** にも追加されます。|
|**PrecompiledHeaderOutputFileDirectory**|省略可能な **string** 型のパラメーターです。<br/><br/>生成されたプリコンパイル済みヘッダー用のディレクトリを指定します。 このディレクトリは、ビルド中に **[追加のインクルード ディレクトリ]** にも追加されます。|
|**PrecompiledHeaderCompileAs**|省略可能な **string** 型のパラメーターです。<br/><br/>プリコンパイル済みヘッダー ファイルのコンパイル言語オプションを選択します。<br/><br/>`-x c-header`、`-x c++-header` を使います。|
|**PreprocessorDefinitions**|省略可能な **string[]** 型のパラメーターです。<br/><br/>ソース ファイルの前処理シンボルを定義します。<br/><br/>`-D`を使用します。|
|**RuntimeLibrary**|省略可能な **string** 型のパラメーターです。<br/><br/>リンクするランタイム ライブラリを指定します。<br/><br/>`MSVC /MT`、`/MTd`、`/MD`、`/MDd` スイッチを使います。<br/><br/>**MultiThreaded**: アプリケーションで、ランタイム ライブラリのマルチスレッド、静的バージョンが使用されます。<br/>**MultiThreadedDebug**: _DEBUG と _MT を定義します。 このオプションによって、リンカーが LIBCMTD.lib を使用して外部シンボルを解決できるように、コンパイラによりライブラリ名 LIBCMTD.lib が .obj ファイルに挿入されます。<br/>**MultiThreadedDLL**: アプリケーションで、ランタイム ライブラリのマルチスレッドおよび DLL 対応バージョンが使用されます。 _MT および _DLL を定義し、コンパイラにライブラリ名 MSVCRT.lib を .obj ファイルに挿入させます。<br/>**MultiThreadedDebugDLL**: _DEBUG、_MT、および _DLL が定義され、アプリケーションで、ランタイム ライブラリのデバッグ マルチスレッドおよび DLL 対応バージョンが使用されます。 また、コンパイラによって、ライブラリ名 MSVCRTD.lib が .obj ファイルに挿入されます。|
|**RuntimeTypeInfo**|省略可能な **bool** 型のパラメーターです。<br/><br/>実行時に C++ のオブジェクト型をチェックするコードを追加します (ランタイム型情報)。<br/><br/>`frtti`、`fno-rtti` を使います。|
|**ShowIncludes**|省略可能な **bool** 型のパラメーターです。<br/><br/>コンパイラ出力を持つインクルード ファイルのリストを生成します。<br/><br/>`-H`を使用します。|
|**Sources**|必須の **ITaskItem[]** 型のパラメーターです。|
|**StrictAliasing**|省略可能な **bool** 型のパラメーターです。<br/><br/>厳密なエイリアスのルールを想定します。 ある型のオブジェクトが別の型のオブジェクトと同じアドレスに存在することは決してないと想定します。|
|**Sysroot**|省略可能な **string** 型のパラメーターです。<br/><br/>ヘッダーおよびライブラリのルート ディレクトリのフォルダー パス。|
|**TargetArch**|省略可能な **string** 型のパラメーターです。<br/><br/>ターゲット アーキテクチャです。|
|**ThumbMode**|省略可能な **string** 型のパラメーターです。<br/><br/>Thumb マイクロアーキテクチャを実行するコードを生成します。 これは、arm アーキテクチャにのみ適用されます。<br/><br/>**Thumb**: Thumb コードを生成します (`mthumb` を使います)。<br/>**ARM**: Arm コードを生成します (`marm` を使います)。<br/>**Disabled**: オプションは選択したプラットフォームには適用されません。|
|**TrackerLogDirectory**|省略可能な **string** 型のパラメーターです。<br/><br/>トラッカー ログのディレクトリです。|
|**TreatWarningAsError**|省略可能な **bool** 型のパラメーターです。<br/><br/>コンパイラ警告をすべてエラーとして扱います。<br/><br/>新しいプロジェクトの場合、すべてのコンパイルで `/WX` を使用することをお勧めします。すべての警告を解決することで、見つけにくいコードの欠陥を最少に抑えられます。|
|**UndefinePreprocessorDefinitions**|省略可能な **string[]** 型のパラメーターです。<br/><br/>1 つ以上のプリプロセッサ定義の無効化を指定します。<br/><br/>`-U [macro]`を使用します。|
|**UndefineAllPreprocessorDefinitions**|省略可能な **bool** 型のパラメーターです。<br/><br/>すべてのプリプロセッサの定義済み定義を無効にします。<br/><br/>`-undef`を使用します。|
|**UseMultiToolTask**|省略可能な **bool** 型のパラメーターです。<br/><br/>複数プロセッサによるコンパイルです。|
|**UseShortEnums**|省略可能な **bool** 型のパラメーターです。<br/><br/>列挙型は、入力された使用できる値に必要なバイト数と同じバイト数を使用します。|
|**詳細**|省略可能な **bool** 型のパラメーターです。<br/><br/>実行するコマンドを表示して、詳細出力を使用します。|
|**WarningLevel**|省略可能な **string** 型のパラメーターです。<br/><br/>コード エラーに対するコンパイラの警告レベルを指定します。 その他のフラグは、 **[その他のオプション]** に直接追加する必要があります (`/w`、`/Weverything` を使います)。<br/><br/>**TurnOffAllWarnings**: すべてのコンパイラ警告を無効にします (`w` を使います)。<br/>**EnableAllWarnings**: 既定で無効にされている警告を含む、すべての警告を有効にします (`Wall` を使います)。|

## <a name="see-also"></a>参照

[タスク リファレンス](../msbuild/msbuild-task-reference.md)