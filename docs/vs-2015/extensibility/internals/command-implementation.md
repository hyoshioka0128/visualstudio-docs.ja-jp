---
title: コマンドの実装 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands, implementation
ms.assetid: c782175c-cce4-4bd0-8374-4a897ceb1b3d
caps.latest.revision: 25
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a208fabd3d205793763698cde0f6fe367c7bb8b5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68195055"
---
# <a name="command-implementation"></a>コマンドの実装
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

VSPackage でコマンドを実装するには、次のタスクを実行する必要があります。  
  
1. . Vsct ファイルで、コマンドグループを設定し、コマンドを追加します。 詳細については、「 [Visual Studio コマンドテーブル ()」を参照してください。Vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)  
  
2. コマンドを Visual Studio に登録します。  
  
3. コマンドを実装します。  
  
   次のセクションでは、コマンドを登録して実装する方法について説明します。  
  
## <a name="registering-commands-with-visual-studio"></a>Visual Studio へのコマンドの登録  
 メニューにコマンドが表示されるようにするには、を <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> VSPackage に追加し、メニューの名前またはそのリソース ID の値としてを使用する必要があります。  
  
```  
[ProvideMenuResource("Menus.ctmenu", 1)]  
...  
    public sealed class MyPackage : Package  
    {.. ..}  
  
```  
  
 また、コマンドをに登録する必要があり <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> ます。 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A>VSPackage がから派生している場合は、メソッドを使用してこのサービスを取得でき <xref:Microsoft.VisualStudio.Shell.Package> ます。  
  
```  
OleMenuCommandService mcs = GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
if ( null != mcs )  
{  
    // Create the command for the menu item.  
    CommandID menuCommandID = new CommandID(guidCommandGroup, myCommandID);  
    MenuCommand menuItem = new MenuCommand(MenuItemCallback, menuCommandID );  
    mcs.AddCommand( menuItem );  
}  
  
```  
  
## <a name="implementing-commands"></a>コマンドの実装  
 コマンドを実装する方法はいくつかあります。 常に同じように表示されるコマンドである静的メニューコマンドが必要な場合は、 <xref:System.ComponentModel.Design.MenuCommand> 前のセクションの例に示すように、を使用してコマンドを作成します。 静的コマンドを作成するには、コマンドの実行を担当するイベントハンドラーを指定する必要があります。 コマンドは常に有効で表示されているため、Visual Studio にその状態を指定する必要はありません。 特定の条件に応じてコマンドの状態を変更する場合は、クラスのインスタンスとしてコマンドを作成 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> し、そのコンストラクターで、コマンドを実行するためのイベントハンドラーと、コマンドの状態が変化したときに Visual Studio に通知するためのクエリ状態ハンドラーを指定します。 を <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> コマンドクラスの一部として実装することも、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> プロジェクトの一部としてコマンドを提供する場合にを実装することもできます。 2つのインターフェイスと <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> クラスにはすべて、コマンドの状態の変化を Visual Studio に通知するメソッドと、コマンドの実行を提供するその他のメソッドがあります。  
  
 コマンドがコマンドサービスに追加されると、コマンドのチェーンの1つになります。 コマンドの状態通知と実行メソッドを実装する場合は、その特定のコマンドだけを指定し、その他のすべてのケースをチェーン内の他のコマンドに渡すように注意してください。 コマンドをに渡すことができない場合 (通常はを返し <xref:Microsoft.VisualStudio.OLE.Interop.Constants> ます)、Visual Studio は正常に動作しなくなる可能性があります。  
  
## <a name="query-status-methods"></a>クエリの状態メソッド  
 メソッドまたはメソッドのいずれかを実装する場合は、コマンド <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> が属するコマンドセットの GUID とコマンドの ID を確認します。 次のガイドラインに従ってください。  
  
- GUID が認識されない場合、いずれかのメソッドの実装はを返す必要があり <xref:Microsoft.VisualStudio.OLE.Interop.Constants> ます。  
  
- いずれかのメソッドの実装で GUID が認識されていても、実際にはコマンドが実装されていない場合、メソッドはを返す必要があり <xref:Microsoft.VisualStudio.OLE.Interop.Constants> ます。  
  
