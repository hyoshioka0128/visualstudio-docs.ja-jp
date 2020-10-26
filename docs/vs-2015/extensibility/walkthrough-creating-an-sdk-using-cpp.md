---
title: 'チュートリアル: C++ を使用した SDK の作成 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 36ea793b-3832-41a1-b906-69e680ad5e1d
caps.latest.revision: 33
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1312d61b2d287a5dd8cb757b73e818a9e9cb2241
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202074"
---
# <a name="walkthrough-creating-an-sdk-using-c"></a>チュートリアル: C++ を使用して SDK を作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、ネイティブ C++ math library SDK を作成し、SDK を Visual Studio 拡張機能 (VSIX) としてパッケージ化して、それを使用してアプリを作成する方法について説明します。 このチュートリアルは、次の手順に分かれています。  
  
- [ネイティブライブラリと Windows ランタイムライブラリを作成するには](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createClassLibrary)  
  
- [Nativem、Vsix 拡張機能プロジェクトを作成するには](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createVSIX)  
  
- [クラスライブラリを使用するサンプルアプリを作成するには](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createSample)  
  
## <a name="prerequisites"></a>必須コンポーネント  
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)」を参照してください。  
  
## <a name="to-create-the-native-and-windows-runtime-libraries"></a><a name="createClassLibrary"></a> ネイティブライブラリと Windows ランタイムライブラリを作成するには  
  
1. メニュー バーで、 **[ファイル]** 、 **[新規作成]** 、 **[プロジェクト]** の順にクリックします。  
  
2. テンプレートの一覧で、[ **Visual C++**]、[ **windows ストア**] の順に展開し、[ **DLL (windows ストアアプリ)** ] テンプレートを選択します。 [ **名前** ] ボックスにを指定し、[ `NativeMath` **OK** ] をクリックします。  
  
