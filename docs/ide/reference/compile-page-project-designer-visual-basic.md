---
title: '[コンパイル] ページ、プロジェクト デザイナー (Visual Basic)'
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesCompile
helpviewer_keywords:
- compilation, Visual Basic projects
- compilation, options [Visual Basic]
- compilers, Visual Basic options
- compilation, instructions [Visual Basic]
- compiler options, Visual Basic
- Project Designer, Compile page
- Compile page in Project Designer
ms.assetid: b2a80230-906e-4e85-b3e0-fcd9c40426e1
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9d7a97068b70a76dfe343de5fa68db77d2ce9781
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76111307"
---
# <a name="compile-page-project-designer-visual-basic"></a>[コンパイル] ページ、プロジェクト デザイナー (Visual Basic)

プロジェクト デザイナーの **[コンパイル]** ページを使用して、コンパイル命令を指定します。 このページでは、高度なコンパイラ オプションとビルド前またはビルド後のイベントを指定することもできます。

**[コンパイル]** ページにアクセスするには、**ソリューション エクスプローラー**でプロジェクト ノード ( **[ソリューション]** ノードではありません) を選択します。 その後、メニュー バーで **[プロジェクト]** 、 **[プロパティ]** の順に選択します。 プロジェクト デザイナーが表示されたら、 **[コンパイル]** タブをクリックします。

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

## <a name="configuration-and-platform"></a>構成およびプラットフォーム

次の設定を使用すると、表示または変更する構成およびプラットフォームを選択できます。

> [!NOTE]
> 簡易ビルド構成を使用した場合、デバッグ バージョンとリリース バージョンのどちらをビルドするかの決定はプロジェクト システムによって行われます。 したがって、**構成**リストと**プラットフォーム** リストは表示されません。

**構成**

表示または変更する構成設定を指定します。 設定は、 **[デバッグ]** (既定)、 **[リリース]** 、または **[すべての構成]** のいずれかになります。 詳細については、「[ビルド構成について](../../ide/understanding-build-configurations.md)」と「[方法:構成を作成および編集する](../../ide/how-to-create-and-edit-configurations.md)」を参照してください。

**プラットフォーム**

表示または変更するプラットフォーム設定を指定します。 **[任意の CPU]** (既定)、 **[x64]** 、または **[x86]** を指定できます。

## <a name="compiler-configuration-options"></a>コンパイラの構成オプション

次の設定を使用すると、コンパイラの構成オプションを設定できます。

**ビルド出力パス**

このプロジェクト構成の出力ファイルの場所を指定します。 このボックスにビルド出力のパスを入力するか、 **[参照]** ボタンをクリックしてパスを選択します。 このパスは、相対パスであることに注意してください。絶対パスを入力しても、相対パスとして保存されます。 既定のパスは bin\Debug\ または bin\Release\\ です。

簡易ビルド構成を使用した場合、デバッグ バージョンとリリース バージョンのどちらをビルドするかの決定はプロジェクト システムによって行われます。 **[デバッグ]** メニューの **[ビルド]** コマンド (F5) を使用すると、指定した **[出力パス]** に関係なく、デバッグ用の場所にビルドが配置されます。 ただし、 **[ビルド]** メニューの **[ビルド]** コマンドでは、指定した場所にビルドが配置されます。

**Option Explicit**

変数の暗黙的な宣言を許可するかどうかを指定します。 変数の明示的な宣言を要求する場合は **[オン]** を選択します。 これにより、変数が使用される前に宣言されていないと、コンパイラがエラーを報告します。 変数の暗黙的な宣言を許可するには、 **[オフ]** を選択します。

この設定は、[/optionexplicit](/dotnet/visual-basic/reference/command-line-compiler/optionexplicit) コンパイラ オプションに相当します。

ソース コード ファイルに [Option Explicit ステートメント](/dotnet/visual-basic/language-reference/statements/option-explicit-statement)が含まれている場合、ステートメント内の `On` または `Off` の値が、 **[コンパイル]** ページの **[Option Explicit]** 設定をオーバーライドします。

