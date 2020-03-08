---
title: DLL プロジェクトのデバッグ |Microsoft Docs
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
ms.sourcegitcommit: 3154387056160bf4c36ac8717a7fdc0cd9faf3f9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78409382"
---
# <a name="debug-dlls-in-visual-studio-c-c-visual-basic-f"></a>Visual Studio でのデバッグ dllC#( C++、、Visual Basic F#、)

DLL (ダイナミックリンクライブラリ) は、複数のアプリで使用できるコードとデータが含まれているライブラリです。 Visual Studio を使用して、Dll の作成、ビルド、構成、デバッグを行うことができます。

## <a name="create-a-dll"></a>DLL を作成する

次の Visual Studio プロジェクトテンプレートでは、Dll を作成できます。

- C#、Visual Basic、またF#はクラスライブラリ
- C#または Visual Basic Windows フォーム Control (WCF) ライブラリ
- C++ダイナミックリンクライブラリ (DLL)

詳細については、「[MFC のデバッグ技術](../debugger/mfc-debugging-techniques.md)」を参照してください。

WCF ライブラリのデバッグは、クラスライブラリのデバッグに似ています。 詳細については、「 [Windows フォームコントロール](/dotnet/framework/winforms/controls/index)」を参照してください。

通常は、別のプロジェクトから DLL を呼び出します。 呼び出し元のプロジェクトをデバッグするときに、DLL の構成によっては、DLL コードにステップインしてデバッグすることができます。

## <a name="vxtskdebuggingdllprojectschangingdefaultconfigurations"></a>DLL デバッグ構成

Visual Studio プロジェクトテンプレートを使用してアプリを作成すると、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] によって、デバッグビルド構成およびリリースビルド構成に必要な設定が自動的に作成されます。 必要に応じて、これらの設定を変更できます。 詳細については、次の記事を参照してください。

