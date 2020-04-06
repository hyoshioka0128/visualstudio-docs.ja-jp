---
title: 'チュートリアル: C++ を使用して SDK を作成する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 36ea793b-3832-41a1-b906-69e680ad5e1d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 65643e65490eacb79eea4d76aa49ff10d6cccf66
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697628"
---
# <a name="walkthrough-create-an-sdk-using-c"></a>チュートリアル: C++ を使用して SDK を作成する
このチュートリアルでは、ネイティブ C++ 数学ライブラリ SDK を作成し、その SDK を Visual Studio 拡張機能 (VSIX) としてパッケージ化し、それを使用してアプリを作成する方法を示します。 このチュートリアルは、次の手順に分かれています。

- [ネイティブ ライブラリと Windows ランタイム ライブラリを作成するには](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createClassLibrary)

- [拡張プロジェクトを作成するには](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createVSIX)

- [クラス ライブラリを使用するサンプル アプリを作成するには](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createSample)

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="to-create-the-native-and-windows-runtime-libraries"></a><a name="createClassLibrary"></a>ネイティブ ライブラリと Windows ランタイム ライブラリを作成するには

1. メニュー バーで、[**ファイル] を** > クリックして **[新しい** > **プロジェクト**] をクリックします。

2. テンプレートの一覧で **、[Visual C++** > **Windows ユニバーサル**] を展開し **、DLL (Windows ユニバーサル アプリ)** テンプレートを選択します。 [**名前]** ボックスで`NativeMath`を指定し **、[OK] をクリックします**。

