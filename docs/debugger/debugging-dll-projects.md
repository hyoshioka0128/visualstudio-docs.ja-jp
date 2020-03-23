---
title: DLL プロジェクトをデバッグする |マイクロソフトドキュメント
ms.date: 11/06/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging DLLs
- templates, debugging DLLs
- DLLs, debugging
- debugging [Visual Studio], DLLs
ms.assetid: 433cab30-d191-460b-96f7-90d2530ca243
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 898eb0eb1489d83e97ec9f0a5b38b475bda0199d
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301165"
---
# <a name="debug-dlls-in-visual-studio-c-c-visual-basic-f"></a>Dll をデバッグする (C#、C++、ビジュアル ベーシック、F#)

DLL (ダイナミック リンク ライブラリ) は、コードとデータを含むライブラリで、複数のアプリで使用できます。 Visual Studio を使用して、DLL の作成、ビルド、構成、およびデバッグを行うことができます。

## <a name="create-a-dll"></a>DLL を作成する

次の Visual Studio プロジェクト テンプレートは、DLL を作成できます。

- C# 、ビジュアル ベーシック、または F# クラス ライブラリ
- C# または Visual Basic Windows フォーム コントロール (WCF) ライブラリ
- C++ ダイナミック リンク ライブラリ (DLL)

詳細については、「 [MFC デバッグのテクニック](../debugger/mfc-debugging-techniques.md)」を参照してください。

WCF ライブラリのデバッグは、クラス ライブラリのデバッグと似ています。 詳細については、「 [Windows フォーム コントロール](/dotnet/framework/winforms/controls/index)」を参照してください。

通常は、別のプロジェクトから DLL を呼び出します。 呼び出し元のプロジェクトをデバッグする場合は、DLL の構成に応じて、DLL コードにステップ インしてデバッグできます。

## <a name="dll-debug-configuration"></a><a name="vxtskdebuggingdllprojectschangingdefaultconfigurations"></a>DLL デバッグ構成

Visual Studio プロジェクト テンプレートを使用してアプリを作成[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]すると、デバッグビルド構成とリリース ビルド構成に必要な設定が自動的に作成されます。 これらの設定は、必要に応じて変更できます。 詳細については、次の記事を参照してください。

