---
title: 'チュートリアル: C# または Visual Basic | を使用した SDK の作成Microsoft Docs'
description: このチュートリアルを使用して、Visual C# を使用して簡単な数値演算ライブラリ SDK を作成し、その SDK を Visual Studio 拡張機能としてパッケージ化する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: ef96a249-5eef-402a-a8d5-d74cb49239bd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CSharp
- VB
ms.openlocfilehash: 5b44566e4a8df323af6132128a8881b54c6f493f
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217295"
---
# <a name="walkthrough-create-an-sdk-using-c-or-visual-basic"></a>チュートリアル: C# または Visual Basic を使用した SDK の作成
このチュートリアルでは、Visual C# を使用して単純な数値演算ライブラリ SDK を作成し、その SDK を Visual Studio 拡張機能 (VSIX) としてパッケージ化する方法について説明します。 次の手順を実行します。

- [SimpleMath Windows ランタイムコンポーネントを作成するには](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createClassLibrary)

- [Simplem、Vsix 拡張機能プロジェクトを作成するには](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createVSIX)
- [クラスライブラリを使用するサンプルアプリを作成するには](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createSample)

## <a name="prerequisites"></a>前提条件
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="to-create-the-simplemath-windows-runtime-component"></a><a name="createClassLibrary"></a> SimpleMath Windows ランタイムコンポーネントを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

