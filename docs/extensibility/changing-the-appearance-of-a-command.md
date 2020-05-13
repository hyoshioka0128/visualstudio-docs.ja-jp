---
title: コマンドの外観を変更する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, changing appearance
- menu commands, changing appearance
- menus, changing command appearance
ms.assetid: da2474fa-f92d-4e9e-b8bf-67c61bf249c2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 653f516dda89f4895b8d19d77f7f49bf9c6aa45b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739853"
---
# <a name="change-the-appearance-of-a-command"></a>コマンドの外観を変更する
コマンドの外観を変更することで、ユーザーにフィードバックを提供できます。 たとえば、コマンドが使用できない場合に、コマンドの外観を変える場合があります。 コマンドを使用したり、使用できなくなったり、表示または非表示にしたり、メニューでオンまたはオフにしたりできます。

コマンドの外観を変更するには、次のいずれかの操作を実行します。

- コマンド・テーブル・ファイルのコマンド定義で適切なフラグを指定します。

- サービスを<xref:Microsoft.VisualStudio.Shell.OleMenuCommandService>使用します。

- インターフェイスを<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>実装し、生のコマンド オブジェクトを変更します。

  次の手順では、マネージ パッケージ フレームワーク (MPF) を使用してコマンドの外観を検索および更新する方法を示します。

### <a name="to-change-the-appearance-of-a-menu-command"></a>メニュー コマンドの外観を変更するには

1. メニュー コマンドの[テキストを変更するの手順に](../extensibility/changing-the-text-of-a-menu-command.md)従って、 という名前`New Text`のメニュー項目を作成します。

2. *ChangeMenuText.cs*ファイルに次の using ステートメントを追加します。

    ```csharp
    using System.Security.Permissions;
    ```

3. *ChangeMenuTextPackageGuids.cs*ファイルに次の行を追加します。

    ```csharp
    public const string guidChangeMenuTextPackageCmdSet= "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file
    ```

4. *ChangeMenuText.cs*ファイルで、ShowMessageBox メソッドのコードを次のように置き換えます。

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        var command = sender as OleMenuCommand;
        if (command.Text == "New Text")
            ChangeMyCommand(command.CommandID.ID, false);
    }
    ```

5. オブジェクトから更新するコマンドを<xref:Microsoft.VisualStudio.Shell.OleMenuCommandService>取得し、コマンド オブジェクトに適切なプロパティを設定します。 たとえば、次のメソッドは、VSPackage コマンド セットから指定されたコマンドを使用または使用できるようにします。 次のコードは、メニュー項目を`New Text`クリックした後に使用できない状態にします。

    ```csharp
    public bool ChangeMyCommand(int cmdID, bool enableCmd)
    {
        bool cmdUpdated = false;
        var mcs = this.ServiceProvider.GetService(typeof(IMenuCommandService))
            as OleMenuCommandService;
        var newCmdID = new CommandID(new Guid(ChangeMenuTextPackageGuids.guidChangeMenuTextPackageCmdSet), cmdID);
        MenuCommand mc = mcs.FindCommand(newCmdID);
        if (mc != null)
        {
            mc.Enabled = enableCmd;
            cmdUpdated = true;
        }
        return cmdUpdated;
    }
    ```

6. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。

7. [**ツール**] メニューの [**メニューテキストの呼び出し**] をクリックします。 この時点で、コマンド名は **[ChangeMenuText の呼び出し**] なので、コマンド ハンドラは**ChangeMyCommand()** を呼び出しません。

8. [**ツール**] メニューに **[新しいテキスト]** が表示されます。 [**新しいテキスト**] をクリックします。 コマンドはグレー表示されます。

## <a name="see-also"></a>関連項目
- [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)
- [VSPackages がユーザー インターフェイス要素を追加する方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)
- [コマンド テーブル (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
