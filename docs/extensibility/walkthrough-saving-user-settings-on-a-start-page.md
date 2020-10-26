---
title: 'チュートリアル: スタートページへのユーザー設定の保存 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 754b9bf3-8681-4c77-b0a4-09146a4e1d2d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 8dd20513defd1db8848cf6a80a29e04c127c9dd4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85903170"
---
# <a name="walkthrough-save-user-settings-on-a-start-page"></a>チュートリアル: スタートページにユーザー設定を保存する

スタートページのユーザー設定を保持することができます。 このチュートリアルに従うと、ユーザーがボタンをクリックしたときにレジストリに設定を保存するコントロールを作成し、スタートページが読み込まれるたびにその設定を取得できます。 スタートページのプロジェクトテンプレートにはカスタマイズ可能なユーザーコントロールが含まれており、既定のスタートページの XAML でそのコントロールが呼び出されるため、スタートページ自体を変更する必要はありません。

このチュートリアルでインスタンス化されている設定ストアは、インターフェイスのインスタンスであり <xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore> 、次のレジストリ位置が呼び出されたときに読み取りと書き込みを行います。 **HKCU\Software\Microsoft\VisualStudio\14.0 \\ \<CollectionName> **

Visual Studio の実験用インスタンスで実行されている場合、設定ストアは HKCU\Software\Microsoft\VisualStudio\14.0Exp の読み取りと書き込みを** \\ \<CollectionName> 行います。**

設定を保持する方法の詳細については、「 [ユーザー設定とオプションの拡張](../extensibility/extending-user-settings-and-options.md)」を参照してください。

## <a name="prerequisites"></a>前提条件

> [!NOTE]
> このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)」を参照してください。
>
> スタートページのプロジェクトテンプレートは、 **拡張機能マネージャー**を使用してダウンロードできます。

## <a name="set-up-the-project"></a>プロジェクトのセットアップ

1. 「 [カスタムスタートページを作成する](creating-a-custom-start-page.md)」の説明に従って、スタートページプロジェクトを作成します。 プロジェクトに **Savemysettings**という名前を設定します。

2. **ソリューションエクスプローラー**で、次のアセンブリ参照を StartPageControl プロジェクトに追加します。

    - EnvDTE

    - EnvDTE80

    - Microsoft.VisualStudio.OLE.Interop

    - Microsoft.VisualStudio.Shell.Interop.11.0

3. *Mycontrol .xaml*を開きます。

4. XAML ペインの最上位の要素の定義で、 <xref:System.Windows.Controls.UserControl> 名前空間の宣言の後に次のイベント宣言を追加します。

    ```xml
    Loaded="OnLoaded"
    ```

5. デザインペインで、コントロールのメイン領域をクリックし、 **del**キーを押します。

     この手順では、 <xref:System.Windows.Controls.Border> 要素とその中のすべての要素を削除し、最上位レベルの要素のみを残し <xref:System.Windows.Controls.Grid> ます。

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

## <a name="implement-the-user-control"></a>ユーザーコントロールを実装する

1. XAML ペインで、 `Click` 要素の属性を右クリックし、 <xref:System.Windows.Controls.Button> [ **イベントハンドラーに移動**] をクリックします。

     この手順では、 *MyControl.xaml.cs*を開き、イベントのスタブハンドラーを作成し `Button_Click` ます。

2. `using`ファイルの先頭に次のディレクティブを追加します。

     [!code-csharp[StartPageDTE#11](../extensibility/codesnippet/CSharp/walkthrough-saving-user-settings-on-a-start-page_1.cs)]

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

     これにより、テキストボックスの内容が、レジストリの "Mysetting" コレクションの "MySetting" フィールドに書き込まれます。 コレクションが存在しない場合は作成されます。

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

     このコードは、テキストボックスのテキストを "MySetting" の現在の値に設定します。

6. ユーザーコントロールをビルドします。

7. **ソリューションエクスプローラー**で、 *source.extension.vsixmanifest*を開きます。

8. マニフェストエディターで、[ **製品名** ] を設定して **[個人用設定の開始] ページを保存**します。

     この機能は、[**オプション**] ダイアログボックスの [**スタートページのカスタマイズ**] の一覧に表示されるスタートページの名前を設定します。

9. *StartPage を*ビルドします。

## <a name="test-the-control"></a>コントロールをテストする

1. **F5**キーを押します。

     Visual Studio の実験用インスタンスが開きます。

2. 実験用インスタンスで、[ **ツール** ] メニューの [ **オプション**] をクリックします。

3. [ **環境** ] ノードで、[ **起動**] をクリックし、[ **スタートページのカスタマイズ** ] ボックスの一覧の **[インストールされている拡張機能] [マイ設定の保存] スタートページ**を選択します。

     **[OK]** をクリックします。

4. 開いている場合はスタートページを閉じ、[ **表示** ] メニューの [ **スタートページ**] をクリックします。

5. スタートページで、[ **Mycontrol** ] タブをクリックします。

6. テキストボックスに「 **Cat**」と入力し、[ **設定を保存**] をクリックします。

7. スタートページを閉じてから、もう一度開きます。

     テキストボックスに "Cat" という単語が表示されます。

8. "Cat" という単語を "Dog" という語に置き換えます。 ボタンはクリックしないでください。

9. スタートページを閉じてから、もう一度開きます。

     設定を保存していない場合でも、テキストボックスに "Dog" という単語が表示されます。これは、visual Studio 自体が閉じられた場合でも、visual Studio がツールウィンドウをメモリ内に保持するためです。

10. Visual Studio の実験用インスタンスを終了します。

11. **F5**キーを押して、実験的なインスタンスを再度開きます。

12. テキストボックスに "Cat" という単語が表示されます。

## <a name="next-steps"></a>次のステップ

このユーザーコントロールを変更して、さまざまなイベントハンドラーの異なる値を使用してプロパティを取得および設定することにより、任意の数のカスタム設定を保存および取得でき `SettingsStore` ます。 の呼び出しごとに異なるパラメーターを使用している限り、 `propertyName` <xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore.SetString%2A> 値はレジストリ内で相互に上書きされません。

## <a name="see-also"></a>関連項目

- <xref:EnvDTE80.DTE2?displayProperty=fullName>
- [スタートページへの Visual Studio コマンドの追加](../extensibility/adding-visual-studio-commands-to-a-start-page.md)