3. 次のコードに一致するように NativeMath を更新します。  
  
     [!code-cpp[CreatingAnSDKUsingCpp#1](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemath/nativemath.h#1)]  
  
4. 次のコードに一致するように NativeMath を更新します。  
  
     [!code-cpp[CreatingAnSDKUsingCpp#2](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemath/nativemath.cpp#2)]  
  
5. **ソリューションエクスプローラー**で、**ソリューション ' NativeMath '** のショートカットメニューを開き、[**追加**]、[**新しいプロジェクト**] の順に選択します。  
  
6. テンプレートの一覧で [ **Visual C++**] を展開し、[ **Windows ランタイムコンポーネント** ] テンプレートを選択します。 [ **名前** ] ボックスにを指定し、[ `NativeMathWRT` **OK** ] をクリックします。  
  
7. 次のコードに一致するように Class1 を更新します。  
  
     [!code-cpp[CreatingAnSDKUsingCpp#3](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemathwrt/class1.h#3)]  
  
8. 次のコードに一致するように Class1 を更新します。  
  
     [!code-cpp[CreatingAnSDKUsingCpp#4](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemathwrt/class1.cpp#4)]  
  
9. メニュー バーの **[ビルド]**、 **[ソリューションのビルド]** の順にクリックします。  
  
## <a name="to-create-the-nativemathvsix-extension-project"></a><a name="createVSIX"></a> Nativem、Vsix 拡張機能プロジェクトを作成するには  
  
1. **ソリューションエクスプローラー**で、**ソリューション ' NativeMath '** のショートカットメニューを開き、[**追加**]、[**新しいプロジェクト**] の順に選択します。  
  
2. テンプレートの一覧で、[ **Visual C#**]、[ **機能拡張**] の順に展開し、[ **VSIX パッケージ**] を選択します。 [ **名前** ] ボックスに「 **Nativemthe vsix**」と入力し、[ **OK** ] をクリックします。  
  
3. VSIX マニフェストデザイナーが表示されたら、それを閉じます。  
  
4. **ソリューションエクスプローラー**で、 **source.extension.vsixmanifest**のショートカットメニューを開き、[**コードの表示**] を選択します。  
  
5. 次の XML を使用して、既存の XML を置き換えます。  
  
    [!code-xml[CreatingAnSDKUsingCpp#6](../../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_6.xml)]
  
6. **ソリューションエクスプローラー**で、 **Nativem、vsix**プロジェクトのショートカットメニューを開き、[**追加**]、[**新しい項目**] の順に選択します。  
  
7. **Visual C# の項目**の一覧で、[**データ**] を展開し、[ **XML ファイル**] を選択します。 [ **名前** ] ボックスにを指定し、[ `SDKManifest.xml` **OK** ] をクリックします。  
  
8. ファイルの内容を置き換えるには、次の XML を使用します。  
  
     [!code-xml[CreatingAnSDKUsingCpp#5](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemathvsix/sdkmanifest.xml#5)]  
  
9. **ソリューションエクスプローラー**の [ **Nativem] vsix**プロジェクトで、次のフォルダー構造を作成します。  
  
    ```  
  
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
  
10. **ソリューションエクスプローラー**で、**ソリューション ' NativeMath '** のショートカットメニューを開き、[**エクスプローラーでフォルダーを開く**] を選択します。  
  
11. **ファイルエクスプローラー**で \NativeMath\NativeMath.h をコピーし、**ソリューションエクスプローラー**の [ **nativem vsix** ] プロジェクトで、\DesignTime\CommonConfiguration\Neutral\Include\ フォルダーに貼り付けます。  
  
     \Debug\NativeMath\NativeMath.lib をコピーし、\DesignTime\Debug\x86\ フォルダーに貼り付けます。  
  
     \Debug\NativeMath\NativeMath.dll コピーして、\Redist\Debug\x86\ フォルダーに貼り付けます。  
  
     DebugNativeMathWRTNativeMathWRT.dll コピーして、RedistDebugx86 フォルダーに貼り付けます。  
  
     DebugNativeMathWRTNativeMathWRT をコピーし、[Commonconfigurationnd] フォルダーに貼り付けます。  
  
     DebugNativeMathWRTNativeMathWRT をコピーし、[Commonconfigurationnd] フォルダーに貼り付けます。  
  
12. \DesignTime\Debug\x86\ フォルダーで、Nativem という名前のテキストファイルを作成し、次の内容を貼り付けます。  
  
    [!code-xml[CreatingAnSDKUsingCpp#7](../../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_7.xml)]  
  
13. メニューバーで、[ **表示**]、[ **その他のウィンドウ**]、[ **プロパティウィンドウ** ] の順に選択します (キーボード: F4 キーを押します)。  
  
14. **ソリューションエクスプローラー**で、 **NativeMathWRT**ファイルを選択します。 [ **プロパティ** ] ウィンドウで、" **ビルドアクション** " プロパティを " **コンテンツ**" に変更し、[ **VSIX に含める** ] プロパティを [ **True**] に変更します。  
  
     **SimpleMath**ファイルに対してこのプロセスを繰り返します。  
  
     **NativeMath**ファイルに対してこのプロセスを繰り返します。  
  
     このプロセスを **Nativemthe** のプロパティのプロパティに対して繰り返します。  
  
15. **ソリューションエクスプローラー**で、 **NativeMath**ファイルを選択します。 [ **プロパティ** ] ウィンドウで、[ **VSIX に含める** ] プロパティを [ **True**] に変更します。  
  
     **NativeMath.dll**ファイルに対してこの手順を繰り返します。  
  
     **NativeMathWRT.dll**ファイルに対してこの手順を繰り返します。  
  
     **SDKManifest.xml**ファイルに対してこの手順を繰り返します。  
  
16. メニュー バーの **[ビルド]**、 **[ソリューションのビルド]** の順にクリックします。  
  
17. **ソリューションエクスプローラー**で、 **Nativem、vsix**プロジェクトのショートカットメニューを開き、[**エクスプローラーでフォルダーを開く**] を選択します。  
  
18. **エクスプローラー**で、\bin\Debug\ フォルダーに移動し、次に、nativem を実行してインストールを開始します。  
  
19. [ **インストール** ] ボタンをクリックし、インストールが完了するのを待ってから、Visual Studio を再起動します。  
  
## <a name="to-create-a-sample-app-that-uses-the-class-library"></a><a name="createSample"></a> クラスライブラリを使用するサンプルアプリを作成するには  
  
1. メニュー バーで、 **[ファイル]** 、 **[新規作成]** 、 **[プロジェクト]** の順にクリックします。  
  
2. テンプレートの一覧で、[ **Visual C++**]、[ **Windows ストア**] の順に展開し、[ **空のアプリ**] を選択します。 [ **名前** ] ボックスに **NativeMathSDKSample**を指定し、[ **OK** ] をクリックします。  
  
3. **ソリューションエクスプローラー**で、 **NativeMathSDKSample**プロジェクトのショートカットメニューを開き、[**追加**]、[**参照**] の順に選択します。  
  
4. [ **共通プロパティ**] の **[フレームワークと参照** ] プロパティページで、参照型の一覧から [ **Windows**] を展開し、[ **拡張機能**] を選択します。 詳細ペインで、 **ネイティブの MATH SDK** 拡張機能を選択し、[ **新しい参照の追加** ] をクリックします。  
  
5. [ **参照の追加** ] ダイアログボックスで、[ **ネイティブ Math SDK** ] チェックボックスをオンにし、[ **OK** ] をクリックします。  
  
6. NativeMathSDKSample のプロジェクトプロパティを表示します。  
  
    参照を追加したときに、Nativemに定義したプロパティが適用されました。 これを確認するには、プロジェクトの**構成プロパティ**の [ **VC + + ディレクトリ**] プロパティを調べます。  
  
7. **ソリューションエクスプローラー**で mainpage.xaml を開き、次の xaml を使用してそのコンテンツを置き換えます。  
  
    [!code-xml[CreatingAnSDKUsingCppDemoApp#1](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcppdemoapp/cpp/mainpage.xaml#1)]  
  
8. 次のコードに一致するように Mainpage.xaml を更新します。  
  
    [!code-cpp[CreatingAnSDKUsingCppDemoApp#2](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcppdemoapp/cpp/mainpage.xaml.h#2)]  
  
9. 次のコードに一致するように Mainpage.xaml を更新します。  
  
     [!code-cpp[CreatingAnSDKUsingCppDemoApp#3](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcppdemoapp/cpp/mainpage.xaml.cpp#3)]  
  
10. F5 キーを押してアプリを実行します。  
  
11. アプリで、任意の2つの数値を入力し、操作を選択して、ボタンをクリックし **=** ます。  
  
     正しい結果が表示されます。  
  
    このチュートリアルでは、拡張 SDK を作成して使用し、 [!INCLUDE[wrt](../includes/wrt-md.md)] ライブラリと以外のライブラリを呼び出す方法について説明しました [!INCLUDE[wrt](../includes/wrt-md.md)] 。  
  
## <a name="next-steps"></a>次の手順  
  
## <a name="see-also"></a>参照  
 [チュートリアル: C# または Visual Basic を使用した SDK の作成](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)   
 [ソフトウェア開発キットを作成する](../extensibility/creating-a-software-development-kit.md)
