---
title: 'チュートリアル: C# または Visual Basic | を使用した SDK の作成Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: ef96a249-5eef-402a-a8d5-d74cb49239bd
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a604e3500c0ea438c987c4cf07ded98a5e03dd61
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "77558210"
---
# <a name="walkthrough-creating-an-sdk-using-c-or-visual-basic"></a>チュートリアル: C# または Visual Basic を使用して SDK を作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、Visual C# を使用して単純な数値演算ライブラリ SDK を作成し、その SDK を Visual Studio 拡張機能 (VSIX) としてパッケージ化する方法について説明します。 次の手順を実行します。  
  
- [SimpleMath Windows ランタイムコンポーネントを作成するには](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createClassLibrary)  
  
- [Simplem、Vsix 拡張機能プロジェクトを作成するには](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createVSIX)  
  
- [クラスライブラリを使用するサンプルアプリを作成するには](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createSample)  
  
## <a name="prerequisites"></a>前提条件  
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)」を参照してください。  
  
## <a name="to-create-the-simplemath-windows-runtime-component"></a><a name="createClassLibrary"></a> SimpleMath Windows ランタイムコンポーネントを作成するには  
  
1. メニューバーで、[ **ファイル**]、[ **新規作成**]、[ **新しいプロジェクト**] の順に選択します。  
  
