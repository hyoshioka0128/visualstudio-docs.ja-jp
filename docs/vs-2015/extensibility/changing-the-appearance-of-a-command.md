---
title: コマンドの外観を変更する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands, changing appearance
- menu commands, changing appearance
- menus, changing command appearance
ms.assetid: da2474fa-f92d-4e9e-b8bf-67c61bf249c2
caps.latest.revision: 24
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4741059410e052c571d77088b9cbe109fb651642
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184506"
---
# <a name="changing-the-appearance-of-a-command"></a>コマンドの外観の変更
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コマンドの外観を変更することで、ユーザーにフィードバックを提供できます。 たとえば、使用できなくなったときに、コマンドの外観を変更することができます。 コマンドを使用できるようにするか、使用できないようにするか、メニューの表示と非表示を切り替えることができます。  
  
 コマンドの外観を変更するには、次のいずれかの操作を実行します。  
  
- コマンドテーブルファイルのコマンド定義で、適切なフラグを指定します。  
  
- サービスを使用し <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> ます。  
  
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>インターフェイスを実装し、未加工のコマンドオブジェクトを変更します。  
  
  次の手順では、Managed Package Framework (MPF) を使用してコマンドの外観を検索および更新する方法について説明します。  
  
### <a name="to-change-the-appearance-of-a-menu-command"></a>メニューコマンドの外観を変更するには  
  
1. [メニューコマンドのテキストを変更](../extensibility/changing-the-text-of-a-menu-command.md)する手順に従って、という名前のメニュー項目を作成 `New Text` します。  
  
2. ChangeMenuText.cs ファイルで、次の using ステートメントを追加します。  
  
    ```csharp  
    using System.Security.Permissions;  
    ```  
  
3. ChangeMenuTextPackageGuids.cs ファイルに、次の行を追加します。  
  
    ```csharp  
    public const string guidChangeMenuTextPackageCmdSet= "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file  
    ```  
  
4. ChangeMenuText.cs ファイルで、ShowMessageBox メソッドのコードを次のコードに置き換えます。  
  
    ```csharp  
    private void ShowMessageBox(object sender, EventArgs e)  
    {  
        var command = sender as OleMenuCommand;  
        if (command.Text == "New Text")  
            ChangeMyCommand(command.CommandID.ID, false);}  
    }  
    ```  
  
5. オブジェクトから更新するコマンドを取得 <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> し、コマンドオブジェクトの適切なプロパティを設定します。 たとえば、次のメソッドは、指定されたコマンドを VSPackage コマンドセットから使用可能または使用できない状態にします。 次のコードでは、メニュー項目が `New Text` クリックされた後に使用できなくなります。  
  
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
        return cmdUpdated;    }  
    }  
    ```  
  
6. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。  
  
7. [ **ツール** ] メニューの [ **ChangeMenuText の呼び出し** ] をクリックします。 この時点で、コマンド名は **Invoke ChangeMenuText**であるため、コマンドハンドラーは ChangeMyCommand () を呼び出しません。  
  
8. [ **ツール** ] メニューに、 **新しいテキスト**が表示されます。 [ **新しいテキスト**] をクリックします。 これで、コマンドが淡色表示されます。  
  
## <a name="see-also"></a>参照  
 [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)   
 [Vspackage のユーザーインターフェイス要素の追加方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)   
 [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
