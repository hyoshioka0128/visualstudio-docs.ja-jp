---
title: スタート ページへの Visual Studio コマンドの追加 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- start page commands
- vs:VSCommands
ms.assetid: a8e2765c-cfb5-47b5-a414-6e48b434e0c2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 13dd40006039209b06cc6a71760fdbaa240db4fe
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740119"
---
# <a name="add-visual-studio-commands-to-a-start-page"></a>スタート ページへの Visual Studio コマンドの追加

カスタム スタート ページを作成するときに、Visual Studio のコマンドを追加できます。 このドキュメントでは、Visual Studio コマンドをスタート ページの XAML オブジェクトにバインドするさまざまな方法について説明します。

XAML でのコマンドの詳細については、「[コマンドの概要」を](/dotnet/framework/wpf/advanced/commanding-overview)参照してください。

## <a name="add-commands-from-the-command-well"></a>コマンドウェルからコマンドを追加する

「カスタム スタート ページ[の作成](../extensibility/creating-a-custom-start-page.md)」で作成された<xref:Microsoft.VisualStudio.PlatformUI?displayProperty=fullName>スタート<xref:Microsoft.VisualStudio.Shell?displayProperty=fullName>ページでは、 および 名前空間が次のように追加されました。

```xml
xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
```

アセンブリから別の名前空間*を追加します*。 (プロジェクトでこのアセンブリへの参照を追加する必要があります)。

```xml
xmlns:vscom="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.Immutable.11.0"
```

このエイリアスを使用`vscom:`して、コントロールのプロパティを<xref:System.Windows.Controls.Primitives.ButtonBase.Command%2A>`vscom:VSCommands.ExecuteCommand`に設定することで、Visual Studio コマンドをページ上の XAML コントロールにバインドできます。 次の<xref:System.Windows.Controls.Primitives.ButtonBase.CommandParameter%2A>例に示すように、実行するコマンドの名前をプロパティに設定できます。

```xml
<Button Name="btnNewProj" Content="New Project"
    Command="{x:Static vscom:VSCommands.ExecuteCommand}"
    CommandParameter="File.NewProject" >
</Button>
```

> [!NOTE]
> XAML`x:`スキーマを参照するエイリアスは、すべてのコマンドの先頭に必要です。

 プロパティの値は`Command`、**コマンド**ウィンドウからアクセスできる任意のコマンドに設定できます。 使用できるコマンドの一覧については、「 [Visual Studio のコマンド エイリアス](../ide/reference/visual-studio-command-aliases.md)」を参照してください。

 追加するコマンドで追加のパラメーターが必要な場合は、`CommandParameter`プロパティの値に追加できます。 次の例に示すように、スペースを使用してコマンドからパラメーターを分離します。

```xml
<Button Content="Web Search"
        Command="{x:Static vscom:VSCommands.ExecuteCommand}"
        CommandParameter="View.WebBrowser www.bing.com" />
```

### <a name="call-extensions-from-the-command-well"></a>コマンドウェルから拡張機能を呼び出す
 他の Visual Studio コマンドを呼び出すために使用されるのと同じ構文を使用して、登録済みの VSPackage からコマンドを呼び出すことができます。 たとえば、インストールされている VSPackage が [**表示**] メニューに **[ホーム ページ**] コマンドを追加`View.HomePage`した場合は、 に設定`CommandParameter`してそのコマンドを呼び出すことができます。

> [!NOTE]
> VSPackage に関連付けられているコマンドを呼び出す場合、コマンドが呼び出されたときにパッケージを読み込む必要があります。

## <a name="add-commands-from-assemblies"></a>アセンブリからコマンドを追加する
 アセンブリからコマンドを呼び出す、またはメニュー コマンドに関連付けられていない VSPackage のコードにアクセスするには、アセンブリのエイリアスを作成し、エイリアスを呼び出す必要があります。

### <a name="to-call-a-command-from-an-assembly"></a>アセンブリからコマンドを呼び出すには

1. ソリューションで、アセンブリへの参照を追加します。

2. 次の例に示すように *、StartPage.xaml*ファイルの先頭に、アセンブリの名前空間ディレクティブを追加します。

    ```xml
    xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"
    ```

3. 次の例に示すように`Command`、XAML オブジェクトのプロパティを設定してコマンドを呼び出します。

     Xaml

    ```
    <vs:Button Text="Hide me" Command="{x:Static vsc:HideControl}" .../>
    ```

> [!NOTE]
> アセンブリをコピーし、*.に貼り付ける必要があります。\\{Visual Studio のインストール フォルダー}\Common7\IDE\PrivateAssembly を使用\*して、呼び出される前に読み込まれるようにします。

## <a name="add-commands-with-the-dte-object"></a>DTE オブジェクトを使用したコマンドの追加
 DTE オブジェクトには、マークアップとコードの両方で、スタート ページからアクセスできます。

 マークアップでは、[バインディング マークアップ拡張機能](/dotnet/framework/wpf/advanced/binding-markup-extension)構文を使用してオブジェクトを呼び出すことによって<xref:EnvDTE.DTE>、このオブジェクトにアクセスできます。 この方法を使用すると、コレクションを返すプロパティなどの単純なプロパティにバインドできますが、メソッドやサービスにバインドすることはできません。 <xref:EnvDTE._DTE.Name%2A>プロパティにバインド<xref:System.Windows.Controls.TextBlock>するコントロールと、プロパティによって返されるコレクションのプロパティを<xref:System.Windows.Controls.ListBox><xref:EnvDTE.Window.Caption%2A>列挙するコントロールの例を次に<xref:EnvDTE._DTE.Windows%2A>示します。

```xml
<TextBlock Text="{Binding Path=DTE.Name}" FontSize="12" HorizontalAlignment="Center"/>
<ListBox ItemsSource="{Binding Path=DTE.Windows}">
    <ListBox.ItemTemplate>
        <DataTemplate>
            <TextBlock Text="{Binding Path=Caption}"/>
        </DataTemplate>
    </ListBox.ItemTemplate>
</ListBox
```

 例については、「[チュートリアル: スタート ページでのユーザー設定の保存 」を](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md)参照してください。

## <a name="see-also"></a>関連項目

- [スタート ページへのユーザー コントロールの追加](../extensibility/adding-user-control-to-the-start-page.md)
