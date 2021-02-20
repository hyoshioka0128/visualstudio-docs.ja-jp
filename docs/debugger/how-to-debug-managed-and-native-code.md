---
title: 'チュートリアル: C# と C++ コードをデバッグする (混在モード)'
description: 混合モードのデバッグを使用して .NET Core または .NET Framework のアプリからネイティブ DLL をデバッグする方法について学習します
ms.custom: seodec18
ms.date: 11/02/2018
ms.topic: tutorial
dev_langs:
- CSharp
- C++
helpviewer_keywords:
- mixed mode debugging
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
- cplusplus
ms.openlocfilehash: 4b1d250ed5306ce101fd7482b740ad57514e4f0a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99899418"
---
# <a name="tutorial-debug-c-and-c-in-the-same-debugging-session"></a>チュートリアル: 同じデバッグ セッションで C# と C++ をデバッグする

Visual Studio では、1 つのデバッグ セッションで複数のデバッガーの種類を有効にすることができます。これは混合モードのデバッグと呼ばれます。 このチュートリアルでは、1 つのデバッグ セッションで、マネージド コードとネイティブ コードの両方をデバッグすることを学習します。

このチュートリアルでは、マネージド アプリからネイティブ コードをデバッグする方法を示していますが、[ネイティブ アプリからマネージド コードをデバッグする](../debugger/how-to-debug-in-mixed-mode.md)こともできます。 デバッガーは、[Python とネイティブ コード](../python/debugging-mixed-mode-c-cpp-python-in-visual-studio.md)などの他の種類の混合モードのデバッグもサポートしており、ASP.NET などのアプリの種類ではスクリプト デバッガーの使用もサポートしています。

このチュートリアルでは、次の作業を行います。

> [!div class="checklist"]
> * 単純なネイティブ DLL を作成する
> * DLL を呼び出す単純な .NET Core または .NET Framework のアプリを作成する
> * 混合モードのデバッグを構成する
> * デバッガーを起動する
> * マネージド アプリでブレークポイントにヒットさせる
> * ネイティブ コードにステップ インする

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio がインストールされ、次のワークロードがある必要があります。
- **C++ によるデスクトップ開発**
- 作成するアプリの種類に応じて、 **.NET デスクトップ開発** または **.NET Core クロス プラットフォーム開発** のいずれか

Visual Studio をお持ちでない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads/) ページに移動し、無料試用版をインストールしてください。

Visual Studio はインストールされているが、必要なワークロードがない場合は、Visual Studio の **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウにある **[Visual Studio インストーラーを開く]** を選択します。 Visual Studio インストーラーで、必要なワークロードを選択し、 **[変更]** を選択します。

## <a name="create-a-simple-native-dll"></a>単純なネイティブ DLL を作成する

**DLL プロジェクト用のファイルを作成するには:**

1. Visual Studio を開き、プロジェクトを作成します。

    ::: moniker range=">=vs-2019"
    **Esc** キーを押してスタート ウィンドウを閉じます。 **Ctrl + Q** キーを押して検索ボックスを開き、「**空のプロジェクト**」と入力し、 **[テンプレート]** を選択してから、C++ 用の **[空のプロジェクト]** を選択します。 表示されたダイアログ ボックスで、 **[作成]** を選択します。 次に、**Mixed_Mode_Debugging** のような名前を入力して、 **[作成]** をクリックします。
    ::: moniker-end
    ::: moniker range="vs-2017"
    上部のメニュー バーから、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** の左側のウィンドウで、 **[Visual C++]** の下にある **[その他]** を選択し、次に、真ん中のウィンドウで **[空のプロジェクト]** を選択します。 次に、**Mixed_Mode_Debugging** のような名前を入力して、 **[OK]** をクリックします。
    ::: moniker-end

    **[空のプロジェクト]** プロジェクト テンプレートが表示されない場合は、 **[ツール]**  >  **[ツールと機能を取得...]** に移動して、Visual Studio インストーラーを開きます。 Visual Studio インストーラーが起動します。 **[C++ によるデスクトップ開発]** ワークロード、 **[変更]** の順に選択します。

    Visual Studio によってプロジェクトが作成されます。

1. **ソリューション エクスプローラー** で、 **[ソース ファイル]** を選択し、 **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。 または、 **[ソース ファイル]** を右クリックして、 **[追加]**  >  **[新しい項目]** の順に選択します。

1. **[新しい項目]** ダイアログで、 **[C++ ファイル (.cpp)]** を選択します。 **[名前]** フィールドに「**Mixed_Mode.cpp**」を入力し、 **[追加]** を選択します。

    Visual Studio によって新しい C++ ファイルが **ソリューション エクスプローラー** に追加されます。

1. *Mixed_Mode.cpp* に次のコードをコピーします。

    ```cpp
    #include "Mixed_Mode.h"
    ```