新しいプロジェクトを作成するときに、 **[コンパイル]** ページの **[Option Explicit]** 設定が **[オプション]** ダイアログ ボックスの **[Option Explicit]** 設定の値に設定されます。 このダイアログ ボックスの設定を表示または変更するには、 **[ツール]** メニューで **[オプション]** をクリックします。 **[オプション]** ダイアログ ボックスの **[プロジェクトおよびソリューション]** を展開し、 **[VISUAL BASIC の既定値]** をクリックします。 **[VISUAL BASIC の既定値]** での **[Option Explicit]** の初期の既定値は **[オン]** です。

**[Option Explicit]** を `Off` に設定することは、通常はお勧めできません。 変数名のスペルを 1 か所以上間違えると、プログラムの実行時に予期しない結果を招く可能性があります。

**Option Strict**

厳密な型セマンティクスを適用するかどうかを指定します。 **[Option Strict]** が **[オン]** になっていると、次の条件によりコンパイル時エラーが発生します。

- 暗黙的な縮小変換

- 遅延バインディング

- 結果が `Object` 型となる暗黙の型指定

縮小変換する暗黙的なデータ型変換がある場合は、暗黙的な縮小変換エラーが発生します。 詳細については、「[Option Strict ステートメント](/dotnet/visual-basic/language-reference/statements/option-strict-statement)」、「[暗黙の型変換と明示的な型変換](/dotnet/visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions)」、および「[拡大変換と縮小変換](/dotnet/visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions)」を参照してください。

`Object` 型として宣言された変数のプロパティまたはメソッドにオブジェクトを代入する場合は、そのオブジェクトは遅延バインディングされます。 詳細については、「[Option Strict ステートメント](/dotnet/visual-basic/language-reference/statements/option-strict-statement)」および「[事前バインディングと遅延バインディング](/dotnet/visual-basic/programming-guide/language-features/early-late-binding)」を参照してください。

適切な型が宣言された変数を推論できない場合は暗黙的なオブジェクトの型エラーが発生するため、`Object` の型が推論されます。 これは主に、`As` 句を使用せず、`Option Infer` をオフにして、`Dim` ステートメントを使用して変数を宣言した場合に発生します。 詳細については、「[Option Strict ステートメント](/dotnet/visual-basic/language-reference/statements/option-strict-statement)」、「[Option Infer ステートメント](/dotnet/visual-basic/language-reference/statements/option-infer-statement)」、および「[Visual Basic Language Specification](/dotnet/visual-basic/reference/language-specification)」 (Visual Basic 言語仕様) を参照してください。

**[Option Strict]** 設定は、[/optionstrict](/dotnet/visual-basic/reference/command-line-compiler/optionstrict) コンパイラ オプションに相当します。

ソース コード ファイルに [Option Strict ステートメント](/dotnet/visual-basic/language-reference/statements/option-strict-statement)が含まれている場合、ステートメント内の `On` または `Off` の値が、 **[コンパイル]** ページの **[Option Strict]** 設定をオーバーライドします。

プロジェクトを作成するときに、 **[コンパイル]** ページの **[Option Strict]** 設定が **[オプション]** ダイアログ ボックスの **[Option Strict]** 設定の値に設定されます。 このダイアログ ボックスの設定を表示または変更するには、 **[ツール]** メニューで **[オプション]** をクリックします。 **[オプション]** ダイアログ ボックスの **[プロジェクトおよびソリューション]** を展開し、 **[VISUAL BASIC の既定値]** をクリックします。 **[VISUAL BASIC の既定値]** での **[Option Strict]** の初期の既定値は **[オフ]** です。

**Option Strict の個々の警告**

**[コンパイル]** ページの **[警告の構成]** セクションには、`Option Strict` がオンになっているときにコンパイル時エラーが発生する 3 つの条件に相当する設定があります。 これらの設定を次に示します。

- **暗黙的な変換**

- **遅延バインディング、呼び出しが実行時に失敗する可能性があります**

- **暗黙的な型、オブジェクトと見なされます**

**[Option Strict]** を **[オン]** に設定すると、これら 3 つの警告の構成設定のすべてが **[エラー]** に設定されます。 **[Option Strict]** を **[オフ]** に設定すると、3 つの設定すべてが **[なし]** に設定されます。

