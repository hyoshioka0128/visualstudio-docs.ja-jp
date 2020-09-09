---
title: IntelliSense の C++ プロジェクトを構成する
ms.date: 10/08/2018
ms.topic: conceptual
author: corob-msft
ms.author: corob
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: 610f3d92d86e227973be9c481adaf830d3d16737
ms.sourcegitcommit: 5caad925ca0b5d136416144a279e984836d8f28c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2020
ms.locfileid: "89509888"
---
# <a name="configure-a-c-project-for-intellisense"></a>IntelliSense の C++ プロジェクトを構成する

場合によっては、IntelliSense が正常に機能するために、C++ プロジェクトを手動で構成する必要があります。 (.vcxproj ファイルに基づく) MSBuild プロジェクトの場合は、プロジェクト プロパティで設定を調整できます。 MSBuild 以外のプロジェクトの場合は、プロジェクトのルート ディレクトリにある CppProperties.json ファイルで設定を調整します。 場合によっては、IntelliSense がマクロ定義を解釈できるようにヒント ファイルを作成する必要があります。 Visual Studio IDE は、IntelliSense の問題を特定して修正するのに役立ちます。

## <a name="single-file-intellisense"></a>単一ファイルの IntelliSense

プロジェクトに含まれていないファイルを開くと、Visual Studio によっていくつかの IntelliSense サポートが提供されますが、既定ではエラーを示す波線は表示されません。 **ナビゲーション バー**に *[その他のファイル]* が表示されている場合は、それが不正なコードの下にエラーを示す波線が表示されない理由、またはプリプロセッサ マクロが定義されていない理由の説明になる場合があります。

## <a name="check-the-error-list"></a>エラー一覧を確認する

ファイルがシングルファイル モードで開いておらず、IntelliSense が正しく機能していない場合に、最初に確認するのが [エラー一覧] ウィンドウです。 現在のソース ファイルのすべての IntelliSense エラーを、含まれているすべてのヘッダー ファイルとともに表示するには、ドロップダウンで **[ビルド + IntelliSense]** を選択します。

![エラー一覧の VC++ IntelliSense](media/vcpp-intellisense-error-list.png)

IntelliSense では、最大 1000 個のエラーが生成されます。 ソース ファイルに含まれるヘッダー ファイルに 1000 を超えるエラーがある場合、ソース ファイルの先頭に 1 つのエラーの波線だけが表示されます。

## <a name="ensure-include-paths-are-correct"></a>#include パスが正しいことを確認する

### <a name="msbuild-projects"></a>MSBuild プロジェクト

Visual Studio IDE の外部でビルドを実行し、ビルドは成功したが IntelliSense が正しくない場合、コマンドラインが 1 つまたは複数の構成のプロジェクト設定と同期していない可能性があります。 **ソリューション エクスプローラー**でプロジェクト ノードを右クリックして、現在の構成とプラットフォームに対してすべての **#include** パスが正しいことを確認します。 すべての構成とプラットフォームでパスが同一の場合は、 **[すべての構成]** と **[すべてのプラットフォーム]** を選択し、パスが正しいことを確認します。

![VC++ インクルード ディレクトリ](media/vcpp-intellisense-include-paths.png)

**VC_IncludePath** などのビルド マクロの現在の値を表示するには、[インクルード ディレクトリ] 行を選択し、右側のドロップダウンをクリックします。 次に、 **[\<Edit>]** を選択し、 **[マクロ]** ボタンをクリックします。

### <a name="makefile-projects"></a>メイクファイル プロジェクト

NMake プロジェクト テンプレートに基づくメイクファイル プロジェクトの場合は、左側のウィンドウで **[NMake]** を選択してから、 **[IntelliSense]** カテゴリの下で **[インクルードの検索パス]** を選択します。

![メイクファイル プロジェクトのインクルード パス](media/vcpp-intellisense-makefile-include-paths.png)

### <a name="open-folder-projects"></a>"フォルダーを開く" プロジェクト

CMake プロジェクトの場合は、CMakeLists.txt ですべての構成に対して #include パスが正しく指定されていることを確認します。 その他のプロジェクトの種類では、CppProperties.json ファイルが必要になる場合があります。 詳細については、[CppProperties.json を使って IntelliSense を構成する](/cpp/build/open-folder-projects-cpp#configure-code-navigation-with-cpppropertiesjson)に関するページを参照してください。 ファイルで定義されている各構成に対するパスが正しいことを確認します。

CppProperties.json ファイルに構文エラーがある場合、影響を受けるファイル内の IntelliSense は不正になります。 Visual Studio の出力ウィンドウにエラーが表示されます。

## <a name="tag-parser-issues"></a>タグ パーサーの問題

タグ パーサーは、参照とナビゲーションに使用される "あいまいな" C++ パーサーです。 これは非常に高速ですが、すべてのコード コンストラクトを完全に理解しようとはしません。

たとえば、プリプロセッサ マクロを評価しないため、それらを多用するコードを誤って解析する場合があります。 タグ パーサーにより、未知のコード コンストラクターが検出されると、そのコードの領域の全体がスキップされることがあります。

