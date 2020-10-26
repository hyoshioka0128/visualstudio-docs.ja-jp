---
title: メニューコマンドのテキストを変更する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- menus, changing text
- text, menus
- commands, changing text
ms.assetid: 5cb676a0-c6e2-47e5-bd2b-133dc8842e46
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d8fd3fc01a5dd3e10e633b876b719695d6b26c18
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184490"
---
# <a name="changing-the-text-of-a-menu-command"></a>メニュー コマンドのテキストの変更
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

次の手順は、サービスを使用してメニューコマンドのテキストラベルを変更する方法を示して <xref:System.ComponentModel.Design.IMenuCommandService> います。  
  
## <a name="changing-a-menu-command-label-with-the-imenucommandservice"></a>IMenuCommandService を使用してメニューコマンドのラベルを変更する  
  
1. `MenuText` **ChangeMenuText**という名前のメニューコマンドを使用して、という名前の VSIX プロジェクトを作成します。 詳細については、「 [メニューコマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。  
  
2. Vstc ファイルで、 `TextChanges` 次の例に示すように、メニューコマンドにフラグを追加します。  
  
    ```xml  
    <Button guid="guidChangeMenuTextPackageCmdSet" id="ChangeMenuTextId" priority="0x0100" type="Button">  
        <Parent guid="guidChangeMenuTextPackageCmdSet" id="MyMenuGroup" />  
        <Icon guid="guidImages" id="bmpPic1" />  
        <CommandFlag>TextChanges</CommandFlag>  
        <Strings>  
            <ButtonText>Invoke ChangeMenuText</ButtonText>  
        </Strings>  
    </Button>  
    ```  
  
3. ChangeMenuText.cs ファイルで、メニューコマンドが表示される前に呼び出されるイベントハンドラーを作成します。  
  
    ```csharp  
    private void OnBeforeQueryStatus(object sender, EventArgs e)  
    {  
        var myCommand = sender as OleMenuCommand;  
        if (null != myCommand)  
        {  
            myCommand.Text = "New Text";  
                    }  
    }  
    ```  
  
     また、オブジェクトの、、の各プロパティを変更することで、このメソッドのメニューコマンドの状態を更新することもでき <xref:System.ComponentModel.Design.MenuCommand.Visible%2A> <xref:System.ComponentModel.Design.MenuCommand.Checked%2A> <xref:System.ComponentModel.Design.MenuCommand.Enabled%2A> <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> ます。  
  
4. ChangeMenuText コンストラクターで、元のコマンド初期化と配置コードを、メニューコマンドを表す (ではなく) を作成するコードに置き換えて、 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> `MenuCommand` イベントハンドラーを追加し、メニューコマンド <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> をメニューコマンドサービスに渡します。  
  
     次のようになります。  
  
    ```csharp  
    private ChangeMenuText(Package package)  
    {  
        if (package == null)  
        {  
            throw new ArgumentNullException(nameof(package));  
        }  
  
        this.package = package;  
  
        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
        if (commandService != null)  
        {  
            CommandID menuCommandID = new CommandID(MenuGroup, CommandId);  
            EventHandler eventHandler = this.ShowMessageBox;  
            OleMenuCommand menuItem = new OleMenuCommand(ShowMessageBox, menuCommandID);  
            menuItem.BeforeQueryStatus +=  
                new EventHandler(OnBeforeQueryStatus);  
            commandService.AddCommand(menuItem);  
        }  
    }  
    ```  
  
5. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。  
  
6. [ **ツール** ] メニューに、 **Invoke ChangeMenuText**という名前のコマンドが表示されます。  
  
7. コマンドをクリックします。 MenuItemCallback が呼び出されたことを示すメッセージボックスが表示されます。 メッセージボックスを閉じると、[ツール] メニューのコマンドの名前が **新しいテキスト**になっていることがわかります。