1. **ソリューション エクスプローラー** で、 **[ヘッダー ファイル]** を選択し、 **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。 または、 **[ヘッダー ファイル]** を右クリックして、 **[追加]**  >  **[新しい項目]** の順に選択します。

1. **[新しい項目]** ダイアログで、 **[ヘッダー ファイル (.h)]** を選択します。 **[名前]** フィールドに「**Mixed_Mode.h**」を入力し、 **[追加]** を選択します。

   Visual Studio によって新しいヘッダー ファイルが **ソリューション エクスプローラー** に追加されます。

1. *Mixed_Mode.h* に次のコードをコピーします。

    ```cpp
    #ifndef MIXED_MODE_MULTIPLY_HPP
    #define MIXED_MODE_MULTIPLY_HPP

    extern "C"
    {
      __declspec(dllexport) int __stdcall mixed_mode_multiply(int a, int b) {
        return a * b;
      }
    }
    #endif
    ```

1. **[ファイル]**  >  **[すべて保存]** を選択するか、**Ctrl**+**Shift**+**S** キーを押してファイルを保存します。

**DLL プロジェクトを構成してビルドするには:**

1. Visual Studio ツールバーで、 **[デバッグ]** 構成を選択し、 **[x86]** または **[x64]** プラットフォームを選択します。 呼び出し元のアプリが常に 64 ビット モードで実行される .NET Core の場合は、プラットフォームとして **[x64]** を選択します。

1. **ソリューション エクスプローラー** で、 **[Mixed_Mode_Debugging]** プロジェクト ノードを選択し、 **[プロパティ]** アイコンを選択するか、プロジェクト ノードを右クリックして **[プロパティ]** を選択します。

1. **[プロパティ]** ウィンドウの上部で、 **[構成]** が **[アクティブ (デバッグ)]** に設定され、 **[プラットフォーム]** がツールバーで設定したプラットフォームと同じになっていることを確認します ( **[x64]** 、または x86 プラットフォームの場合は **[Win32]** )。

   > [!IMPORTANT]
   > プラットフォームを **x86** から **x64** (またはその逆) に切り替えた場合、新しいプラットフォーム用にプロパティを再構成する必要があります。

1. 左側のウィンドウの **[構成プロパティ]** の下で、 **[リンカー]**  >  **[詳細設定]** の順に選択し、 **[エントリポイントなし]** の横のドロップダウンで **[いいえ]** を選択します。 **[いいえ]** に変更した場合は、 **[適用]** を選択します。

1. **[構成プロパティ]** の下で、 **[全般]** を選択し、 **[構成の種類]** の横にあるドロップダウンで **[ダイナミック ライブラリ (.dll)]** を選択します。 **[適用]** を選択し、 **[OK]** を選択します。

   ![ネイティブ DLL に切り替える](../debugger/media/mixed-mode-set-as-native-dll.png)

1. **ソリューション エクスプローラー** でプロジェクトを選択し、 **[ビルド]**  >  **[ソリューションのビルド]** の順に選択し、**F7** キーを押すか、プロジェクトを右クリックして **[ビルド]** を選択します。

   プロジェクトがエラーのない状態でビルドされます。

## <a name="create-a-simple-managed-app-to-call-the-dll"></a>単純なマネージド アプリを作成して DLL を呼び出す