- どちらのメソッドの実装でも GUID とコマンドの両方が認識される場合、メソッドは、次のフラグを使用して、(パラメーター内の) すべてのコマンドのコマンドフラグフィールドを設定する必要があり `prgCmds` ます。  
  
  - <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> コマンドがサポートされている場合は。  
  
  - <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> コマンドを表示しない場合は。  
  
  - <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> コマンドがオンになっていて、チェックされているかどうかを示します。  
  
  - <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> コマンドが有効な場合は。  
  
  - <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> ショートカットメニューにコマンドが表示されている場合に、コマンドを非表示にする必要がある場合は。  
  
  - <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> コマンドがメニューコントローラーであり、が有効になっておらず、ドロップダウンメニューリストが空ではなく、引き続き使用可能な場合。 (このフラグはほとんど使用されません)。  
  
- コマンドがフラグを使用して. vsct ファイルで定義されている場合は `TextChanges` 、次のパラメーターを設定します。  
  
  - `rgwz`パラメーターの要素 `pCmdText` をコマンドの新しいテキストに設定します。  
  
  - `cwActual`パラメーターの要素 `pCmdText` をコマンド文字列のサイズに設定します。  
  
  また、コマンドが明示的にオートメーション関数を処理するように設定されていない限り、現在のコンテキストがオートメーション関数でないことを確認してください。  
  
  特定のコマンドをサポートしていることを示すには、を返し <xref:Microsoft.VisualStudio.VSConstants.S_OK> ます。 それ以外のすべてのコマンドについては、を返し <xref:Microsoft.VisualStudio.OLE.Interop.Constants> ます。  
  
  次の例では、最初にクエリの状態メソッドによってコンテキストがオートメーション関数でないことが確認され、次に正しいコマンドセット GUID とコマンド ID が検出されます。 コマンド自体は、enabled および supported に設定されています。 他のコマンドはサポートされていません。  
  
```  
public int QueryStatus(ref Guid pguidCmdGroup, uint cCmds, OLECMD[] prgCmds, IntPtr pCmdText)  
{  
    if (!VsShellUtilities.IsInAutomationFunction(m_provider.ServiceProvider))  
    {  
        if (pguidCmdGroup == VSConstants.VSStd2K && cCmds > 0)  
        {  
            // make the Right command visible   
            if ((uint)prgCmds[0].cmdID == (uint)VSConstants.VSStd2KCmdID.RIGHT)  
            {  
                prgCmds[0].cmdf = (int)Microsoft.VisualStudio.OLE.Interop.Constants.MSOCMDF_ENABLED | (int)Microsoft.VisualStudio.OLE.Interop.Constants.MSOCMDF_SUPPORTED;  
                return VSConstants.S_OK;  
            }  
        }  
        return Constants.OLECMDERR_E_NOTSUPPORTED;  
    }  
}  
  
```  
  
## <a name="execution-methods"></a>実行メソッド  
 Execute メソッドの実装は、query status メソッドの実装に似ています。 まず、コンテキストがオートメーション関数ではないことを確認します。 次に、GUID とコマンド ID の両方をテストします。 GUID またはコマンド ID が認識されない場合は、を返し <xref:Microsoft.VisualStudio.OLE.Interop.Constants> ます。  
  
 コマンドを処理するには、コマンドを実行して <xref:Microsoft.VisualStudio.VSConstants.S_OK> 、実行が成功した場合はを返します。 コマンドは、エラーの検出と通知を行います。そのため、実行が失敗した場合は、エラーコードを返します。 次の例は、実行メソッドを実装する方法を示しています。  
  
```  
public int Exec(ref Guid pguidCmdGroup, uint nCmdID, uint nCmdexecopt, IntPtr pvaIn, IntPtr pvaOut)  
{  
    if (!VsShellUtilities.IsInAutomationFunction(m_provider.ServiceProvider))  
    {  
        if (pguidCmdGroup == VSConstants.GUID_VSStandardCommandSet97)  
        {  
             if (nCmdID ==(uint) uint)VSConstants.VSStd2KCmdID.RIGHT)  
            {  
                //execute the command  
                return VSConstants.S_OK;  
            }  
        }  
    }  
    return Constants.OLECMDERR_E_NOTSUPPORTED;  
}  
  
```  
  
## <a name="see-also"></a>参照  
 [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