Visual Studio では、この問題を明示する 2 つの一般的な方法があります。

1. ナビゲーション バーに最も内側のマクロが表示されている場合は、現在の関数定義はスキップされました。

   ![タグ パーサーにより関数の定義がスキップされる](media/vcpp-intellisense-tag-parser-macro.png)

1. IDE は、既に定義されている関数に対して関数定義を作成します。

   ![タグ パーサーにより既存の関数の定義が提案される](media/vcpp-intellisense-tag-parser-function.png)

この種の問題を解決するには、**cpp.hint** という名前のファイルをソリューション ディレクトリのルートに追加します。 詳細については、「[ヒント ファイル](/cpp/build/reference/hint-files)」を参照してください。

タグ パーサーのエラーは、 **[エラー一覧]** ウィンドウに表示されます。

## <a name="validate-project-settings-with-diagnostic-logging"></a>診断ログでプロジェクト設定を検証する

IntelliSense コンパイラが、インクルード パスとプリプロセッサ マクロを含む正しいコンパイラ オプションを使用しているかどうかを確認するには、IntelliSense コマンド ラインの診断ログ ( **[ツール] > [オプション] > [テキスト エディター] > [C/C++] > [詳細設定]> [診断ログ]** ) をオンにします。 **[ログの有効化]** を True、 **[ログ レベル]** を 5 (最も詳細)、 **[ログ フィルター]** を 8 (IntelliSense ログ) に設定します。

出力ウィンドウに、IntelliSense コンパイラに渡されるコマンドラインが表示されます。 出力例を次に示します。

```output
[IntelliSense] Configuration Name: Debug|Win32
[IntelliSense] Toolset IntelliSense Identifier:
[IntelliSense] command line options:
/c
/I.
/IC:\Repo\Includes
/DWIN32
/DDEBUG
/D_DEBUG
/Zc:wchar_t-
/Zc:forScope
/Yustdafx.h
```

この情報は、IntelliSense が不正確な情報を提供している理由を理解するのに役立ちます。 たとえば、プロジェクトのインクルード ディレクトリに **$(MyVariable)\Include** が含まれていて、診断ログにインクルード パスとして **/I\Include** が表示される場合、 **$(MyVariable)** は評価されず、最終的なインクルード パスから削除されたことを意味します。

## <a name="about-the-intellisense-build"></a>IntelliSense のビルドについて

Visual Studio では、専用の C++ コンパイラを使用して、すべての IntelliSense 機能を実現するデータベースを作成および維持します。 IntelliSense データベースをコードと同期させるため、Visual Studio はプロジェクト設定またはソース ファイルに行われた特定の変更に応えて、IntelliSense 専用のビルドをバックグラウンド タスクとして自動的に起動します。

ただし、場合によっては、Visual Studio で IntelliSense データベースが適切なタイミングで更新されない場合があります。 たとえば、**git pull** または **git checkout** コマンドを実行すると、Visual Studio でファイル内の変更を検出するのに、最大 1 時間かかる場合があります。 **ソリューション エクスプローラー**でプロジェクト ノードを右クリックして **[ソリューションの再スキャン]** を選択し、ソリューション内のすべてのファイルの再スキャンを強制することができます。

## <a name="troubleshooting-intellisense-build-failures"></a>IntelliSense のビルド エラーのトラブルシューティング

IntelliSense のビルドでは、バイナリは作成されませんが、それでもエラーが発生する可能性があります。 エラーの考えられる原因の 1 つは、.props や .targets のカスタム ファイルです。 Visual Studio 2017 バージョン 15.6 以降では、IntelliSense 専用のビルド エラーが出力ウィンドウに記録されます。 これらを表示するには、 **[出力元の表示]** を **[ソリューション]** に設定します。

![ソリューション エラーの出力ウィンドウ](media/vcpp-intellisense-output-window.png)

エラー メッセージに、デザイン時のトレースを有効にする指示が含まれていることがあります。

```output
error: Designtime build failed for project 'E:\src\MyProject\MyProject.vcxproj',
configuration 'Debug|x64'. IntelliSense might be unavailable.
Set environment variable TRACEDESIGNTIME=true and restart
Visual Studio to investigate.
```

環境変数 TRACEDESIGNTIME を true に設定して、Visual Studio を再起動すると、ビルド エラーの診断に役立つ可能性がある %TEMP% ディレクトリ内のログ ファイルが表示されます。

環境変数 TRACEDESIGNTIME の詳細については、[Roslyn](https://github.com/dotnet/roslyn/blob/master/docs/wiki/Diagnosing-Project-System-Build-Errors.md)と[共通プロジェクト システム](https://github.com/dotnet/project-system/blob/master/docs/design-time-builds.md)に関するページを参照してください。 これらの記事の情報は、C++ プロジェクトに関連します。

## <a name="see-also"></a>参照

- [Visual C++ IntelliSense](visual-cpp-intellisense.md)
