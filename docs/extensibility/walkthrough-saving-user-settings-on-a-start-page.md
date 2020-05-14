---
title: 'チュートリアル: スタート ページにユーザー設定を保存する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 754b9bf3-8681-4c77-b0a4-09146a4e1d2d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 8c791bb33d6c6a3952c14d5073857b0c3131cecf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697073"
---
# <a name="walkthrough-save-user-settings-on-a-start-page"></a>チュートリアル: スタート ページにユーザー設定を保存する

スタート ページのユーザー設定を保持できます。 このチュートリアルを実行すると、ユーザーがボタンをクリックしたときに設定をレジストリに保存し、スタート ページが読み込まれるたびにその設定を取得するコントロールを作成できます。 スタート ページ プロジェクト テンプレートにはカスタマイズ可能なユーザー コントロールが含まれており、既定のスタート ページ XAML はそのコントロールを呼び出すため、スタート ページ自体を変更する必要はありません。

このチュートリアルでインスタンス化される設定ストアは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore>呼び出されたときに次のレジストリの場所に読み取りおよび書き込みを行うインターフェイスのインスタンス **>です。\\\<**

Visual Studio の実験用インスタンスで実行されている場合、設定ストアは**HKCU\ソフトウェア\マイクロソフト\VisualStudio\14.0Exp\\\<コレクション名>** 読み取りと書き込みを行います。

