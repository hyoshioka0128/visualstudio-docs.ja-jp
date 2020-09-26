---
title: 'チュートリアル: スタートページへのユーザー設定の保存 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 754b9bf3-8681-4c77-b0a4-09146a4e1d2d
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8976d329f6303d60cc00609bc9ed9471456c1b63
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "91391701"
---
# <a name="walkthrough-saving-user-settings-on-a-start-page"></a>チュートリアル: スタート ページのユーザー設定の保存
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

スタートページのユーザー設定を保持することができます。 このチュートリアルに従うと、ユーザーがボタンをクリックしたときにレジストリに設定を保存するコントロールを作成し、スタートページが読み込まれるたびにその設定を取得できます。 スタートページのプロジェクトテンプレートにはカスタマイズ可能なユーザーコントロールが含まれており、既定のスタートページの XAML でそのコントロールが呼び出されるため、スタートページ自体を変更する必要はありません。  
  
 このチュートリアルでインスタンス化されている設定ストアは、インターフェイスのインスタンスであり <xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore> 、次のレジストリ位置が呼び出されたときに読み取りと書き込みを行います。 HKCU\Software\Microsoft\VisualStudio\14.0 \\ *CollectionName*  
  
 Visual Studio の実験用インスタンスで実行されている場合、設定ストアは HKCU\Software\Microsoft\VisualStudio\14.0Exp CollectionName に読み取りと書き込みを \\ *行います。*  
  
 設定を保持する方法の詳細については、「 [ユーザー設定とオプションの拡張](../extensibility/extending-user-settings-and-options.md)」を参照してください。  
  
## <a name="prerequisites"></a>[前提条件]  
  
> [!NOTE]
> このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)」を参照してください。  
>   
> スタートページのプロジェクトテンプレートは、 **拡張機能マネージャー**を使用してダウンロードできます。  
  
## <a name="setting-up-the-project"></a>プロジェクトの設定  
  
#### <a name="to-configure-the-project-for-this-walkthrough"></a>このチュートリアル用のプロジェクトを構成するには  
  
1. スタートページのプロジェクトテンプレートを使用して、スタートページプロジェクトを作成します。詳細については、「 [独自のスタートページを作成する](../misc/creating-your-own-start-page.md)」を参照してください。 プロジェクトに **Savemysettings**という名前を設定します。  
  
2. **ソリューションエクスプローラー**で、次のアセンブリ参照を StartPageControl プロジェクトに追加します。  
  
    - EnvDTE  
  
    - EnvDTE80  
  
    - Microsoft.VisualStudio.OLE.Interop  
  
    - Microsoft.VisualStudio.Shell.Interop.11.0  
  
3. MyControl.xaml を開きます。  
  
4. XAML ペインの最上位の要素の定義で、 <xref:System.Windows.Controls.UserControl> 名前空間の宣言の後に次のイベント宣言を追加します。  
  
    ```  
    Loaded="OnLoaded"  
    ```  
  
5. デザインペインで、コントロールのメイン領域をクリックし、DEL キーを押します。  
  
     これ <xref:System.Windows.Controls.Border> により、要素とその中のすべての要素が削除され、最上位レベルの要素のみが残さ <xref:System.Windows.Controls.Grid> れます。  
  
6. [ **ツールボックス**] から <xref:System.Windows.Controls.StackPanel> コントロールをグリッドにドラッグします。  
  
7. ここで、、、 <xref:System.Windows.Controls.TextBlock> <xref:System.Windows.Controls.TextBox> およびボタンをにドラッグし <xref:System.Windows.Controls.StackPanel> ます。  
  
8. 次の**x:Name** <xref:System.Windows.Controls.TextBox> `Click` 例に示すように、の x:Name 属性と、のイベントを追加し <xref:System.Windows.Controls.Button> ます。  
  
    ```xml  
    <StackPanel Width="300" HorizontalAlignment="Center" VerticalAlignment="Center">  
        <TextBlock Width="140" FontSize="14">Enter your setting</TextBlock>  
        <TextBox x:Name="txtblk" Margin="0, 5, 0, 10" Width="140" />  
        <Button Click="Button_Click" Width="100">Save My Setting</Button>  
    </StackPanel>  
    ```  
  
## <a name="implementing-the-user-control"></a>ユーザーコントロールの実装  
  
#### <a name="to-implement-the-user-control"></a>ユーザーコントロールを実装するには  
  
1. XAML ペインで、 `Click` 要素の属性を右クリックし、 <xref:System.Windows.Controls.Button> [ **イベントハンドラーに移動**] をクリックします。  
  
     MyControl.xaml.cs が開き、イベントのスタブハンドラーが作成さ `Button_Click` れます。  
  
