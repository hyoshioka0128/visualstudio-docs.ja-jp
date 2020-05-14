---
title: 'チュートリアル : C# または Visual Basic を使用して SDK を作成する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ef96a249-5eef-402a-a8d5-d74cb49239bd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CSharp
- VB
ms.openlocfilehash: 16eb20452601a65c498ff112ea996f2d93559940
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697551"
---
# <a name="walkthrough-create-an-sdk-using-c-or-visual-basic"></a>チュートリアル: C# または Visual Basic を使用して SDK を作成する
このチュートリアルでは、Visual C# を使用して簡単な数学ライブラリ SDK を作成し、その SDK を Visual Studio 拡張機能 (VSIX) としてパッケージ化する方法について説明します。 次の手順を実行します。

- [シンプルな計算ウィンドウ のランタイム コンポーネントを作成するには](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createClassLibrary)

- [拡張プロジェクトを作成するには](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createVSIX)
- [クラス ライブラリを使用するサンプル アプリを作成するには](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createSample)

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="to-create-the-simplemath-windows-runtime-component"></a><a name="createClassLibrary"></a>シンプルな計算ウィンドウ のランタイム コンポーネントを作成するには

1. メニュー バーで、[**ファイル] を** > クリックして **[新しい** > **プロジェクト**] をクリックします。