1. Visual Studio を起動し、新しいプロジェクトを作成します。

    ::: moniker range=">=vs-2019"
    **Esc** キーを押してスタート ウィンドウを閉じます。 **Ctrl + Q** キーを押して検索ボックスを開き、「**コンソール**」と入力し、 **[テンプレート]** を選択して、C# 用の **[コンソール アプリ (.NET Core)]** または **[コンソール アプリ (.NET Framework)]** を選択します。 表示されたダイアログ ボックスで、 **[作成]** を選択します。

    次に、**Mixed_Mode_Calling_App** のような名前を入力して、 **[作成]** をクリックします。
    ::: moniker-end
    ::: moniker range="vs-2017"
    上部のメニュー バーから、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで、 **[Visual C#]** の下にある **[Windows デスクトップ]** を選択し、次に真ん中のウィンドウで **[コンソール アプリ (.NET Framework)]** または **[コンソール アプリ (.NET Core)]** を選択します。

    次に、**Mixed_Mode_Calling_App** のような名前を入力して、 **[OK]** をクリックします。
    ::: moniker-end

    **[コンソール アプリ]** プロジェクト テンプレートが表示されない場合は、 **[ツール]**  >  **[ツールと機能を取得...]** に移動して、Visual Studio インストーラーを開きます。 **.NET デスクトップ開発** ワークロードを選択し、 **[変更]** を選択します。

    > [!NOTE]
    > 新しいマネージド プロジェクトを既存の C++ ソリューションに追加することもできます。 混合モードのデバッグタスクがより難しくなるよう、新しいソリューションでプロジェクトを作成しています。

   Visual Studio によって空のプロジェクトが作成され、**ソリューション エクスプローラー** にファイルが表示されます。

1. *Program.cs* 内のすべてのコードを次のコードで置き換えます。

    ```csharp
    using System;
    using System.Runtime.InteropServices;

    namespace Mixed_Mode_Calling_App
    {
        public class Program
        {
            // Replace the file path shown here with the
            // file path on your computer. For .NET Core, the typical (default) path
            // for a 64-bit DLL might look like this:
            // C:\Users\username\source\repos\Mixed_Mode_Debugging\x64\Debug\Mixed_Mode_Debugging.dll
            // Here, we show a typical path for a DLL targeting the **x86** option.
            [DllImport(@"C:\Users\username\source\repos\Mixed_Mode_Debugging\Debug\Mixed_Mode_Debugging.dll", EntryPoint =
            "mixed_mode_multiply", CallingConvention = CallingConvention.StdCall)]
            public static extern int Multiply(int x, int y);
            public static void Main(string[] args)
            {
                int result = Multiply(7, 7);
                Console.WriteLine("The answer is {0}", result);
                Console.ReadKey();
            }
        }
    }
    ```

1. 新しいコードで、`[DllImport]` 内のファイル パスを先ほど作成した *Mixed_Mode_Debugging.dll* への実際のファイル パスに置き換えます。 ヒントとしてコード コメントを参照してください。 プレースホルダー *username* を必ず置き換えてください。

1. **[ファイル]**  >  **[Program.cs の保存]** を選択するか、**Ctrl**+**S** キーを押してファイルを保存します。

## <a name="configure-mixed-mode-debugging"></a>混合モードのデバッグを構成する

1. **ソリューション エクスプローラー** で、 **[Mixed_Mode_Calling_App]** プロジェクト ノードを選択し、 **[プロパティ]** アイコンを選択するか、プロジェクト ノードを右クリックして **[プロパティ]** を選択します。

1. 左側のウィンドウで **[デバッグ]** を選択し、 **[ネイティブ コードのデバッグを有効にする]** チェック ボックスをオンにしてから、プロパティ ページを閉じて変更を保存します。

    ![混合モード デバッグを有効にする](../debugger/media/mixed-mode-enable-native-code-debugging.png)

## <a name="set-a-breakpoint-and-start-debugging"></a>ブレークポイントを設定し、デバッグを開始する

1. C# プロジェクトで *Program.cs* を開きます。 コードの次の行にブレークポイントを設定するには、余白の左端をクリックして行を選択し、**F9** キーを押すか、行を右クリックして **[ブレークポイント]**  >  **[ブレークポイントの挿入]** の順に選択します。

    ```csharp
    int result = Multiply(7, 7);
    ```

    左側の余白のブレークポイントを設定した場所に赤い円が表示されます。

1. **F5** キーを押して、Visual Studio のツールバーで緑色の矢印を選択するか、 **[デバッグ]**  >  **[デバッグの開始]** の順に選択してデバッグを開始します。

   設定したブレークポイントのところでデバッガーが一時停止します。 黄色の矢印は、デバッガーが現在一時停止している場所を示します。

## <a name="step-in-and-out-of-native-code"></a>ネイティブ コードのステップ インとステップ アウト

1. マネージド アプリでデバッグが一時停止している間に、**F11** キーを押すか、 **[デバッグ]**  >  **[ステップ イン]** の順に選択します。

   *Mixed_Mode.h* ネイティブ ヘッダー ファイルが開き、デバッガーが一時停止されている場所に黄色の矢印が示されます。

   ![ネイティブ コードにステップ インする](../debugger/media/mixed-mode-step-into-native-code.png)

1. これで、ブレークポイントを設定してそこにヒットしたら、ネイティブ コードまたはマネージド コード内の変数を検査できます。

   - ソース コード内の変数をポイントすると、その値が表示されます。

   - 変数とその値は、 **[自動変数]** ウィンドウと **[ローカル]** ウィンドウで確認できます。

   - デバッガーで一時停止中に、**ウォッチ** ウィンドウと **[呼び出し履歴]** ウィンドウを使用することもできます。

1. もう一度 **F11** キーを押して、デバッガーを 1 行進めます。

1. **Shift**+**F11** キーを押すか、 **[デバッグ]**  >  **[ステップ アウト]** を選択して、マネージド アプリで実行を続行し、もう一度一時停止します。

1. **F5** キーを押すか、緑色の矢印を選択してアプリのデバッグを続行します。

おめでとうございます! 混合モードのデバッグのチュートリアルを完了しました。

## <a name="next-step"></a>次のステップ

このチュートリアルでは、混合モード デバッグを有効化して、マネージド アプリからネイティブ コードをデバッグする方法について学習しました。 その他のデバッガー機能の概要については、次を参照してください。

> [!div class="nextstepaction"]
> [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