各警告の構成設定を個別に **[なし]** 、 **[警告]** 、または **[エラー]** に変更することができます。 3 つの警告の構成設定がすべて **[エラー]** に設定されている場合、`Option strict` ボックスに `On` が表示されます。 3 つすべてが **[なし]** に設定されている場合、このボックスには `Off` が表示されます。 これらの設定のその他の組み合わせに対しては、 **(カスタム)** が表示されます。

**Option Compare**

使用する文字列比較の種類を指定します。 バイナリの大文字と小文字を区別する文字列比較を使用するようにコンパイラに指示するには、 **[バイナリ]** を選択します。 ロケール固有の大文字と小文字を区別しないテキスト文字列比較を使用するには、 **[テキスト]** を選択します。

この設定は、[/optioncompare](/dotnet/visual-basic/reference/command-line-compiler/optioncompare) コンパイラ オプションに相当します。

ソース コード ファイルに [Option Compare ステートメント](/dotnet/visual-basic/language-reference/statements/option-compare-statement)が含まれている場合、ステートメント内の `Binary` または `Text` の値が、 **[コンパイル]** ページの **[Option Compare]** 設定をオーバーライドします。

プロジェクトを作成するときに、 **[コンパイル]** ページの **[Option Compare]** 設定が **[オプション]** ダイアログ ボックスの **[Option Compare]** 設定の値に設定されます。 このダイアログ ボックスの設定を表示または変更するには、 **[ツール]** メニューで **[オプション]** をクリックします。 **[オプション]** ダイアログ ボックスの **[プロジェクトおよびソリューション]** を展開し、 **[VISUAL BASIC の既定値]** をクリックします。 **[VISUAL BASIC の既定値]** での **[Option Compare]** の初期の既定値は **[バイナリ]** です。

**Option Infer**

変数宣言でローカル型推論を許可するかどうかを指定します。 ローカル型推論の使用を許可するには、 **[オン]** を選択します。 ローカル型推論をブロックするには、 **[オフ]** を選択します。

この設定は、[/optioninfer](/dotnet/visual-basic/reference/command-line-compiler/optioninfer) コンパイラ オプションに相当します。

ソース コード ファイルに [Option Infer ステートメント](/dotnet/visual-basic/language-reference/statements/option-infer-statement)が含まれている場合、ステートメント内の `On` または `Off` の値が、 **[コンパイル]** ページの **[Option Infer]** 設定をオーバーライドします。

プロジェクトを作成するときに、 **[コンパイル]** ページの **[Option Infer]** 設定が **[オプション]** ダイアログ ボックスの **[Option Infer]** 設定の値に設定されます。 このダイアログ ボックスの設定を表示または変更するには、 **[ツール]** メニューで **[オプション]** をクリックします。 **[オプション]** ダイアログ ボックスの **[プロジェクトおよびソリューション]** を展開し、 **[VISUAL BASIC の既定値]** をクリックします。 **[VISUAL BASIC の既定値]** での **[Option Infer]** の初期の既定値は **[オン]** です。

**対象の CPU**

出力ファイルがターゲットとするプロセッサを指定します。 32 ビット Intel 互換プロセッサの場合は **[x86]** を、64 ビット Intel 互換プロセッサの場合は **[x64]** を、ARM プロセッサの場合は **[ARM]** をそれぞれ指定します。または、どのプロセッサでもかまわないことを指定する場合は、 **[任意の CPU]** を選択します。 **[任意の CPU]** は、ほとんどのハードウェアの種類でアプリケーションの実行を許可しているため、これが新しいプロジェクトの既定値となります。

