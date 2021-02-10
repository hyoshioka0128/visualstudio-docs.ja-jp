---
title: コマンドの実装 |Microsoft Docs
description: Visual Studio でのコマンドの実装、VSPackage でコマンドグループを設定する方法、コマンドを追加する方法、コマンドを登録する方法、および実装する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, implementation
ms.assetid: c782175c-cce4-4bd0-8374-4a897ceb1b3d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2031fd74a10c8725157908eaa906c1963a477526
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99940112"
---
# <a name="command-implementation"></a>コマンドの実装
VSPackage でコマンドを実装するには、次のタスクを実行する必要があります。

1. *. Vsct* ファイルで、コマンドグループを設定し、コマンドを追加します。 詳細については、「 [Visual Studio コマンドテーブル (vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)」を参照してください。

2. コマンドを Visual Studio に登録します。

3. コマンドを実装します。

次のセクションでは、コマンドを登録して実装する方法について説明します。

## <a name="register-commands-with-visual-studio"></a>Visual Studio でのコマンドの登録
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

## <a name="implement-commands"></a>コマンドの実装
 コマンドを実装する方法はいくつかあります。 常に同じように表示されるコマンドである静的メニューコマンドが必要な場合は、 <xref:System.ComponentModel.Design.MenuCommand> 前のセクションの例に示すように、を使用してコマンドを作成します。 静的コマンドを作成するには、コマンドの実行を担当するイベントハンドラーを指定する必要があります。 コマンドは常に有効で表示されているため、Visual Studio にその状態を指定する必要はありません。 特定の条件に応じてコマンドの状態を変更する場合は、クラスのインスタンスとしてコマンドを作成 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> し、そのコンストラクターで、コマンドを実行するためのイベントハンドラーと、 `QueryStatus` コマンドの状態が変化したときに Visual Studio に通知するハンドラーを指定します。 を <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> コマンドクラスの一部として実装することも、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> プロジェクトの一部としてコマンドを提供する場合にを実装することもできます。 2つのインターフェイスと <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> クラスにはすべて、コマンドの状態の変化を Visual Studio に通知するメソッドと、コマンドの実行を提供するその他のメソッドがあります。

 コマンドがコマンドサービスに追加されると、コマンドのチェーンの1つになります。 コマンドの状態通知と実行メソッドを実装する場合は、その特定のコマンドだけを指定し、その他のすべてのケースをチェーン内の他のコマンドに渡すように注意してください。 コマンドをに渡すことができない場合 (通常はを返し <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> ます)、Visual Studio は正常に動作しなくなる可能性があります。

## <a name="querystatus-methods"></a>QueryStatus メソッド
 メソッドまたはメソッドのいずれかを実装する場合は、コマンド <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> が属するコマンドセットの GUID とコマンドの ID を確認します。 次のガイドラインに従ってください。

- GUID が認識されない場合、いずれかのメソッドの実装はを返す必要があり <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_UNKNOWNGROUP> ます。

- いずれかのメソッドの実装で GUID が認識されていても、コマンドが実装されていない場合、メソッドはを返す必要があり <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> ます。

- どちらのメソッドの実装でも GUID とコマンドの両方が認識される場合、メソッドは、次のフラグを使用して、(パラメーター内の) すべてのコマンドのコマンドフラグフィールドを設定する必要があり `prgCmds` <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> ます。

  - `OLECMDF_SUPPORTED`: コマンドがサポートされています。

  - `OLECMDF_INVISIBLE`: コマンドを表示することはできません。

  - `OLECMDF_LATCHED`: コマンドが切り替わり、オンになっているように見えます。

  - `OLECMDF_ENABLED`: コマンドが有効になっています。

  - `OLECMDF_DEFHIDEONCTXTMENU`: ショートカットメニューに表示されている場合は、コマンドを非表示にする必要があります。

  - `OLECMDF_NINCHED`: コマンドがメニューコントローラーであり、有効になっていませんが、ドロップダウンメニューリストが空ではなく、引き続き使用できます。 (このフラグはほとんど使用されません)。

- コマンドがフラグを使用して *. vsct* ファイルで定義されている場合は `TextChanges` 、次のパラメーターを設定します。

  - `rgwz`パラメーターの要素 `pCmdText` をコマンドの新しいテキストに設定します。

  - `cwActual`パラメーターの要素 `pCmdText` をコマンド文字列のサイズに設定します。

また、コマンドがオートメーション関数を処理することを意図していない限り、現在のコンテキストがオートメーション関数でないことを確認してください。

特定のコマンドをサポートしていることを示すには、を返し <xref:Microsoft.VisualStudio.VSConstants.S_OK> ます。 それ以外のすべてのコマンドについては、を返し <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> ます。

次の例では、 `QueryStatus` メソッドは最初にコンテキストがオートメーション関数でないことを確認し、次に正しいコマンドセット GUID とコマンド ID を検索します。 コマンド自体は、enabled および supported に設定されています。 他のコマンドはサポートされていません。

```csharp
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
 メソッドの実装は `Exec` 、メソッドの実装に似て `QueryStatus` います。 まず、コンテキストがオートメーション関数ではないことを確認します。 次に、GUID とコマンド ID の両方をテストします。 GUID またはコマンド ID が認識されない場合は、を返し <xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED> ます。

 コマンドを処理するには、コマンドを実行して <xref:Microsoft.VisualStudio.VSConstants.S_OK> 、実行が成功した場合はを返します。 コマンドは、エラーの検出と通知を行います。そのため、実行が失敗した場合は、エラーコードを返します。 次の例は、実行メソッドを実装する方法を示しています。

```csharp
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

## <a name="see-also"></a>関連項目

- [Vspackage のユーザーインターフェイス要素の追加方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