- [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)
- [C# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)
- [Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [方法: デバッグ構成とリリース構成を設定する](../debugger/how-to-set-debug-and-release-configurations.md)

### <a name="set-c-debuggableattribute"></a>DebuggableAttribute C++の設定

デバッガーがC++ DLL にアタッチされるようにするC++には、コードで `DebuggableAttribute`を生成する必要があります。

**`DebuggableAttribute`を設定するには:**

1. ソリューションエクスプローラーでC++ DLL プロジェクトを選択し、 **[プロパティ]** アイコンを選択するか、プロジェクトを右クリックして **[プロパティ]** を選択します。

1. **[プロパティ]** ペインの [**リンカー** > **デバッグ**] で、デバッグ可能な **[アセンブリ]** に [**はい] (/assemblydebug)** を選択します。

詳細については、「 [/assemblydebug](/cpp/build/reference/assemblydebug-add-debuggableattribute)」を参照してください。

### <a name="vxtskdebuggingdllprojectsexternal"></a>C/C++ DLL ファイルの場所を設定する

外部 DLL をデバッグするには、呼び出し元のプロジェクトが DLL、 [.pdb ファイル](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)、および dll に必要なその他のファイルを検索できる必要があります。 カスタムビルドタスクを作成して、これらのファイルを *\<のプロジェクトフォルダー > \Debug*出力フォルダーにコピーしたり、ファイルを手動でコピーしたりすることができます。

C/C++プロジェクトの場合は、出力フォルダーにコピーするのではなく、プロジェクトのプロパティページでヘッダーと LIB のファイルの場所を設定できます。

**C/C++ヘッダーおよび LIB ファイルの場所を設定するには:**

1. ソリューションエクスプローラーで C/C++ DLL プロジェクトを選択し、 **[プロパティ]** アイコンを選択するか、プロジェクトを右クリックして **[プロパティ]** を選択します。

1. **プロパティ**ペインの上部にある **[構成]** で、 **[すべての構成]** を選択します。

1. [ **C/C++**  > **全般** > **追加のインクルードディレクトリ**] の下で、ヘッダーファイルを含むフォルダーを指定します。

1. **リンカー** > **全般** > **追加ライブラリディレクトリ** の下で、LIB ファイルがあるフォルダーを指定します。

1. **リンカー** > 追加の**依存関係**を**入力** > には、LIB ファイルの完全なパスとファイル名を指定します。

1. **[OK]** を選択します。

C++プロジェクト設定の詳細については、「 [Windows C++プロパティページリファレンス](/cpp/build/reference/property-pages-visual-cpp)」を参照してください。

## <a name="vxtskdebuggingdllprojectsbuildingadebugversion"></a>デバッグバージョンのビルド

デバッグを開始する前に、必ず DLL のデバッグバージョンをビルドしてください。 DLL をデバッグするには、呼び出し元のアプリがその[.pdb ファイル](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)と dll に必要なその他のファイルを見つけることができる必要があります。

カスタムビルドタスクを作成し、DLL ファイルを *\<呼び出し元のプロジェクトフォルダー > \Debug*出力フォルダーにコピーしたり、ファイルを手動でコピーしたりすることができます。

必ず正しい場所に DLL を呼び出してください。 これは明らかに見えるかもしれませんが、呼び出し元のアプリが DLL の別のコピーを検出して読み込む場合、設定したブレークポイントにデバッガーがヒットすることはありません。

## <a name="vxtskdebuggingdllprojectswaystodebugthedll"></a>DLL のデバッグ

DLL を直接実行することはできません。 これは、アプリ (通常は *.exe*ファイル) から呼び出す必要があります。 詳細については、「 [Visual Studio C++プロジェクト- ](/cpp/ide/creating-and-managing-visual-cpp-projects)」を参照してください。

DLL をデバッグするには、[呼び出し元のアプリからデバッグを開始](#vxtskdebuggingdllprojectsthecallingapplication)するか、呼び出し元のアプリを指定して[dll プロジェクトからデバッグ](how-to-debug-from-a-dll-project.md)することができます。 デバッガーの [[イミディエイト] ウィンドウ](#vxtskdebuggingdllprojectstheimmediatewindow)を使用して、呼び出し元のアプリを使用せずに、デザイン時に DLL の関数やメソッドを評価することもできます。

詳細については、「[デバッガーの最初の確認](../debugger/debugger-feature-tour.md)」を参照してください。

### <a name="vxtskdebuggingdllprojectsthecallingapplication"></a>呼び出し元アプリからデバッグを開始する

DLL を呼び出すアプリは次のようになります。

- DLL と同じまたは別のソリューション内の [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロジェクトのアプリ。
- テストコンピューターまたは実稼働コンピューターで既に配置され、実行されている既存のアプリ。
- Web に配置され、URL からアクセスするアプリケーション。
- DLL を埋め込む web ページを含む web アプリ。

呼び出し元アプリから DLL をデバッグするには、次のようにします。

- 呼び出し元のアプリのプロジェクトを開き、[デバッグ > デバッグの**開始**] を選択するか、 **F5**キーを押し**てデバッグを**開始します。

  or

- テストコンピューターまたは実稼働コンピューターで既に展開され、実行されているアプリにアタッチします。 このメソッドは、web サイトまたは web アプリの Dll に対して使用します。 詳細については、「[方法: 実行中のプロセスにアタッチする](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)」を参照してください。

呼び出し元のアプリのデバッグを開始する前に、DLL にブレークポイントを設定します。 「[ブレークポイントの使用」を](../debugger/using-breakpoints.md)参照してください。 DLL のブレークポイントにヒットしたら、コードをステップ実行して、各行でアクションを観察できます。 詳細については、「[デバッガーでのコード間の移動](../debugger/navigating-through-code-with-the-debugger.md)」を参照してください。

デバッグ中に、 **[モジュール]** ウィンドウを使用して、アプリが読み込む dll ファイルと *.exe*ファイルを確認できます。 **[モジュール]** ウィンドウを開くには、デバッグ中に [**デバッグ** > **Windows** > **モジュール**] を選択します。 詳細については、「[方法: [モジュール] ウィンドウを使用する](../debugger/how-to-use-the-modules-window.md)」を参照してください。

### <a name="vxtskdebuggingdllprojectstheimmediatewindow"></a>[イミディエイト] ウィンドウを使用する

**イミディエイト**ウィンドウを使用すると、デザイン時に DLL の関数やメソッドを評価できます。 **[イミディエイト]** ウィンドウは、呼び出し元のアプリの役割を果たします。

>[!NOTE]
>ほとんどのプロジェクトの種類では、デザイン時に **[イミディエイト]** ウィンドウを使用できます。 SQL、web プロジェクト、またはスクリプトではサポートされていません。

たとえば、クラス `Class1`で `Test` という名前のメソッドをテストするには、次のようにします。

1. DLL プロジェクトを開いた状態で、[**デバッグ** > **Windows** > **イミディエイト**] を選択するか **、Ctrl**+**Alt**+**I**キーを押して、**イミディエイト**ウィンドウを開きます。

1. [ C# **イミディエイト**] ウィンドウに次のコードを入力し、 **enter**キーを押して `Class1` 型のオブジェクトをインスタンス化します。 このマネージコードは、 C#との Visual Basic に対して機能し、適切な構文を変更します。

   ```csharp
   Class1 obj = new Class1();
   ```

   C# では、すべての名前を完全修飾する必要があります。 言語サービスが式を評価しようとするときは、すべてのメソッドまたは変数が現在のスコープとコンテキストに含まれている必要があります。

1. `Test` が 1 つの `int` パラメーターを受け取るものと想定し、 `Test` [イミディエイト] **ウィンドウを使用して** を評価します。

   ```csharp
   ?obj.Test(10);
   ```

   結果は **[イミディエイト]** ウィンドウに出力されます。

1. `Test` の中にブレークポイントを配置し、関数を再び評価してデバッグを継続できます。

   ブレークポイントにヒットし、`Test`をステップ実行できます。 `Test` の実行が終了すると、デバッガーはデザイン モードに戻ります。

## <a name="vxtskdebuggingdllprojectsmixedmodedebugging"></a> 混合モードのデバッグ

DLL の呼び出し元アプリをマネージコードまたはネイティブコードで記述できます。 ネイティブアプリがマネージ DLL を呼び出し、両方をデバッグする場合は、プロジェクトのプロパティでマネージデバッガーとネイティブデバッガーの両方を有効にすることができます。 正確なプロセスは、DLL プロジェクトからデバッグを開始するか、呼び出し元のアプリプロジェクトからデバッグを開始するかによって異なります。 詳細については、「[方法: 混合モードでデバッグする](../debugger/how-to-debug-in-mixed-mode.md)」を参照してください。

マネージ呼び出しプロジェクトからネイティブ DLL をデバッグすることもできます。 詳細については、「[マネージコードとネイティブコードをデバッグする方法](how-to-debug-managed-and-native-code.md)」を参照してください。

## <a name="see-also"></a>参照
- [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
- [プロジェクトのデバッグC++の準備](../debugger/debugging-preparation-visual-cpp-project-types.md)
- [C#、F#、Visual Basic プロジェクト タイプ](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)
- [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)
- [C# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)
- [Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