2. テンプレートの一覧で [ **Visual C#** ] または [ **Visual Basic**] を展開し、[ **Windows ストア** ] ノードを選択して、 **Windows ランタイムコンポーネント** テンプレートを選択します。

3. [ **名前** ] ボックスに **SimpleMath** を指定し、[ **OK** ] をクリックします。

4. **ソリューションエクスプローラー** で、 **SimpleMath** プロジェクトノードのショートカットメニューを開き、[**プロパティ**] を選択します。

5. **Class1** を「**数学的**」に変更し、次のコードに一致するように更新します。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/creatingansdkusingwinrt/cs/winrtmath/arithmetic.cs" id="Snippet3":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/creatingansdkusingwinrt/vb/winrtmath/arithmetic.vb" id="Snippet3":::

6. **ソリューションエクスプローラー** で、**ソリューション ' SimpleMath '** ノードのショートカットメニューを開き、[ **Configuration Manager**] を選択します。

    [ **Configuration Manager** ] ダイアログボックスが表示されます。

7. [ **アクティブソリューション構成** ] の一覧で [ **リリース**] を選択します。

8. [ **構成** ] 列で、[ **SimpleMath** ] 行が [ **リリース**] に設定されていることを確認し、[ **閉じる** ] をクリックして変更を受け入れます。

   > [!IMPORTANT]
   > SimpleMath コンポーネントの SDK に含まれる構成は1つだけです。 この構成はリリースビルドである必要があります。または、コンポーネントを使用するアプリがの認定を受けられません [!INCLUDE[win8_appstore_long](../debugger/includes/win8_appstore_long_md.md)] 。

9. **ソリューションエクスプローラー** で、 **SimpleMath** プロジェクトノードのショートカットメニューを開き、[**ビルド**] を選択します。

## <a name="to-create-the-simplemathvsix-extension-project"></a><a name="createVSIX"></a> Simplem、Vsix 拡張機能プロジェクトを作成するには

1. **ソリューション ' SimpleMath '** ノードのショートカットメニューで、[新しいプロジェクトの **追加**] を選択し  >  ます。

2. テンプレートの一覧で [ **Visual C#** ] または [ **Visual Basic**] を展開し、[ **機能拡張** ] ノードを選択して、[ **VSIX プロジェクト** ] テンプレートを選択します。

3. [ **名前** ] ボックスに「 **Simplemthe vsix**」と入力し、[ **OK** ] をクリックします。

4. **ソリューションエクスプローラー** で、 **source.extension.vsixmanifest** 項目を選択します。

5. メニュー バーで **[表示]**  >  **[コード]** の順に選択します。

6. 既存の XML を次の XML に置き換えます。

   ```xml
   <PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011" xmlns:d="http://schemas.microsoft.com/developer/vsx-schema-design/2011">
     <Metadata>
       <Identity Id="SimpleMath" Version="1.0" Language="en-US" Publisher="[YourName]" />
       <DisplayName>SimpleMath Library</DisplayName>
       <Description xml:space="preserve">Basic arithmetic operations in a WinRT-compatible library. Implemented in C#.</Description>
     </Metadata>
     <Installation Scope="Global" AllUsers="true">
       <InstallationTarget Id="Microsoft.ExtensionSDK" TargetPlatformIdentifier="Windows" TargetPlatformVersion="v8.0" SdkName="SimpleMath" SdkVersion="1.0" />
     </Installation>
     <Prerequisites>
       <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[14.0,16.0]" />
     </Prerequisites>
     <Dependencies>
       <Dependency Id="Microsoft.Framework.NDP" DisplayName="Microsoft .NET Framework" d:Source="Manual" Version="4.5" />
     </Dependencies>
     <Assets>
       <Asset Type="Microsoft.ExtensionSDK" d:Source="File" Path="SDKManifest.xml" />
     </Assets>
   </PackageManifest>
   ```

7. **ソリューションエクスプローラー** で、[ **Simplem] vsix** プロジェクトを選択します。

8. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

9. **共通項目** の一覧で、[**データ**] を展開し、[ **XML ファイル**] を選択します。

10. [ **名前** ] ボックスにを指定し、 `SDKManifest.xml` [ **追加** ] をクリックします。

11. **ソリューションエクスプローラー** で、のショートカットメニュー `SDKManifest.xml` を開き、[**プロパティ**] を選択します。次に、[ **VSIX に含ま** れる] プロパティの値を **True** に変更します。

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

13. **ソリューションエクスプローラー** で、 **Simplemの vsix** プロジェクトのショートカットメニューを開き、[**追加**]、[**新しいフォルダー**] の順に選択します。

14. フォルダーの名前をに変更 `references` します。

15. [ **参照** ] フォルダーのショートカットメニューを開き、[ **追加**]、[ **新しいフォルダー**] の順に選択します。

16. サブフォルダーの名前をに変更し `commonconfiguration` 、その中にサブフォルダーを作成して、サブフォルダーに名前を指定し `neutral` ます。

17. 前の4つの手順を繰り返します。今度は、最初のフォルダーの名前をに変更 `redist` します。

     プロジェクトに次のフォルダー構造が含まれるようになりました。

    ```xml
    references\commonconfiguration\neutral
    redist\commonconfiguration\neutral
    ```

18. **ソリューションエクスプローラー** で、 **SimpleMath** プロジェクトのショートカットメニューを開き、[**エクスプローラーでフォルダーを開く**] を選択します。

19. **エクスプローラー** で、 *bin\Release* フォルダーに移動し、 **SimpleMath** ファイルのショートカットメニューを開き、[**コピー**] を選択します。

20. **ソリューションエクスプローラー** で、 **Simplemreferences\commonconfiguration\neutral vsix** プロジェクトのフォルダーにファイルを貼り付けます。

21. 前の手順を繰り返して、 **SimpleMath** ファイルを **Simplem vsix** プロジェクトの *redist\commonconfiguration\neutral* フォルダーに貼り付けます。

22. **ソリューションエクスプローラー** で、[ **SimpleMath**] を選択します。

23. メニューバーで、[プロパティの **表示**] を選択し  >  ます (キーボード: **F4** キーを押します)。

24. [ **プロパティ** ] ウィンドウで、" **ビルドアクション** " プロパティを " **コンテンツ**" に変更し、[ **VSIX に含める** ] プロパティを [ **True**] に変更します。

25. **ソリューションエクスプローラー** で、 **SimpleMath** に対してこのプロセスを繰り返します。

26. **ソリューションエクスプローラー** で、[ **Simplem] vsix** プロジェクトを選択します。

27. メニューバーで、 **[ビルド]**[  >  **simplem] [vsix**] の順に選択します。

28. **ソリューションエクスプローラー** で、 **Simplemの vsix** プロジェクトのショートカットメニューを開き、[**エクスプローラーでフォルダーを開く**] を選択します。

29. **エクスプローラー** で、\bin\Release フォルダーに移動してから、 *simplem* を実行してインストールします。 

30. [ **インストール** ] ボタンをクリックし、インストールが完了するのを待ってから、Visual Studio を再起動します。

## <a name="to-create-a-sample-app-that-uses-the-class-library"></a><a name="createSample"></a> クラスライブラリを使用するサンプルアプリを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

2. テンプレートの一覧で [ **Visual C#** ] または [ **Visual Basic**] を展開し、[ **Windows ストア** ] ノードを選択します。

3. [ **空のアプリケーション** ] テンプレートを選択し、プロジェクトに **ArithmeticUI** という名前を指定して、[ **OK** ] をクリックします。

4. **ソリューションエクスプローラー** で、 **ArithmeticUI** プロジェクトのショートカットメニューを開き、[参照の **追加**] を選択し  >  ます。

5. 参照の種類の一覧で、[ **Windows**] を展開し、[ **拡張機能**] を選択します。

6. 詳細ペインで、 **WinRT Math ライブラリ** 拡張機能を選択します。

    SDK に関する追加情報が表示されます。 このチュートリアルの前半の SDKManifest.xml ファイルで指定したように、[ **詳細情報** ] リンクをクリックして開くことができ https://msdn.microsoft.com/ ます。

7. [ **参照マネージャー** ] ダイアログボックスで、[ **WinRT Math Library** ] チェックボックスをオンにし、[ **OK** ] をクリックします。

8. メニューバーで、[オブジェクトブラウザーの **表示**] を選択し  >  ます。

9. [ **参照** ] ボックスの一覧で、[ **単純な数値演算**] を選択します。

     SDK の内容を調べることができるようになりました。

10. **ソリューションエクスプローラー** で **mainpage.xaml** を開き、その内容を次の xaml に置き換えます。

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

11. 次のコードに一致するように **mainpage.xaml** を更新します。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Windows.Foundation;
using Windows.Foundation.Collections;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Controls.Primitives;
using Windows.UI.Xaml.Data;
using Windows.UI.Xaml.Input;
using Windows.UI.Xaml.Media;
using Windows.UI.Xaml.Navigation;

// The Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=234238

namespace ArithmeticUI
{
    /// <summary>
    /// An empty page that can be used on its own or navigated to within a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        public static string operation = null;

        public MainPage()
        {
            this.InitializeComponent();
        }

        /// <summary>
        /// Invoked when this page is about to be displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.  The Parameter
        /// property is typically used to configure the page.</param>
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
        }

        /// <summary>
        /// Sets the operator chosen by the user
        /// </summary>
        /// <param name="sender"></param>
        /// <param name="e"></param>
        private void OnOperatorClick(object sender, RoutedEventArgs e)
        {
            operation = (sender as Button).Content.ToString();
        }

        /// <summary>
        /// Calls the SimpleMath SDK to do simple arithmetic
        /// </summary>
        /// <param name="sender"></param>
        /// <param name="e"></param>
        private void OnResultsClick(object sender, RoutedEventArgs e)
        {
            try
            {
                float firstNumber = float.Parse(this._firstNumber.Text);
                float secondNumber = float.Parse(this._secondNumber.Text);

                SimpleMath.Arithmetic math = new SimpleMath.Arithmetic();

                switch (operation)
                {
                    case "+":
                        this._result.Text = (math.add(firstNumber, secondNumber)).ToString();
                        break;
                    case "-":
                        this._result.Text = (math.subtract(firstNumber, secondNumber)).ToString();
                        break;
                    case "*":
                        this._result.Text = (math.multiply(firstNumber, secondNumber)).ToString();
                        break;
                    case "/":
                        this._result.Text = (math.divide(firstNumber, secondNumber)).ToString();
                        break;
                    default:
                        this._result.Text = "Choose operator";
                        break;
                }
            }
            catch
            {
                this._result.Text = "Enter valid #";
            }
        }
    }
}
```

```vb
' The Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=234238

''' <summary>
''' An empty page that can be used on its own or navigated to within a Frame.
''' </summary>
Public NotInheritable Class MainPage
    Inherits Page

    ''' <summary>
    ''' Invoked when this page is about to be displayed in a Frame.
    ''' </summary>
    ''' <param name="e">Event data that describes how this page was reached.  The Parameter
    ''' property is typically used to configure the page.</param>
    Protected Overrides Sub OnNavigatedTo(e As Navigation.NavigationEventArgs)
    
    End Sub

    Public Shared operation As String = Nothing

    ''' <summary>
    ''' Sets the operator chosen by the user
    ''' </summary>
    ''' <param name="sender"></param>
    ''' <param name="e"></param>
    Private Sub OnOperatorClick(ByVal sender As Object, ByVal e As RoutedEventArgs)
        operation = If(TypeOf sender Is Button, CType(sender, Button), Nothing).Content.ToString()
    End Sub


    ''' <summary>
    ''' Calls the SimpleMath SDK to do simple arithmetic
    ''' </summary>
    ''' <param name="sender"></param>
    ''' <param name="e"></param>
    Private Sub OnResultsClick(ByVal sender As Object, ByVal e As RoutedEventArgs)

        Try

            Dim firstNumber As Single = Single.Parse(Me._firstNumber.Text)
            Dim secondNumber As Single = Single.Parse(Me._secondNumber.Text)

            Dim math As New SimpleMath.Arithmetic()

            Select Case (operation)

                Case "+"
                    Me._result.Text = (math.Add(firstNumber, secondNumber)).ToString()

                Case "-"
                    Me._result.Text = (math.Subtract(firstNumber, secondNumber)).ToString()
                Case "*"
                    Me._result.Text = (math.Multiply(firstNumber, secondNumber)).ToString()
                Case "/"
                    Me._result.Text = (math.Divide(firstNumber, secondNumber)).ToString()
                Case Else
                    Me._result.Text = "Choose operator"

            End Select

        Catch
            Me._result.Text = "Enter valid #"
        End Try
    End Sub
End Class
```

12. F5 キーを **押し** てアプリを実行します。

13. アプリで、任意の2つの数値を入力し、操作を選択して、ボタンをクリックし **=** ます。

     正しい結果が表示されます。

    拡張機能 SDK が正常に作成され、使用されました。

## <a name="see-also"></a>関連項目
- [チュートリアル: C++ を使用して SDK を作成する](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)
- [チュートリアル: JavaScript を使用した SDK の作成](../extensibility/walkthrough-creating-an-sdk-using-javascript.md)
- [ソフトウェア開発キットを作成する](../extensibility/creating-a-software-development-kit.md)
