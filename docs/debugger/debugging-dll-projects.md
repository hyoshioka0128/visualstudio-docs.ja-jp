---
title: DLL プロジェクトをデバッグする | Microsoft Docs
description: Visual Studio のダイナミックリンク ライブラリ (DLL) ファイルをデバッグします。 Visual Studio を使用し、DLL を作成、ビルド、構成、デバッグします。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b6ad51d6b791def360f12b2d64e4ef6841c7bcda
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99872795"
---
# <a name="debug-dlls-in-visual-studio-c-c-visual-basic-f"></a>Visual Studio で DLL をデバッグする (C#、C++、Visual Basic、F#)

DLL (ダイナミック リンク ライブラリ) は、複数のアプリで使用できるコードとデータが含まれているライブラリです。 Visual Studio を使用して、DLL の作成、ビルド、構成、デバッグを行うことができます。

## <a name="create-a-dll"></a>DLL を作成する

次の Visual Studio プロジェクト テンプレートでは、DLL を作成できます。

- C#、Visual Basic、または F# のクラス ライブラリ
- C# または Visual Basic の Windows フォーム コントロール (WCF) ライブラリ
- C++ のダイナミック リンク ライブラリ (DLL)

詳細については、「[MFC のデバッグ技術](../debugger/mfc-debugging-techniques.md)」を参照してください。

WCF ライブラリのデバッグは、クラス ライブラリのデバッグと似ています。 詳細については、「[Windows フォーム コントロール](/dotnet/framework/winforms/controls/index)」を参照してください。

通常は、別のプロジェクトから DLL を呼び出します。 呼び出し元のプロジェクトをデバッグするとき、DLL の構成によっては、DLL のコードにステップ インしてデバッグすることができます。

## <a name="dll-debug-configuration"></a><a name="vxtskdebuggingdllprojectschangingdefaultconfigurations"></a> DLL のデバッグ構成

Visual Studio のプロジェクト テンプレートを使用してアプリを作成すると、デバッグ ビルドとリリース ビルドの構成に必要な設定は、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] によって自動的に作成されます。 これらの設定は必要に応じて変更できます。 詳細については、次の記事を参照してください。