設定を保持する方法の詳細については、「[ユーザー設定とオプションの拡張](../extensibility/extending-user-settings-and-options.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント

> [!NOTE]
> このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。
>
> [スタート ページ] プロジェクト テンプレートは **、拡張機能マネージャー**を使用してダウンロードできます。

## <a name="set-up-the-project"></a>プロジェクトのセットアップ

1. カスタムスタートページの作成 の説明に従って[スタートページプロジェクトを作成](creating-a-custom-start-page.md)します。 プロジェクトに名前を**付けます。**

2. **ソリューション エクスプローラー**で、次のアセンブリ参照を StartPageControl プロジェクトに追加します。

    - EnvDTE

    - EnvDTE80

    - Microsoft.VisualStudio.OLE.Interop

    - Microsoft.VisualStudio.Shell.Interop.11.0

3. *を*開きます。

4. XAML ペインの最上位の<xref:System.Windows.Controls.UserControl>要素定義で、名前空間宣言の後に次のイベント宣言を追加します。

    ```xml
    Loaded="OnLoaded"
    ```

5. デザイン ウィンドウで、コントロールのメイン領域をクリックし **、Del**キーを押します。

     この手順では、<xref:System.Windows.Controls.Border>要素とその中のすべてのものが削除され、最上位の<xref:System.Windows.Controls.Grid>要素だけが残ります。

6. **ツールボックス**から、コントロールを<xref:System.Windows.Controls.StackPanel>グリッドにドラッグします。

7. では、 <xref:System.Windows.Controls.TextBlock>、 <xref:System.Windows.Controls.TextBox>、 、 ボタン<xref:System.Windows.Controls.StackPanel>を にドラッグします。

8. **x:Name**属性を<xref:System.Windows.Controls.TextBox>追加し、次の`Click`例に示<xref:System.Windows.Controls.Button>すように、 にイベントを追加します。

    ```xml
    <StackPanel Width="300" HorizontalAlignment="Center" VerticalAlignment="Center">
        <TextBlock Width="140" FontSize="14">Enter your setting</TextBlock>
        <TextBox x:Name="txtblk" Margin="0, 5, 0, 10" Width="140" />
        <Button Click="Button_Click" Width="100">Save My Setting</Button>
    </StackPanel>
    ```

## <a name="implement-the-user-control"></a>ユーザー コントロールを実装する

1. XAML ペインで、`Click`<xref:System.Windows.Controls.Button>要素の属性を右クリックし、[イベント**ハンドラーに移動**] をクリックします。

     この手順では *、 MyControl.xaml.cs*開き、イベントのスタブ`Button_Click`ハンドラーを作成します。

2. ファイルの先頭`using`に次のディレクティブを追加します。

     [!code-csharp[StartPageDTE#11](../extensibility/codesnippet/CSharp/walkthrough-saving-user-settings-on-a-start-page_1.cs)]

3. 次の例`SettingsStore`に示すように、プライベート プロパティを追加します。

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

     このプロパティは、まず、オートメーション<xref:EnvDTE80.DTE2>オブジェクト モデルを含むインターフェイスへの参照をユーザー<xref:System.Windows.FrameworkElement.DataContext%2A>コントロールから取得し、次に DTE を使用してインターフェイスの<xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsManager>インスタンスを取得します。 その後、そのインスタンスを使用して現在のユーザー設定を返します。

4. イベントを`Button_Click`次のように入力します。

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

     これにより、テキスト ボックスの内容がレジストリの "MySettings" コレクションの "MySetting" フィールドに書き込まれます。 コレクションが存在しない場合は、作成されます。

5. ユーザー コントロールのイベントに`OnLoaded`対して次のハンドラーを追加します。

    ```csharp
    private void OnLoaded(Object sender, RoutedEventArgs e)
    {
        string value;
        SettingsStore.GetStringOrDefault(
            "MySettings", "MySetting", "", out value);
        txtblk.Text = value;
    }
    ```

     このコードは、テキスト ボックスのテキストを現在の値 "MySetting" に設定します。

6. ユーザー コントロールをビルドします。

7. **ソリューション エクスプローラー**で、*ソース.extension.vsixmanifest*を開きます。

8. マニフェスト エディターで、[**製品名]** を **[個人用設定のスタート ページの保存]** に設定します。

     この機能は、[**オプション]** ダイアログ ボックスの [スタート ページのカスタマイズ] リストに表示される **[スタート ページ**] の名前を設定します。

9. *ビルド のスタート ページ.xaml*.

## <a name="test-the-control"></a>コントロールをテストする

1. **F5**キーを押します。

     Visual Studio の実験用インスタンスが開きます。

2. 実験用のインスタンスで、[**ツール**] メニューの [**オプション**] をクリックします。

3. [**環境**] ノードで [**スタートアップ**] をクリックし、[スタート**ページのカスタマイズ]** ボックスの一覧の [**インストールされた拡張機能] 個人用設定の保存開始ページ**] をクリックします。

     **[OK]** をクリックします。

4. スタート ページが開いている場合は閉じ、[**表示**] メニューの [**スタート ページ**] をクリックします。

5. スタート ページで、[マイ**コントロール**] タブをクリックします。

6. テキスト ボックスに**Cat**と入力し、[**設定の保存**] をクリックします。

7. スタート ページを閉じてから、もう一度開きます。

     テキスト ボックスに "Cat" という単語が表示されます。

8. "猫" という単語を "Dog" という単語に置き換えます。 ボタンをクリックしないでください。

9. スタート ページを閉じてから、もう一度開きます。

     Visual Studio 自体が閉じるまで、Visual Studio はツール ウィンドウをメモリに保持するため、設定を保存しなくても、テキスト ボックスに "Dog" という語を表示する必要があります。

10. Visual Studio の実験用インスタンスを終了します。

11. **F5 キー**を押して、実験用インスタンスを再度開きます。

12. テキスト ボックスに "Cat" という単語が表示されます。

## <a name="next-steps"></a>次の手順

このユーザー コントロールを変更して、さまざまなイベント ハンドラの異なる値を使用してプロパティを取得および設定することで、任意の`SettingsStore`数のカスタム設定を保存および取得できます。 の呼び出しごとに異`propertyName`なるパラメーターを<xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore.SetString%2A>使用する限り、レジストリ内の値は上書きしません。

## <a name="see-also"></a>関連項目

- <xref:EnvDTE80.DTE2?displayProperty=fullName>
- [スタート ページへの Visual Studio コマンドの追加](../extensibility/adding-visual-studio-commands-to-a-start-page.md)