3. 次のコードに一致するように*NativeMath.h*を更新します。

     [!code-cpp[CreatingAnSDKUsingCpp#1](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_1.h)]

4. 次のコードに一致するように*NativeMath.cpp*を更新します。

     [!code-cpp[CreatingAnSDKUsingCpp#2](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_2.cpp)]

5. **ソリューション エクスプローラー**で、ソリューション **'NativeMath'** のショートカット メニューを開き、[**新しいプロジェクト**の**追加** > ] をクリックします。

6. テンプレートの一覧で **、[Visual C++]** を展開し **、[Windows ランタイム コンポーネント]** テンプレートを選択します。 [**名前]** ボックスで`NativeMathWRT`を指定し **、[OK] をクリックします**。

7. *Class1.h*を次のコードと一致するように更新します。

     [!code-cpp[CreatingAnSDKUsingCpp#3](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_3.h)]

8. *Class1.cpp*をこのコードと一致するように更新します。

     [!code-cpp[CreatingAnSDKUsingCpp#4](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_4.cpp)]

9. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

## <a name="to-create-the-nativemathvsix-extension-project"></a><a name="createVSIX"></a>拡張プロジェクトを作成するには

1. **ソリューション エクスプローラー**で、ソリューション **'NativeMath'** のショートカット メニューを開き、[**新しいプロジェクト**の**追加** > ] をクリックします。

2. テンプレートの一覧で **、[Visual C#** > **の機能拡張**] を展開し **、[VSIX プロジェクト**] を選択します。 [**名前]** ボックス**で、NativeMathVSIX**を指定し **、[OK]** ボタンをクリックします。

3. **ソリューション エクスプローラー**で **、source.extension.vsixmanifest**のショートカット メニューを開き、[**コードの表示**] をクリックします。

4. 既存の XML を置き換えるには、次の XML を使用します。

    [!code-xml[CreatingAnSDKUsingCpp#6](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_6.xml)]

5. **ソリューション エクスプローラー**で **、NativeMathVSIX**プロジェクトのショートカット メニューを開き、[**Add** > **新しい項目**の追加] をクリックします。

6. **Visual C# の項目**の一覧で、[**データ**] を展開し **、[XML ファイル**] を選択します。 [**名前]** ボックスで`SDKManifest.xml`を指定し **、[OK] をクリックします**。

7. この XML を使用して、ファイルの内容を置き換えます。

     [!code-xml[CreatingAnSDKUsingCpp#5](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_5.xml)]

8. **ソリューション エクスプローラー**の**NativeMathVSIX**プロジェクトの下に、次のフォルダー構造を作成します。

    ```xml
    \DesignTime
          \CommonConfiguration
                \Neutral
                      \Include
          \Debug
                \x86
    \Redist
          \Debug
                \x86
    \References
          \CommonConfiguration
                \Neutral
    ```

9. **ソリューション エクスプローラー**で、**ソリューション 'NativeMath'** のショートカット メニューを開き、[**エクスプローラーでフォルダーを開く**] をクリックします。

10. **ファイル エクスプローラー**で *、$SolutionRoot \\NativeMath\NativeMath.h*をコピーし、**ソリューション エクスプローラー**の**NativeMathVSIX**プロジェクトの下に *、$SolutionRoot$\NativeMathVSIX\DesignTime\共通構成\ニュートラル\\\インクルード*フォルダーに貼り付けます。

     *$SolutionRootを*コピーし *、$SolutionRoot$\NativeMathVSIX\デザインタイム\デバッグ\x86\\*フォルダーに貼り付けます。

     *$SolutionRoot\デバッグ\ネイティブ数学\ネイティブ数学.dll*をコピーし *、$SolutionRoot$\NativeMathVSIX\Redist\デバッグ\x86\\*フォルダーに貼り付けます。

     *$SolutionRoot\デバッグ\ネイティブ数学WRT\ネイティブMathWRT.dll*をコピーし *、$SolutionRoot$\NativeMathVSIX\Redist\デバッグ\x86*フォルダーに貼り付けます。
     *$SolutionRoot\デバッグ\ネイティブ数学WRT\ネイティブMathWRT.winmd*をコピーし *、$SolutionRoot$\NativeMathVSIX\参照\共通構成\ニュートラル*フォルダーに貼り付けます。

     *$SolutionRootを*コピーし *、$SolutionRoot$\NativeMathVSIX\参照\共通構成\ニュートラル*フォルダーに貼り付けます。

11. *$SolutionRoot\NativeMathVSIX\DesignTime\Debug\x86\\*フォルダーに *、NativeMathSDK.props*という名前のテキスト ファイルを作成し、その中に次の内容を貼り付けます。

    [!code-xml[CreatingAnSDKUsingCpp#7](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_7.xml)]

12. メニュー バーで、[**他のウィンドウ** > **のプロパティ ウィンドウ**を**表示** > ] (キーボード: **F4**キーを選択) を選択します。

13. **ソリューション エクスプローラー**で、**ネイティブ MathWRT.winmd**ファイルを選択します。 [**プロパティ]** ウィンドウで、[**ビルド アクション**] プロパティを **[コンテンツ]** に変更し **、[VSIX に含める**] プロパティを**True**に変更します。

     この手順を **、ネイティブ Math.h**ファイルに対して繰り返します。

     このプロセスを **、ネイティブMathWRT.pri**ファイルに対して繰り返します。

     このプロセスを **、ネイティブの Math.Lib**ファイルに対して繰り返します。

     このプロセスを **、ネイティブMathSDK.props**ファイルに対して繰り返します。

14. **ソリューション エクスプローラー**で **、NativeMath.h**ファイルを選択します。 [**プロパティ]** ウィンドウ**で、[VSIX に含める**] プロパティを **[True]** に変更します。

     このプロセスを**ネイティブMath.dll**ファイルに対して繰り返します。

     このプロセスを **、ネイティブMathWRT.dll**ファイルに対して繰り返します。

     このプロセスを**SDKManifest.xml**ファイルに対して繰り返します。

15. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

16. **ソリューション エクスプローラー**で **、NativeMathVSIX**プロジェクトのショートカット メニューを開き、[**エクスプローラーでフォルダーを開く**] をクリックします。

17. **エクスプローラー**で *、$SolutionRoot$\NativeMathVSIX\bin\Debug*フォルダーに移動し、次に*NativeMathVSIX.vsix*を実行してインストールを開始します。

18. [**インストール**] ボタンをクリックし、インストールが完了するのを待ってから、Visual Studio を開きます。

## <a name="to-create-a-sample-app-that-uses-the-class-library"></a><a name="createSample"></a>クラス ライブラリを使用するサンプル アプリを作成するには

1. メニュー バーで、[**ファイル] を** > クリックして **[新しい** > **プロジェクト**] をクリックします。

2. テンプレートの一覧で **、[Visual C++** > **Windows ユニバーサル**] を展開し、[**空のアプリケーション**] を選択します。 [**名前]** ボックス**で、NativeMathSDKSample**を指定し **、[OK]** ボタンをクリックします。

3. **ソリューション エクスプローラー**で **、NativeMathSDKSample**プロジェクトのショートカット メニューを開き、[**参照**の**追加** > ] をクリックします。

4. [**参照の追加**] ダイアログ ボックスの参照の種類の一覧で、[**ユニバーサル Windows]** を展開し、[**拡張機能**] を選択します。 最後に、[**ネイティブ数学 SDK]** チェック ボックスをオンにし **、[OK] ボタン**をクリックします。

5. プロジェクトプロパティを表示します。

    参照を追加したときに *、NativeMathSDK.props*で定義したプロパティが適用されました。 プロジェクトの **[構成**プロパティ] の **[VC++ ディレクトリ]** プロパティを調べることで、プロパティが適用されたことを確認できます。

6. **ソリューション エクスプローラー**で**MainPage.xaml**を開き、次の XAML を使用してコンテンツを置き換えます。

    [!code-xml[CreatingAnSDKUsingCppDemoApp#1](../extensibility/codesnippet/Xaml/walkthrough-creating-an-sdk-using-cpp_8.xaml)]

7. このコードに一致するように*Mainpage.xaml.h*を更新します。

    [!code-cpp[CreatingAnSDKUsingCppDemoApp#2](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_9.h)]

8. 次のコードに一致するように*MainPage.xaml.cpp*を更新します。

     [!code-cpp[CreatingAnSDKUsingCppDemoApp#3](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_10.cpp)]

9. **F5**キーを押してアプリを実行します。

10. アプリで、任意の 2 つの数値を入力し、操作を選択**=** して、ボタンを選択します。

     正しい結果が表示されます。

    このチュートリアルでは、ライブラリと非[!INCLUDE[wrt](../extensibility/includes/wrt_md.md)][!INCLUDE[wrt](../extensibility/includes/wrt_md.md)]ライブラリを呼び出すために、拡張 SDK を作成して使用する方法を示しました。

## <a name="next-steps"></a>次の手順

## <a name="see-also"></a>関連項目
- [チュートリアル: C# または Visual Basic を使用して SDK を作成する](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)
- [ソフトウェア開発キットの作成](../extensibility/creating-a-software-development-kit.md)