- [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)
- [C# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)
- [Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [方法: デバッグ構成とリリース構成を設定する](../debugger/how-to-set-debug-and-release-configurations.md)

### <a name="set-c-debuggableattribute"></a>C++ の DebuggableAttribute を設定する

C++ DLL にデバッガーをアタッチするには、C++ のコードで `DebuggableAttribute` を生成する必要があります。

**`DebuggableAttribute` を設定するには:**

1. **ソリューション エクスプローラー** で C++ DLL プロジェクトを選択し、 **[プロパティ]** アイコンを選択するか、プロジェクトを右クリックして **[プロパティ]** を選択します。

1. **[プロパティ]** ペインの **[リンカー]**  >  **[デバッグ]** で、 **[デバッグできるアセンブリ]** に対して **[はい (/ASSEMBLYDEBUG)]** を選択します。

詳細については、「[/ASSEMBLYDEBUG](/cpp/build/reference/assemblydebug-add-debuggableattribute)」を参照してください。

### <a name="set-cc-dll-file-locations"></a><a name="vxtskdebuggingdllprojectsexternal"></a> C/C++ DLL のファイルの場所を設定する

外部 DLL をデバッグするには、呼び出し元のプロジェクトで、DLL、その [.pdb ファイル](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)、および DLL で必要な他のファイルを見つけることができる必要があります。 カスタム ビルド タスクを作成して、これらのファイルを *\<project folder>\Debug* 出力フォルダーにコピーするか、ファイルを手動でここにコピーすることができます。

C/C++ プロジェクトの場合は、出力フォルダーにコピーするのではなく、プロジェクトのプロパティ ページでヘッダーと LIB ファイルの場所を設定できます。

**C/C++ のヘッダー ファイルと LIB ファイルの場所を設定するには:**

1. **ソリューション エクスプローラー** で C/C++ DLL プロジェクトを選択し、 **[プロパティ]** アイコンを選択するか、プロジェクトを右クリックして **[プロパティ]** を選択します。

1. **[プロパティ]** ペインの上部にある **[構成]** で、 **[すべての構成]** を選択します。

1. **[C/C++]**  >  **[全般]**  >  **[追加のインクルード ディレクトリ]** で、ヘッダー ファイルのフォルダーを指定します。

1. **[リンカー]**  >  **[全般]**  >  **[追加のライブラリ ディレクトリ]** で、LIB ファイルのフォルダーを指定します。

1. **[リンカー]**  >  **[入力]**  >  **[追加の依存ファイル ]** で、LIB ファイルの完全なパスとファイル名を指定します。

1. **[OK]** を選択します。

C++ プロジェクトの設定の詳細については、[Windows C++ のプロパティ ページのリファレンス](/cpp/build/reference/property-pages-visual-cpp)に関するページを参照してください。

## <a name="build-a-debug-version"></a><a name="vxtskdebuggingdllprojectsbuildingadebugversion"></a> デバッグ バージョンをビルドする

デバッグを始める前に、必ず DLL のデバッグ バージョンをビルドしてください。 DLL をデバッグするには、呼び出し元のアプリで、その [.pdb ファイル](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)および DLL で必要な他のファイルを見つけることができる必要があります。

カスタム ビルド タスクを作成して、DLL ファイルを *\<calling project folder>\Debug* 出力フォルダーにコピーするか、ファイルを手動でここにコピーすることができます。

正しい場所の DLL を呼び出していることを確認します。 これは明白なことのように見えるかもしれませんが、呼び出し元のアプリで DLL の別のコピーを検出して読み込んだ場合、設定したブレークポイントにデバッガーがヒットすることはありません。

## <a name="debug-a-dll"></a><a name="vxtskdebuggingdllprojectswaystodebugthedll"></a> DLL をデバッグする

DLL を直接実行することはできません。 アプリ (通常は *.exe* ファイル) で呼び出す必要があります。 詳細については、「[Visual Studio のプロジェクト - C++](/cpp/ide/creating-and-managing-visual-cpp-projects)」を参照してください。

DLL をデバッグするには、[呼び出し元のアプリからデバッグを開始する](#vxtskdebuggingdllprojectsthecallingapplication)か、呼び出し元のアプリを指定することにより [DLL プロジェクトからデバッグする](how-to-debug-from-a-dll-project.md)ことができます。 また、デバッガーの [[イミディエイト] ウィンドウ](#vxtskdebuggingdllprojectstheimmediatewindow)を使用して、呼び出し元アプリを使用せずに、デザイン時に DLL の関数やメソッドを評価することもできます。

詳細については、「[デバッガーでのはじめに](../debugger/debugger-feature-tour.md)」を参照してください。

### <a name="start-debugging-from-the-calling-app"></a><a name="vxtskdebuggingdllprojectsthecallingapplication"></a> 呼び出し元アプリからデバッグを開始する

DLL を呼び出すことができるアプリは次のとおりです。

- DLL と同じまたは別のソリューション内の [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロジェクトのアプリ。
- テスト コンピューターや運用コンピューターに既に配置されて実行されている既存のアプリ。
- Web に配置され、URL からアクセスするアプリケーション。
- DLL が埋め込まれている Web ページを含む Web アプリ。

呼び出し元アプリから DLL をデバッグするには、次のようにします。

- 呼び出し元アプリのプロジェクトを開き、 **[デバッグ]**  >  **[デバッグの開始]** を選択するか、**F5** キーを押して、デバッグを開始します。

  or

- テスト コンピューターまたは運用コンピューターに既に配置されて実行されている既存のアプリにアタッチします。 Web サイト上または Web アプリ内の DLL に対しては、この方法を使用します。 詳細については、[実行中のプロセスにアタッチする](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)

呼び出し元アプリのデバッグを始める前に、DLL 内にブレークポイントを設定します。 [ブレークポイントの使用](../debugger/using-breakpoints.md)に関するページを参照してください。 DLL のブレークポイントにヒットしたら、コードをステップ実行して、1 行ずつアクションを確認できます。 詳細については、[デバッガーでのコード間の移動](../debugger/navigating-through-code-with-the-debugger.md)に関するページを参照してください。

デバッグ中に、 **[モジュール]** ウィンドウを使用して、アプリで読み込まれる DLL と *.exe* ファイルを確認できます。 **[モジュール]** ウィンドウを開くには、デバッグ中に、 **[デバッグ]**  >  **[ウィンドウ]**  >  **[モジュール]** を選択します。 詳細については、[[モジュール] ウィンドウを使用する](../debugger/how-to-use-the-modules-window.md)」を参照してください。

### <a name="use-the-immediate-window"></a><a name="vxtskdebuggingdllprojectstheimmediatewindow"></a> [イミディエイト] ウィンドウを使用する

**[イミディエイト]** ウィンドウを使用すると、デザイン時に DLL の関数またはメソッドを評価できます。 **[イミディエイト]** ウィンドウは、呼び出し元アプリの役割を果たします。

>[!NOTE]
>ほとんどのプロジェクトの種類で、デザイン時に **[イミディエイト]** ウィンドウを使用できます。 SQL、Web プロジェクト、またはスクリプトではサポートされていません。

たとえば、`Class1` クラスの `Test` という名前のメソッドをテストするには、次のようにします。

1. DLL プロジェクトを開き、 **[デバッグ]**  >  **[ウィンドウ]**  >  **[イミディエイト]** を選択するか、**Ctrl** + **Alt** + **I** キーを押して、 **[イミディエイト]** ウィンドウを開きます。

1. 次の C# コードを **[イミディエイト]** ウィンドウに入力して **Enter** キーを押し、`Class1` 型のオブジェクトをインスタンス化します。 このマネージド コードは、構文を適切に変更することで C# と Visual Basic で動作します。

   ```csharp
   Class1 obj = new Class1();
   ```

   C# では、すべての名前を完全修飾する必要があります。 言語サービスによって式の評価が試みられる時点で、すべてのメソッドまたは変数が現在のスコープとコンテキストに含まれている必要があります。

1. `Test` が 1 つの `int` パラメーターを受け取るものと想定し、 `Test` [イミディエイト] **ウィンドウを使用して** を評価します。

   ```csharp
   ?obj.Test(10);
   ```

   結果が **[イミディエイト]** ウィンドウに出力されます。

1. `Test` の中にブレークポイントを配置し、関数を再び評価してデバッグを継続できます。

   ブレークポイントにヒットし、`Test` をステップ実行できます。 `Test` の実行が終了すると、デバッガーはデザイン モードに戻ります。

## <a name="mixed-mode-debugging"></a><a name="vxtskdebuggingdllprojectsmixedmodedebugging"></a> 混合モードのデバッグ

マネージド コードまたはネイティブ コードで、DLL の呼び出し元アプリを記述できます。 ネイティブ アプリでマネージド DLL が呼び出されていて、その両方をデバッグする場合は、プロジェクトのプロパティでマネージド デバッガーとネイティブ デバッガーの両方を有効にすることができます。 厳密なプロセスは、DLL プロジェクトまたは呼び出し元アプリのプロジェクトのどちらからデバッグを開始するかによって異なります。 詳細については、[混合モードでデバッグする](../debugger/how-to-debug-in-mixed-mode.md)

マネージド呼び出し元プロジェクトからネイティブ DLL をデバッグすることもできます。 詳細については、[マネージド コードとネイティブ コードをデバッグする方法](how-to-debug-managed-and-native-code.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目
- [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
- [C++ プロジェクトのデバッグの準備](../debugger/debugging-preparation-visual-cpp-project-types.md)
- [C#、F#、Visual Basic プロジェクト タイプ](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)
- [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)
- [C# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)
- [Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
