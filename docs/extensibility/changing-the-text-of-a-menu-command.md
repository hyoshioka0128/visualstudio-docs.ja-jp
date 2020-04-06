---
title: メニュー コマンドのテキストを変更する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus, changing text
- text, menus
- commands, changing text
ms.assetid: 5cb676a0-c6e2-47e5-bd2b-133dc8842e46
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ff6af7bdd64342e86201af79dbe5c7968b247d6b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739848"
---
# <a name="change-the-text-of-a-menu-command"></a>メニュー コマンドのテキストを変更する
次の手順は、サービスを使用してメニュー コマンドのテキスト ラベルを<xref:System.ComponentModel.Design.IMenuCommandService>変更する方法を示しています。

## <a name="changing-a-menu-command-label-with-the-imenucommandservice"></a>メニュー コマンド ラベルを変更する

1. という名前のメニュー コマンド`MenuText`で名前を付けた VSIX プロジェクト**を作成します**。 詳細については、「[メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

2. *vsct*ファイルで、次の`TextChanges`例に示すように、メニュー コマンドにフラグを追加します。

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

3. *ChangeMenuText.cs*ファイルで、メニュー コマンドが表示される前に呼び出されるイベント ハンドラーを作成します。

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

    オブジェクトの プロパティ<xref:System.ComponentModel.Design.MenuCommand.Visible%2A>、 、<xref:System.ComponentModel.Design.MenuCommand.Checked%2A>および<xref:System.ComponentModel.Design.MenuCommand.Enabled%2A>プロパティを変更して、このメソッドのメニュー コマンドの<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>状態を更新することもできます。

4. ChangeMenuText コンストラクターで、元のコマンド初期化コードと配置コードを、メニュー コマンド<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>を表す`MenuCommand`( ではなく ) を作成する<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>コードに置き換え、イベント ハンドラーを追加し、メニュー コマンド をメニュー コマンド サービスに渡します。

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

6. [**ツール**] メニューに[**変更メニューテキストの呼び出し**]というコマンドが表示されます。

7. コマンドをクリックします。 メッセージ ボックスが表示され **、MenuItemCallback**が呼び出されたことを通知するメッセージ ボックスが表示されます。 メッセージ ボックスを閉じると、[ツール] メニューのコマンドの名前が **[新しいテキスト]** になっていることがわかります。