- [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)
- [C# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)
- [Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [方法 : デバッグ構成とリリース構成を設定する](../debugger/how-to-set-debug-and-release-configurations.md)

### <a name="set-c-debuggableattribute"></a>C++ デバッグ可能属性の設定

デバッガーが C++ DLL にアタッチするには、C++ コードが出力`DebuggableAttribute`する必要があります。

**設定`DebuggableAttribute`するには:**

1. **ソリューション エクスプローラ**で C++ DLL プロジェクトを選択し、[**プロパティ]** アイコンを選択するか、プロジェクトを右クリックして **[プロパティ]** を選択します。

1. [**プロパティ]** ペインの [**リンカー** > **のデバッグ**] で、[**デバッグ可能なアセンブリ**] で [**はい ] を**選択します。

詳細については[、/ASSEMBLYDEBUG](/cpp/build/reference/assemblydebug-add-debuggableattribute)を参照してください。

### <a name="set-cc-dll-file-locations"></a><a name="vxtskdebuggingdllprojectsexternal"></a>C/C++ DLL ファイルの場所を設定する

外部 DLL をデバッグするには、呼び出し元のプロジェクトで、DLL、その[.pdb ファイル](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)、およびその DLL に必要なその他のファイルを見つけなければなりません。 これらのファイルを*\<プロジェクト フォルダー>\Debug*出力フォルダーにコピーするカスタム ビルド タスクを作成するか、またはファイルを手動でコピーできます。

C/C++ プロジェクトの場合、ヘッダーファイルと LIB ファイルの場所を出力フォルダーにコピーする代わりに、プロジェクトのプロパティページで設定できます。

**C/C++ ヘッダーと LIB ファイルの場所を設定するには、次の手順を実行します。**

1. **ソリューション エクスプローラ**で C/C++ DLL プロジェクトを選択し、[**プロパティ]** アイコンを選択するか、プロジェクトを右クリックして **[プロパティ]** を選択します。

1. **[プロパティ]** ウィンドウの上部にある **[構成**] で、[**すべての構成**] を選択します。

1. **[C/C++** > **全般** > **追加インクルード ディレクトリ]** で、ヘッダー ファイルを含むフォルダを指定します。

1. [**リンカー** > **の一般** > **追加ライブラリ ディレクトリ] で**、LIB ファイルを含むフォルダを指定します。

1. [**リンカー** > **入力** > **追加の依存関係**] で、LIB ファイルの完全なパスとファイル名を指定します。

1. **[OK]** を選択します。

C++ プロジェクト設定の詳細については、「 [Windows C++ プロパティ ページ リファレンス](/cpp/build/reference/property-pages-visual-cpp)」を参照してください。

## <a name="build-a-debug-version"></a><a name="vxtskdebuggingdllprojectsbuildingadebugversion"></a>デバッグ バージョンをビルドする

デバッグを開始する前に、必ず DLL のデバッグ バージョンをビルドしてください。 DLL をデバッグするには、呼び出し元のアプリが[.pdb ファイル](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)と、DLL が必要とするその他のファイルを見つけなければなりません。

DLL ファイルを*\<呼び出し元のプロジェクト フォルダー>\Debug*出力フォルダーにコピーするカスタム ビルド タスクを作成するか、ファイルを手動でコピーできます。

DLL を正しい場所で呼び出してください。 これは明らかなように思えるかもしれませんが、呼び出し元のアプリが DLL の別のコピーを見つけて読み込んだ場合、デバッガーは設定したブレークポイントにヒットしません。

## <a name="debug-a-dll"></a><a name="vxtskdebuggingdllprojectswaystodebugthedll"></a>DLL をデバッグする

DLL を直接実行することはできません。 これは、通常は *.exe*ファイルであるアプリによって呼び出される必要があります。 詳細については、「 [Visual Studio プロジェクト - C++](/cpp/ide/creating-and-managing-visual-cpp-projects)」を参照してください。

DLL をデバッグするには、[呼び出し元のアプリからデバッグを開始するか、呼び出し元のアプリ](#vxtskdebuggingdllprojectsthecallingapplication)を指定して[DLL プロジェクトからデバッグ](how-to-debug-from-a-dll-project.md)を開始します。 デバッガー[の [イミディエイト] ウィンドウ](#vxtskdebuggingdllprojectstheimmediatewindow)を使用して、呼び出し元のアプリを使用せずに、デザイン時に DLL 関数またはメソッドを評価することもできます。

詳細については、「[最初にデバッガーを参照](../debugger/debugger-feature-tour.md)してください 。

### <a name="start-debugging-from-the-calling-app"></a><a name="vxtskdebuggingdllprojectsthecallingapplication"></a>呼び出し元アプリからデバッグを開始する

DLL を呼び出すアプリは、次のようになります。

- DLL と同[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]じソリューションまたは異なるソリューション内のプロジェクトからのアプリ。
- 既に展開され、テスト コンピューターまたは実稼働コンピューターで実行されている既存のアプリ。
- Web に配置され、URL からアクセスするアプリケーション。
- DLL を埋め込む Web ページを含む Web アプリ。

呼び出し元のアプリから DLL をデバッグするには、次の方法があります。

- 呼び出し元のアプリのプロジェクトを開き、[**Debug** > **デバッグ開始デバッグ**] を選択するか **、F5**キーを押してデバッグを開始します。

  or

- 既に展開され、テスト コンピューターまたは運用コンピューターで実行されているアプリにアタッチします。 このメソッドは、Web サイトまたは Web アプリの DLL に使用します。 詳細については、「[方法 : 実行中のプロセスにアタッチする](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)」を参照してください。

呼び出し元のアプリのデバッグを開始する前に、DLL にブレークポイントを設定します。 [ブレークポイントの使用を](../debugger/using-breakpoints.md)参照してください。 DLL ブレークポイントにヒットすると、コードをステップ実行して、各行のアクションを確認できます。 詳細については、「[デバッガーでのコードの移動](../debugger/navigating-through-code-with-the-debugger.md)」を参照してください。

デバッグ中に、[**モジュール**] ウィンドウを使用して、アプリが読み込む DLL と *.exe*ファイルを確認できます。 デバッグ中に **[モジュール**] ウィンドウを開くには **、[Windows** > モジュール**のデバッグ** > ] を**選択**します。 詳細については、「方法[: モジュール ウィンドウを使用する](../debugger/how-to-use-the-modules-window.md)」を参照してください。

### <a name="use-the-immediate-window"></a><a name="vxtskdebuggingdllprojectstheimmediatewindow"></a>イミディエイト ウィンドウを使用する

**[イミディエイト**] ウィンドウを使用すると、デザイン時に DLL 関数またはメソッドを評価できます。 **イミディエイト**ウィンドウは、呼び出し元のアプリの役割を果たします。

>[!NOTE]
>ほとんどのプロジェクトの種類では、デザイン時に **[イミディエイト**] ウィンドウを使用できます。 SQL、Web プロジェクト、またはスクリプトではサポートされていません。

たとえば、class`Test``Class1`で指定されたメソッドをテストするには、

1. DLL プロジェクトを開いた後 **、[Windows** > の**即時デバッグ** > ] を選択**するか、Ctrl**+**Alt I**+**キーを**押して **[イミディエイト]** ウィンドウを開きます。 **Immediate**

1. **イミディエイト**`Class1`ウィンドウに次の C# コードを入力し **、Enter**キーを押して、型のオブジェクトをインスタンス化します。 このマネージ コードは、C# と Visual Basic で適切な構文変更を行う場合に使用できます。

   ```csharp
   Class1 obj = new Class1();
   ```

   C# では、すべての名前を完全修飾する必要があります。 言語サービスが式を評価する際には、すべてのメソッドまたは変数が現在のスコープとコンテキストに含まれている必要があります。

1. `Test` が 1 つの `int` パラメーターを受け取るものと想定し、 `Test` [イミディエイト] **ウィンドウを使用して** を評価します。

   ```csharp
   ?obj.Test(10);
   ```

   結果は**イミディエイト**ウィンドウに表示されます。

1. `Test` の中にブレークポイントを配置し、関数を再び評価してデバッグを継続できます。

   ブレークポイントにヒットし、 をステップ実行`Test`できます。 `Test` の実行が終了すると、デバッガーはデザイン モードに戻ります。

## <a name="mixed-mode-debugging"></a><a name="vxtskdebuggingdllprojectsmixedmodedebugging"></a>混合モードデバッグ

マネージ コードまたはネイティブ コードで DLL の呼び出し元アプリを記述できます。 ネイティブ アプリがマネージ DLL を呼び出し、両方をデバッグする場合は、プロジェクトのプロパティでマネージ デバッガーとネイティブ デバッガーの両方を有効にできます。 正確なプロセスは、DLL プロジェクトからデバッグを開始するか、呼び出し元のアプリ プロジェクトからデバッグを開始するかによって異なります。 詳細については、「[方法 : 混在モードでデバッグする](../debugger/how-to-debug-in-mixed-mode.md)」を参照してください。

マネージ呼び出し元のプロジェクトからネイティブ DLL をデバッグすることもできます。 詳細については、「[マネージ コードとネイティブ コードをデバッグする方法](how-to-debug-managed-and-native-code.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
- [C++ プロジェクトのデバッグの準備](../debugger/debugging-preparation-visual-cpp-project-types.md)
- [C#、F#、Visual Basic プロジェクト タイプ](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)
- [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)
- [C# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)
- [Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