詳細については、「[/platform (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/platform)」を参照してください。

**32 ビットを優先**

**[32 ビットの優先]** チェック ボックスがオンの場合、アプリケーションは、Windows の 32 ビット バージョンおよび 64 ビット バージョンで 32 ビット アプリケーションとして実行されます。 それ以外の場合は、アプリケーションは、Windows の 32 ビット バージョンでは 32 ビット アプリケーションとして、Windows の 64 ビット バージョンでは 64 ビット アプリケーションとして実行されます。

64 ビット アプリケーションを実行すると、ポインターのサイズが 2 倍になり、32 ビット専用のライブラリで互換性の問題が発生する可能性があります。 アプリケーションを 64 ビットで実行するのが合理的なのは、アプリケーションの実行速度が非常に速いか、4 GB を超えるメモリが必要な場合だけです。

このチェック ボックスは、次の条件がすべて満たされた場合にのみ利用できます。

- **[コンパイル]** ページで、 **[ターゲット CPU]** リストが **[任意の CPU]** に設定されている。

- **[アプリケーション]** ページの **[アプリケーションの種類]** リストで、プロジェクトがアプリケーションであることが指定されている。

- **[アプリケーション]** ページの **[ターゲット フレームワーク]** ボックスの一覧で、.NET Framework 4.5 が指定されている。

**警告の構成**

この表には、ビルドの条件とそれぞれに対応する通知レベル ( **[なし]** 、 **[警告]** 、または **[エラー]** ) が一覧表示されます。

既定では、コンパイル時のすべてのコンパイラ警告が、[タスク一覧] に追加されます。 **[すべての警告を表示しない]** を選択し、警告またはエラーを発行しないようにコンパイラに指示します。 コンパイラが警告を修正する必要があるエラーとして扱うにする場合は、 **[すべての警告をエラーとして扱う]** を選択します。

**すべての警告を表示しない**

このドキュメントで既に説明した、**条件と通知**テーブルで指定されているとおりにコンパイラに通知の発行を許可するかどうかを指定します。 既定では、このチェック ボックスはオフになっています。 警告またはエラーを発行しないようにコンパイラに指示するには、このチェック ボックスを選択します。

この設定は、[/nowarn](/dotnet/visual-basic/reference/command-line-compiler/nowarn) コンパイラ オプションに相当します。

**すべての警告をエラーとして扱う**

警告の処理方法を指定します。 既定では、このチェック ボックスはオフになっているため、すべての警告通知が **[警告]** に設定されたままになっています。 すべての警告通知を **[エラー]** に変更するには、このチェック ボックスをオンにします。

このオプションは、 **[すべての警告を表示しない]** がオフになっている場合にのみ使用できます。

**XML ドキュメント ファイルを生成する**

ドキュメント情報を生成するかどうかを指定します。 既定では、このチェック ボックスはオンになっており、ドキュメント情報を生成してそれを XML ファイルに含めるようにコンパイラに指示します。 ドキュメントを作成しないようにコンパイラに指示するには、このチェック ボックスをオフにします。

この設定は、[/doc](/dotnet/visual-basic/reference/command-line-compiler/doc) コンパイラ オプションに相当します。

**COM の相互運用機能に登録**

マネージド アプリケーションで、COM オブジェクトがアプリケーションとやり取りできるようにする COM オブジェクト (COM 呼び出し可能ラッパー) を公開するかどうかを指定します。

既定では、このチェック ボックスはオフになっており、アプリケーションで COM 相互運用を許可しないことを指定します。 COM 相互運用を許可するには、このチェック ボックスを選択します。

このオプションは、Windows アプリケーション、またはコンソール アプリケーション プロジェクトでは使用できません。

**ビルド イベント**

このボタンをクリックして **[ビルド イベント]** ダイアログ ボックスにアクセスします。 このダイアログ ボックスを使用して、プロジェクトのビルド前およびビルド後の構成手順を指定します。 このダイアログ ボックスは、Visual Basic プロジェクトにのみ適用されます。 詳細については、「[[ビルド イベント] ダイアログ ボックス (Visual Basic)](../../ide/reference/build-events-dialog-box-visual-basic.md)」を参照してください。

**詳細コンパイル オプション**

このボタンをクリックして、 **[コンパイラの詳細設定]** ダイアログ ボックスにアクセスします。 **[コンパイラの詳細設定]** ダイアログ ボックスを使用して、プロジェクトの詳細なビルド構成プロパティを指定します。 このダイアログ ボックスは、Visual Basic プロジェクトにのみ適用されます。 詳細については、「[[ビルドの詳細設定] ダイアログ ボックス (Visual Basic)](../../ide/reference/advanced-compiler-settings-dialog-box-visual-basic.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [方法: ビルド イベントを指定する (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)
- [Visual Basic のコマンド ライン コンパイラ](/dotnet/visual-basic/reference/command-line-compiler/index)
- [方法: 構成を作成および編集する](../../ide/how-to-create-and-edit-configurations.md)