2. テンプレートの一覧で [ **Visual C#** ] または [ **Visual Basic**] を展開し、[ **Windows ストア** ] ノードを選択して、 **Windows ランタイムコンポーネント** テンプレートを選択します。  
  
3. [ **名前** ] ボックスに **SimpleMath**を指定し、[ **OK** ] をクリックします。  
  
4. **ソリューションエクスプローラー**で、 **SimpleMath**プロジェクトノードのショートカットメニューを開き、[**プロパティ**] を選択します。  
  
5. **Class1.cs**の名前を**Arithmetic.cs**に変更し、次のコードに一致するように更新します。  
  
     [!code-csharp[CreatingAnSDKUsingWinRT#3](../snippets/csharp/VS_Snippets_VSSDK/creatingansdkusingwinrt/cs/winrtmath/arithmetic.cs#3)]
     [!code-vb[CreatingAnSDKUsingWinRT#3](../snippets/visualbasic/VS_Snippets_VSSDK/creatingansdkusingwinrt/vb/winrtmath/arithmetic.vb#3)]  
  
6. **ソリューションエクスプローラー**で、**ソリューション ' SimpleMath '** ノードのショートカットメニューを開き、[ **Configuration Manager**] を選択します。  
  
     [ **Configuration Manager** ] ダイアログボックスが表示されます。  
  
7. [ **アクティブソリューション構成** ] の一覧で [ **リリース**] を選択します。  
  
8. [ **構成** ] 列で、[ **SimpleMath** ] 行が [ **リリース**] に設定されていることを確認し、[ **閉じる** ] をクリックして変更を受け入れます。  
  
    > [!IMPORTANT]
    > SimpleMath コンポーネントの SDK に含まれる構成は1つだけです。 この構成はリリースビルドである必要があります。または、コンポーネントを使用するアプリがの認定を受けられません [!INCLUDE[win8_appstore_long](../includes/win8-appstore-long-md.md)] 。  
  
9. **ソリューションエクスプローラー**で、 **SimpleMath**プロジェクトノードのショートカットメニューを開き、[**ビルド**] を選択します。  
  
## <a name="to-create-the-simplemathvsix-extension-project"></a><a name="createVSIX"></a> Simplem、Vsix 拡張機能プロジェクトを作成するには  
  
1. **ソリューション ' SimpleMath '** ノードのショートカットメニューで、[**追加**]、[**新しいプロジェクト**] の順に選択します。  
  
2. テンプレートの一覧で [ **Visual C#** ] または [ **Visual Basic**] を展開し、[ **機能拡張** ] ノードを選択して、[ **VSIX プロジェクト** ] テンプレートを選択します。  
  
3. [ **名前** ] ボックスに「 **Simplemthe vsix**」と入力し、[ **OK** ] をクリックします。  
  
4. **ソリューションエクスプローラー**で、 **source.extension.vsixmanifest**項目を選択します。  
  
5. メニュー バーで **[表示]**、 **[コード]** の順に選択します。  
  
6. 既存の XML を次の XML に置き換えます。  
  
     [!code-xml[CreatingAnSDKUsingWinRT#1](../../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_2.xml)]
  
7. **ソリューションエクスプローラー**で、[ **Simplem] vsix**プロジェクトを選択します。  
  
8. メニューバーで、[ **プロジェクト**]、[ **新しい項目の追加**] の順に選択します。  
  
9. **共通項目**の一覧で、[**データ**] を展開し、[ **XML ファイル**] を選択します。  
  
10. [ **名前** ] ボックスにを指定し、 `SDKManifest.xml` [ **追加** ] をクリックします。  
  
11. **ソリューションエクスプローラー**で、のショートカットメニュー `SDKManifest.xml` を開き、[**プロパティ**] を選択します。次に、[ **VSIX に含ま**れる] プロパティの値を**True**に変更します。  
  
12. ファイルの内容を次の XML に置き換えます。  
  
     [!code-xml[CreatingAnSDKUsingWinRT#1](../snippets/csharp/VS_Snippets_VSSDK/creatingansdkusingwinrt/cs/winrtmathvsix/sdkmanifest.xml#1)]
     [!code-xml[CreatingAnSDKUsingWinRT#1](../snippets/visualbasic/VS_Snippets_VSSDK/creatingansdkusingwinrt/vb/winrtmathvsix/sdkmanifest.xml#1)]  
  
13. **ソリューションエクスプローラー**で、 **Simplemの vsix**プロジェクトのショートカットメニューを開き、[**追加**]、[**新しいフォルダー**] の順に選択します。  
  
14. フォルダーの名前をに変更 `references` します。  
  
15. [ **参照** ] フォルダーのショートカットメニューを開き、[ **追加**]、[ **新しいフォルダー**] の順に選択します。  
  
16. サブフォルダーの名前をに変更し `commonconfiguration` 、その中にサブフォルダーを作成して、サブフォルダーに名前を指定し `neutral` ます。  
  
17. 前の4つの手順を繰り返します。今度は、最初のフォルダーの名前をに変更 `redist` します。  
  
     プロジェクトに次のフォルダー構造が含まれるようになりました。  
  
    ```  
    references\commonconfiguration\neutral  
    redist\commonconfiguration\neutral  
    ```  
  
18. **ソリューションエクスプローラー**で、 **SimpleMath**プロジェクトのショートカットメニューを開き、[**エクスプローラーでフォルダーを開く**] を選択します。  
  
19. **エクスプローラー**で、bin\Release フォルダーに移動し、SimpleMath ファイルのショートカットメニューを開き、[**コピー**] を選択します。  
  
20. **ソリューションエクスプローラー**で、 **Simplemreferences\commonconfiguration\neutral vsix**プロジェクトのフォルダーにファイルを貼り付けます。  
  
21. 前の手順を繰り返して、SimpleMath ファイルを **Simplem vsix** プロジェクトの redist\commonconfiguration\neutral フォルダーに貼り付けます。  
  
22. **ソリューションエクスプローラー**で、[ **SimpleMath**] を選択します。  
  
23. メニューバーで、[ **表示**]、[ **プロパティ** ] の順に選択します (キーボード: F4 キーを押します)。  
  
24. [ **プロパティ** ] ウィンドウで、" **ビルドアクション** " プロパティを " **コンテンツ**" に変更し、[ **VSIX に含める** ] プロパティを [ **True**] に変更します。  
  
25. **ソリューションエクスプローラー**で、 **SimpleMath**に対してこのプロセスを繰り返します。  
  
26. **ソリューションエクスプローラー**で、[ **Simplem] vsix**プロジェクトを選択します。  
  
27. メニューバーで、[ **ビルド**]、[ **simplemのビルド**] の順に選択します。  
  
28. **ソリューションエクスプローラー**で、 **Simplemの vsix**プロジェクトのショートカットメニューを開き、[**エクスプローラーでフォルダーを開く**] を選択します。  
  
29. **エクスプローラー**で、\bin\Release フォルダーに移動してから、simplem を実行してインストールします。  
  
30. [ **インストール** ] ボタンをクリックし、インストールが完了するのを待ってから、Visual Studio を再起動します。  
  
## <a name="to-create-a-sample-app-that-uses-the-class-library"></a><a name="createSample"></a> クラスライブラリを使用するサンプルアプリを作成するには  
  
1. メニューバーで、[ **ファイル**]、[ **新規作成**]、[ **新しいプロジェクト**] の順に選択します。  
  
2. テンプレートの一覧で [ **Visual C#** ] または [ **Visual Basic**] を展開し、[ **Windows ストア** ] ノードを選択します。  
  
3. [ **空のアプリケーション** ] テンプレートを選択し、プロジェクトに **ArithmeticUI**という名前を指定して、[ **OK** ] をクリックします。  
  
4. **ソリューションエクスプローラー**で、 **ArithmeticUI**プロジェクトのショートカットメニューを開き、[**追加**]、[**参照**] の順に選択します。  
  
5. 参照の種類の一覧で、[ **Windows**] を展開し、[ **拡張機能**] を選択します。  
  
6. 詳細ウィンドウで、 **Simple MATH SDK** 拡張機能を選択します。  
  
    SDK に関する追加情報が表示されます。 このチュートリアルの前半の SDKManifest.xml ファイルで指定したように、[ **詳細情報** ] リンクをクリックして開くことができ https://docs.microsoft.com ます。  
  
7. [ **参照マネージャー** ] ダイアログボックスで、[ **Simple Math SDK** ] チェックボックスをオンにし、[ **OK** ] をクリックします。  
  
8. メニューバーで、[ **表示**]、[ **オブジェクトブラウザー**] の順に選択します。  
  
9. [ **参照** ] ボックスの一覧で、[ **単純な数値演算**] を選択します。  
  
     SDK の内容を調べることができるようになりました。  
  
10. **ソリューションエクスプローラー**で mainpage.xaml を開き、その内容を次の xaml に置き換えます。  
  
     [!code-xml[CreatingAnSDKUsingWinRTDemoApp#1](../snippets/csharp/VS_Snippets_VSSDK/creatingansdkusingwinrtdemoapp/cs/winrtmathtest/mainpage.xaml#1)]
     [!code-xml[CreatingAnSDKUsingWinRTDemoApp#1](../snippets/visualbasic/VS_Snippets_VSSDK/creatingansdkusingwinrtdemoapp/vb/winrtmathtest/mainpage.xaml#1)]  
  
11. 次のコードに一致するように MainPage.xaml.cs を更新します。  
  
     [!code-csharp[CreatingAnSDKUsingWinRTDemoApp#2](../snippets/csharp/VS_Snippets_VSSDK/creatingansdkusingwinrtdemoapp/cs/winrtmathtest/mainpage.xaml.cs#2)]
     [!code-vb[CreatingAnSDKUsingWinRTDemoApp#2](../snippets/visualbasic/VS_Snippets_VSSDK/creatingansdkusingwinrtdemoapp/vb/winrtmathtest/mainpage.xaml.vb#2)]  
  
12. F5 キーを押してアプリを実行します。  
  
13. アプリで、任意の2つの数値を入力し、操作を選択して、ボタンをクリックし **=** ます。  
  
     正しい結果が表示されます。  
  
    拡張機能 SDK が正常に作成され、使用されました。  
  
## <a name="see-also"></a>参照  
 [チュートリアル: C++ を使用した SDK の作成](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)   
 [チュートリアル: JavaScript を使用した SDK の作成](walkthrough-creating-an-sdk-using-javascript.md)   
 [ソフトウェア開発キットを作成する](../extensibility/creating-a-software-development-kit.md)
