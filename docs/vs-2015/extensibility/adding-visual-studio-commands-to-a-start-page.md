---
title: スタートページへの Visual Studio コマンドの追加 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- start page commands
- vs:VSCommands
ms.assetid: a8e2765c-cfb5-47b5-a414-6e48b434e0c2
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0a2042ef9a96eed99636ea0a2f5f09d99cd35ea2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65699154"
---
# <a name="adding-visual-studio-commands-to-a-start-page"></a>Visual Studio コマンドのスタート ページへの追加
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

カスタムスタートページを作成するときに、Visual Studio コマンドを追加できます。 このドキュメントでは、スタートページで Visual Studio コマンドを XAML オブジェクトにバインドするさまざまな方法について説明します。  
  
 XAML でのコマンドの詳細については、「コマンドの[概要](https://msdn.microsoft.com/library/bc208dfe-367d-426a-99de-52b7e7511e81)」を参照してください。  
  
## <a name="adding-commands-from-the-command-well"></a>コマンドウェルからコマンドを追加する  
 「 [カスタムスタートページの作成](../extensibility/creating-a-custom-start-page.md) 」で作成したスタートページには、次のように、 <xref:Microsoft.VisualStudio.PlatformUI?displayProperty=fullName> 名前空間と名前空間が追加されて <xref:Microsoft.VisualStudio.Shell?displayProperty=fullName> います。  
  
```  
xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"  
xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"  
```  
  
 アセンブリ Microsoft.VisualStudio.Shell.Immutable.11.0.dll から VisualStudio の別の名前空間を追加します。 (このアセンブリへの参照をプロジェクトに追加することが必要になる場合があります)。  
  
```xml  
xmlns:vscom="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.Immutable.11.0"  
```  
  
 エイリアスを使用し `vscom:` て、 <xref:System.Windows.Controls.Primitives.ButtonBase.Command%2A> コントロールのプロパティをに設定することにより、Visual Studio のコマンドをページの XAML コントロールにバインドでき `vscom:VSCommands.ExecuteCommand` ます。 その後、次の <xref:System.Windows.Controls.Primitives.ButtonBase.CommandParameter%2A> 例に示すように、プロパティを実行するコマンドの名前に設定できます。  
  
```xml  
<Button Name="btnNewProj" Content="New Project"   
    Command="{x:Static vscom:VSCommands.ExecuteCommand}"  
    CommandParameter="File.NewProject" >  
</Button>  
```  
  
> [!NOTE]
> `x:`すべてのコマンドの先頭には、XAML スキーマを参照するエイリアスが必要です。  
  
 プロパティの値は `Command` 、 **コマンド** ウィンドウからアクセスできる任意のコマンドに設定できます。 使用可能なコマンドの一覧については、「 [Visual Studio コマンドのエイリアス](../ide/reference/visual-studio-command-aliases.md)」を参照してください。  
  
 追加するコマンドに追加のパラメーターが必要な場合は、プロパティの値に追加することができ `CommandParameter` ます。 次の例に示すように、スペースを使用してコマンドからパラメーターを分離します。  
  
```xml  
<Button Content="Web Search"   
        Command="{x:Static vscom:VSCommands.ExecuteCommand}"  
        CommandParameter="View.WebBrowser www.bing.com" />  
```  
  
### <a name="calling-extensions-from-the-command-well"></a>コマンドウェルから拡張機能を呼び出す  
 他の Visual Studio コマンドを呼び出すときと同じ構文を使用して、登録されている Vspackage からコマンドを呼び出すことができます。 たとえば、VSPackage がインストールされている場合、[**表示**] メニューに [**ホームページ**] コマンドを追加すると、をに設定することによって、そのコマンドを呼び出すことができ `CommandParameter` `View.HomePage` ます。  
  
> [!NOTE]
> VSPackage に関連付けられているコマンドを呼び出す場合は、コマンドが呼び出されたときにパッケージを読み込む必要があります。  
  
## <a name="adding-commands-from-assemblies"></a>アセンブリからのコマンドの追加  
 アセンブリからコマンドを呼び出したり、メニューコマンドに関連付けられていない VSPackage 内のコードにアクセスしたりするには、アセンブリのエイリアスを作成し、エイリアスを呼び出す必要があります。  
  
#### <a name="to-call-a-command-from-an-assembly"></a>アセンブリからコマンドを呼び出すには  
  
1. ソリューションで、アセンブリへの参照を追加します。  
  
2. 次の例に示すように、StartPage ファイルの先頭に、アセンブリの名前空間ディレクティブを追加します。  
  
    ```xml  
    xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"  
    ```  
  
3. `Command`次の例に示すように、XAML オブジェクトのプロパティを設定して、コマンドを呼び出します。  
  
     Xaml  
  
    ```  
    <vs:Button Text="Hide me" Command="{x:Static vsc:HideControl}" .../>  
    ```  
  
> [!NOTE]
> アセンブリをコピーしてから、に \\ 貼り付ける必要があります。*Visual Studio のインストールフォルダー*は、呼び出される前に読み込まれていることを確認するために \Common7\IDE\PrivateAssemblies\ します。  
  
## <a name="adding-commands-with-the-dte-object"></a>DTE オブジェクトを使用したコマンドの追加  
 マークアップとコードの両方で、開始ページから DTE オブジェクトにアクセスできます。  
  
 マークアップでは、 [バインディングマークアップ拡張](https://msdn.microsoft.com/library/83d6e2a4-1b0c-4fc8-bd96-b5e98800ab63) 構文を使用してオブジェクトを呼び出すことによってアクセスでき <xref:EnvDTE.DTE> ます。 この方法を使用して、コレクションを返すような単純なプロパティにバインドすることはできますが、メソッドまたはサービスにバインドすることはできません。 次の例は、 <xref:System.Windows.Controls.TextBlock> プロパティにバインドするコントロール <xref:EnvDTE._DTE.Name%2A> と、 <xref:System.Windows.Controls.ListBox> <xref:EnvDTE.Window.Caption%2A> プロパティによって返されるコレクションのプロパティを列挙するコントロールを示して <xref:EnvDTE._DTE.Windows%2A> います。  
  
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
  
 例については、「 [チュートリアル: スタートページへのユーザー設定の保存](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [スタート ページへのユーザー コントロールの追加](../extensibility/adding-user-control-to-the-start-page.md)