2. テンプレートの一覧で **、[Visual C#]** または **[Visual Basic]** を展開し **、[Windows ストア**] ノードを選択して **、[Windows ランタイム コンポーネント]** テンプレートを選択します。

3. [**名前]** ボックスで **、SimpleMath**を指定し **、[OK] をクリックします**。

4. **ソリューション エクスプローラ**で **、SimpleMath**プロジェクト ノードのショートカット メニューを開き、[**プロパティ]** をクリックします。

5. **Class1.cs**の名前を**Arithmetic.cs**に変更し、次のコードに合わせて更新します。

    [!code-csharp[CreatingAnSDKUsingWinRT#3](../extensibility/codesnippet/CSharp/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_1.cs)]
    [!code-vb[CreatingAnSDKUsingWinRT#3](../extensibility/codesnippet/VisualBasic/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_1.vb)]

6. **ソリューション エクスプローラー**で、[**ソリューションの 'SimpleMath]** ノードのショートカット メニューを開き、[**構成マネージャー**] をクリックします。

    **[構成マネージャー]** ダイアログ ボックスが開きます。

7. [**アクティブ なソリューションの構成**] ボックスの一覧で、[**リリース**] を選択します。

8. [**構成**] 列で**SimpleMath**行が **[リリース**] に設定されていることを確認し、[**閉じる**] ボタンをクリックして変更を受け入れます。

   > [!IMPORTANT]
   > SimpleMath コンポーネントの SDK には、1 つの構成のみが含まれています。 この構成はリリース ビルドである必要があります。 [!INCLUDE[win8_appstore_long](../debugger/includes/win8_appstore_long_md.md)]

9. **ソリューション エクスプローラー**で **、 SimpleMath**プロジェクト ノードのショートカット メニューを開き、[**ビルド**] を選択します。

## <a name="to-create-the-simplemathvsix-extension-project"></a><a name="createVSIX"></a>拡張プロジェクトを作成するには

1. [**ソリューション 'SimpleMath]** ノードのショートカット メニューで、[**新しいプロジェクト**の**追加]** > を選択します。

2. テンプレートの一覧で **、[Visual C#]** または **[Visual Basic]** を展開し、[**機能拡張**] ノードを選択し **、[VSIX プロジェクト**] テンプレートを選択します。

3. [**名前]** ボックス**で、SimpleMathVSIX**を指定し **、[OK]** ボタンをクリックします。

4. **ソリューション エクスプローラー**で、**ソース.extension.vsixmanifest**項目を選択します。

5. メニュー バーで 、[**View** > **コード**の表示] をクリックします。

6. 既存の XML を次の XML に置き換えます。

     [!code-xml[CreatingAnSDKUsingWinRT#1](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_2.xml)]

7. **ソリューション エクスプローラー**で **、SimpleMathVSIX**プロジェクトを選択します。

8. メニュー バーで、[**プロジェクト** > **の新しい項目の追加**] をクリックします。

9. **[共通項目**] の一覧で 、[**データ**] を展開し **、[XML ファイル**] を選択します。

10. [**名前]** ボックスで`SDKManifest.xml`を指定し、[**追加**] をクリックします。

11. **ソリューション エクスプローラー**で、 のショートカット`SDKManifest.xml`メニューを開き、[**プロパティ ]** をクリックし、 **[ VSIX に含める**] プロパティの値を**True**に変更します。

12. ファイルの内容を次の XML に置き換えます。

    **C#**

    ```xml
    <FileList
      DisplayName="WinRT Math Library (CS)"
      MinVSVersion="11.0"
      TargetFramework=".NETCore,version=v4.5"
      AppliesTo="WindowsAppContainer"
      SupportsMultipleVersions="Error"
      MoreInfo="https://msdn.microsoft.com/">
    </FileList>
    ```

    **Visual Basic**

    ```xml
    <FileList
      DisplayName="WinRT Math Library (VB)"
      MinVSVersion="11.0"
      TargetFramework=".NETCore,version=v4.5"
      AppliesTo="WindowsAppContainer"
      SupportsMultipleVersions="Error"
      MoreInfo="https://msdn.microsoft.com/">
    </FileList>
    ```

13. **ソリューション エクスプローラー**で**SimpleMathVSIX**プロジェクトのショートカット メニューを開き、[**追加**] をポイントして 、[**新しいフォルダー**] をクリックします。

14. フォルダの名前を`references`にします。

15. **[参照**設定] フォルダのショートカット メニューを開き、[**追加**] をクリックして、[**新しいフォルダ**] を選択します。

16. サブフォルダの名前を`commonconfiguration`に変更し、サブフォルダを作成し、サブフォルダ`neutral`に名前を付けます。

17. 前の 4 つの手順を繰り返し、今度`redist`は最初のフォルダの名前を に変更します。

     これで、プロジェクトには次のフォルダ構造が含まれます。

    ```xml
    references\commonconfiguration\neutral
    redist\commonconfiguration\neutral
    ```

18. **ソリューション エクスプローラー**で**SimpleMath**プロジェクトのショートカット メニューを開き、[**エクスプローラーでフォルダーを開く**] をクリックします。

19. **ファイル エクスプローラ**で*bin\Release*フォルダに移動し **、SimpleMath.winmd**ファイルのショートカット メニューを開き、[**コピー**] を選択します。

20. **ソリューション エクスプローラー**で **、SimpleMathVSIX**プロジェクトの*参照\共通構成\ニュートラル*フォルダーにファイルを貼り付けます。

21. 前の手順を繰り返し **、SimpleMathVSIX**プロジェクトの*再ディスト\共通構成\ニュートラル*フォルダーに**SimpleMath.pri**ファイルを貼り付けます。

22. **ソリューション エクスプローラー**で **、[SimpleMath.winmd]** を選択します。

23. メニュー バーで **[プロパティ**の**表示** > ]を選択します(キーボード: **F4**キーを選択します)。

24. [**プロパティ]** ウィンドウで、[**ビルド アクション**] プロパティを **[コンテンツ]** に変更し **、[VSIX に含める**] プロパティを**True**に変更します。

25. **ソリューション エクスプローラ**で、 **SimpleMath.pri**に対してこのプロセスを繰り返します。

26. **ソリューション エクスプローラー**で **、SimpleMathVSIX**プロジェクトを選択します。

27. メニュー バーで、[**ビルド** > **ビルドシンプル なMathVSIX] を**選択します。

28. **ソリューション エクスプローラー**で**SimpleMathVSIX**プロジェクトのショートカット メニューを開き、[**エクスプローラーでフォルダーを開く**] をクリックします。

29. **エクスプローラー**で*\bin\Release*フォルダーに移動し、それをインストールするのに*は SimpleMathVSIX.vsix*を実行します。

30. [**インストール**] ボタンをクリックし、インストールが完了するのを待ってから、Visual Studio を再起動します。

## <a name="to-create-a-sample-app-that-uses-the-class-library"></a><a name="createSample"></a>クラス ライブラリを使用するサンプル アプリを作成するには

1. メニュー バーで、[**ファイル] を** > クリックして **[新しい** > **プロジェクト**] をクリックします。

2. テンプレートの一覧で **、[Visual C#** ] または **[Visual Basic]** を展開し **、[Windows ストア**] ノードを選択します。

3. [**空のアプリケーション]** テンプレートを選択し、プロジェクト**に 「算術 UI」** という名前を付け **、[OK]** ボタンをクリックします。

4. **ソリューション エクスプローラー**で **、算術 UI**プロジェクトのショートカット メニューを開き、[**参照**の**追加** > ] をクリックします。

5. 参照の種類の一覧で **、[Windows]** を展開し、[**拡張機能**] を選択します。

6. 詳細ウィンドウで **、WinRT 数学ライブラリ拡張機能を**選択します。

    SDK に関する追加情報が表示されます。 このチュートリアルの前の SDKManifest.xml ファイルで指定した **[詳細情報**] リンクを選択して開https://msdn.microsoft.com/くことができます。

7. [**参照マネージャー** ] ダイアログ ボックスで **、[WinRT 数学ライブラリ**] チェック ボックスをオンにし **、[OK] ボタン**をクリックします。

8. メニュー バーの [**View** > **オブジェクト ブラウザ**の表示] をクリックします。

9. **[参照**] ボックスの一覧で、[**単純な数式**] を選択します。

     SDK の内容を確認できます。

10. **ソリューション エクスプローラー**で**MainPage.xaml**を開き、その内容を次の XAML に置き換えます。

    **C#**

    ```xml
    <Page
        x:Class="ArithmeticUI.MainPage"
        IsTabStop="False"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:SimpleMath"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        mc:Ignorable="d">

        <Grid Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
            <TextBox x:Name="_firstNumber" HorizontalAlignment="Left" Margin="414,370,0,0" TextWrapping="Wrap" Text="First Number" VerticalAlignment="Top" Height="32" Width="135" TextAlignment="Center"/>
            <TextBox x:Name="_secondNumber" HorizontalAlignment="Left" Margin="613,370,0,0" TextWrapping="Wrap" Text="Second Number" VerticalAlignment="Top" Height="32" Width="135" TextAlignment="Center"/>
            <Button Content="+" HorizontalAlignment="Left" Margin="557,301,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="-" HorizontalAlignment="Left" Margin="557,345,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="*" HorizontalAlignment="Left" Margin="557,389,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="/" HorizontalAlignment="Left" Margin="557,433,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="=" HorizontalAlignment="Left" Margin="755,367,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnResultsClick"/>
            <TextBox x:Name="_result" HorizontalAlignment="Left" Margin="809,370,0,0" TextWrapping="Wrap" Text="Result" VerticalAlignment="Top" Height="32" Width="163" TextAlignment="Center" IsReadOnly="True"/>
        </Grid>
    </Page>
    ```

    **Visual Basic**

    ```xml
    <Page
        x:Class="ArithmeticUI.MainPage"
        IsTabStop="False"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:SimpleMath"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        mc:Ignorable="d">

        <Grid Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
            <TextBox x:Name="_firstNumber" HorizontalAlignment="Left" Margin="414,370,0,0" TextWrapping="Wrap" Text="First Number" VerticalAlignment="Top" Height="32" Width="135" TextAlignment="Center"/>
            <TextBox x:Name="_secondNumber" HorizontalAlignment="Left" Margin="613,370,0,0" TextWrapping="Wrap" Text="Second Number" VerticalAlignment="Top" Height="32" Width="135" TextAlignment="Center"/>
            <Button Content="+" HorizontalAlignment="Left" Margin="557,301,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="-" HorizontalAlignment="Left" Margin="557,345,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="*" HorizontalAlignment="Left" Margin="557,389,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="/" HorizontalAlignment="Left" Margin="557,433,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="=" HorizontalAlignment="Left" Margin="755,367,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnResultsClick"/>
            <TextBox x:Name="_result" HorizontalAlignment="Left" Margin="809,370,0,0" TextWrapping="Wrap" Text="Result" VerticalAlignment="Top" Height="32" Width="163" TextAlignment="Center" IsReadOnly="True"/>
        </Grid>
    </Page>
    ```

11. 次のコードに一致するように**MainPage.xaml.cs**を更新します。

     [!code-csharp[CreatingAnSDKUsingWinRTDemoApp#2](../extensibility/codesnippet/CSharp/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_5.cs)]
     [!code-vb[CreatingAnSDKUsingWinRTDemoApp#2](../extensibility/codesnippet/VisualBasic/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_5.vb)]

12. **F5**キーを押してアプリを実行します。

13. アプリで、任意の 2 つの数値を入力し、操作を選択**=** して、ボタンを選択します。

     正しい結果が表示されます。

    拡張機能 SDK が正常に作成され、使用されました。

## <a name="see-also"></a>関連項目
- [チュートリアル: C++ を使用して SDK を作成する](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)
- [チュートリアル: Java スクリプトを使用して SDK を作成する](../extensibility/walkthrough-creating-an-sdk-using-javascript.md)
- [ソフトウェア開発キットを作成する](../extensibility/creating-a-software-development-kit.md)