2. 次の `using` ステートメントをファイルの先頭に追加します。  
  
     [!code-csharp[StartPageDTE#11](../snippets/csharp/VS_Snippets_VSSDK/startpagedte/cs/startpagecontrol/mycontrol.xaml.cs#11)]  
  
3. `SettingsStore`次の例に示すように、プライベートプロパティを追加します。  
  
    ```csharp  
    private IVsWritableSettingsStore _settingsStore = null;  
    private IVsWritableSettingsStore SettingsStore  
    {  
        get  
        {  
            if (_settingsStore == null)  
            {  
                // Get a reference to the DTE from the DataContext.   
                var typeDescriptor = DataContext as ICustomTypeDescriptor;  
                var propertyCollection = typeDescriptor.GetProperties();  
                var dte = propertyCollection.Find("DTE", false).GetValue(  
                    DataContext) as DTE2;  
  
                // Get the settings manager from the DTE.   
                var serviceProvider = new ServiceProvider(  
                    (Microsoft.VisualStudio.OLE.Interop.IServiceProvider)dte);  
                var settingsManager = serviceProvider.GetService(  
                    typeof(SVsSettingsManager)) as IVsSettingsManager;  
  
                // Write the user settings to _settingsStore.  
                settingsManager.GetWritableSettingsStore(  
                    (uint)__VsSettingsScope.SettingsScope_UserSettings,  
                    out _settingsStore);  
            }  
            return _settingsStore;  
        }  
    }  
    ```  
  
     このプロパティは、まず、 <xref:EnvDTE80.DTE2> ユーザーコントロールのからのオートメーションオブジェクトモデルを格納するインターフェイスへの参照を取得 <xref:System.Windows.FrameworkElement.DataContext%2A> し、次に DTE を使用してインターフェイスのインスタンスを取得し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsManager> ます。 次に、そのインスタンスを使用して、現在のユーザー設定を返します。  
  
4. イベントに次のように入力し `Button_Click` ます。  
  
    ```csharp  
    private void Button_Click(object sender, RoutedEventArgs e)  
    {  
        int exists = 0;  
        SettingsStore.CollectionExists("MySettings", out exists);  
        if (exists != 1)  
        {  
            SettingsStore.CreateCollection("MySettings");  
        }  
        SettingsStore.SetString("MySettings", "MySetting", txtblk.Text);  
    }  
    ```  
  
     これにより、テキストボックスの内容が、レジストリの "Mysetting" コレクションの "MySetting" フィールドに書き込まれます。 コレクションが存在しない場合は、作成されます。  
  
5. ユーザーコントロールのイベントに対して、次のハンドラーを追加 `OnLoaded` します。  
  
    ```csharp  
    private void OnLoaded(Object sender, RoutedEventArgs e)  
    {  
        string value;  
        SettingsStore.GetStringOrDefault(  
            "MySettings", "MySetting", "", out value);  
        txtblk.Text = value;  
    }  
    ```  
  
     これにより、テキストボックスのテキストが "MySetting" の現在の値に設定されます。  
  
6. ユーザーコントロールをビルドします。  
  
7. **ソリューションエクスプローラー**で、source.extension.vsixmanifest を開きます。  
  
8. マニフェストエディターで、[ **製品名** ] を設定して **[個人用設定の開始] ページを保存**します。  
  
     これにより、[**オプション**] ダイアログボックスの [**スタートページのカスタマイズ**] の一覧に表示される開始ページの名前が設定されます。  
  
9. StartPage をビルドします。  
  
## <a name="testing-the-control"></a>コントロールのテスト  
  
#### <a name="to-test-the-user-control"></a>ユーザーコントロールをテストするには  
  
1. F5 キーを押す。  
  
     Visual Studio の実験用インスタンスが開きます。  
  
2. 実験用インスタンスで、[ **ツール** ] メニューの [ **オプション**] をクリックします。  
  
3. [ **環境** ] ノードで、[ **起動**] をクリックし、[ **スタートページのカスタマイズ** ] ボックスの一覧の **[インストールされている拡張機能] [マイ設定の保存] スタートページ**を選択します。  
  
     **[OK]** をクリックします。  
  
4. スタートページが開いている場合は閉じ、[ **表示** ] メニューの [ **スタートページ**] をクリックします。  
  
5. スタートページで、[ **Mycontrol** ] タブをクリックします。  
  
6. テキストボックスに「 **Cat**」と入力し、[ **設定を保存**] をクリックします。  
  
7. スタートページを閉じてから、もう一度開きます。  
  
     テキストボックスに "Cat" という単語が表示されます。  
  
8. "Cat" という単語を "Dog" という語に置き換えます。 ボタンはクリックしないでください。  
  
9. スタートページを閉じてから、もう一度開きます。  
  
     設定が保存されていない場合でも、テキストボックスに "Dog" という単語が表示されます。 これは、visual Studio 自体が閉じられている場合でも、Visual studio によってツールウィンドウがメモリ内に保持されるために発生します。  
  
10. Visual Studio の実験用インスタンスを終了します。  
  
11. F5 キーを押して、実験用インスタンスを再度開きます。  
  
12. テキストボックスに "Cat" という単語が表示されます。  
  
## <a name="next-steps"></a>次の手順  
 このユーザーコントロールを変更して、さまざまなイベントハンドラーの異なる値を使用してプロパティを取得および設定することにより、任意の数のカスタム設定を保存および取得でき `SettingsStore` ます。 の呼び出しごとに異なるパラメーターを使用している限り、 `propertyName` <xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore.SetString%2A> 値はレジストリ内で相互に上書きされません。  
  
## <a name="see-also"></a>参照  
 <xref:EnvDTE80.DTE2?displayProperty=fullName>   
 [独自のスタートページを作成する](../misc/creating-your-own-start-page.md)   
 [Visual Studio コマンドのスタート ページへの追加](../extensibility/adding-visual-studio-commands-to-a-start-page.md)
