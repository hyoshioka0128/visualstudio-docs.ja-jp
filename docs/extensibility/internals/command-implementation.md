---
title: コマンドの実装 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, implementation
ms.assetid: c782175c-cce4-4bd0-8374-4a897ceb1b3d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c7a536120c81c154cf894717a2af6a4e048d56e2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709576"
---
# <a name="command-implementation"></a>コマンドの実装
VSPackage でコマンドを実装するには、次のタスクを実行する必要があります。

1. *vsct*ファイルで、コマンド グループを設定し、コマンドを追加します。 詳細については、「 [Visual Studio コマンド テーブル (.vsct) ファイル 」](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)を参照してください。

2. コマンドを Visual Studio に登録します。

3. コマンドを実装します。

次のセクションでは、コマンドの登録方法と実装方法について説明します。

## <a name="register-commands-with-visual-studio"></a>コマンドを Visual Studio で登録する
 コマンドをメニューに表示する場合は、VSPackage<xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute>にを追加し、メニューの名前またはそのリソース ID の値として使用する必要があります。

```
[ProvideMenuResource("Menus.ctmenu", 1)]
...
    public sealed class MyPackage : Package
    {.. ..}

```

 また、コマンドを<xref:Microsoft.VisualStudio.Shell.OleMenuCommandService>. このサービスは、VSPackage が<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A>から<xref:Microsoft.VisualStudio.Shell.Package>派生している場合にメソッドを使用して取得できます。

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
 コマンドを実装するには、いくつかの方法があります。 静的メニュー コマンド (常に同じメニューに表示されるコマンド) が必要な場合は、前のセクションの例に<xref:System.ComponentModel.Design.MenuCommand>示すように、コマンドを作成します。 静的コマンドを作成するには、コマンドの実行を担当するイベント ハンドラーを指定する必要があります。 コマンドは常に有効で表示されるため、Visual Studio にその状態を提供する必要はありません。 特定の条件に応じてコマンドの状態を変更する場合は、<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>そのコマンドをクラスのインスタンスとして作成し、そのコンストラクターで、コマンドを実行するイベント ハンドラーと、コマンドの状態が`QueryStatus`変更されたときに Visual Studio に通知するハンドラーを提供します。 コマンド クラスの<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>一部として実装することも、プロジェクトの一部として<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>コマンドを提供する場合は実装することもできます。 2 つのインターフェイスと<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>クラスには、コマンドの状態の変更を Visual Studio に通知するメソッドと、コマンドの実行を提供するその他のメソッドがあります。

 コマンドがコマンド サービスに追加されると、コマンド のチェーンの 1 つになります。 コマンドの状態通知および実行メソッドを実装する場合は、その特定のコマンドのみを提供し、他のすべてのケースをチェーン内の他のコマンドに渡す必要があります。 コマンドを渡すことができない場合 (通常は戻る<xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED>)、Visual Studio が正常に動作しなくなることがあります。

## <a name="querystatus-methods"></a>メソッド
 メソッドまたは<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A><xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A>メソッドを実装する場合は、コマンドが属するコマンド セットの GUID とコマンドの ID を確認します。 次のガイドラインに従ってください。

- GUID が認識されない場合は、どちらのメソッドの実装もを<xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_UNKNOWNGROUP>返す必要があります。

- どちらかのメソッドの実装が GUID を認識するが、コマンドを実装していない場合、メソッドは返<xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED>す必要があります。

- どちらかのメソッドの実装が GUID とコマンドの両方を認識する場合、メソッドは次`prgCmds`<xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF>のフラグを使用して、(パラメーター内の) すべてのコマンドの command-flags フィールドを設定する必要があります。

  - `OLECMDF_SUPPORTED`: コマンドはサポートされています。

  - `OLECMDF_INVISIBLE`: コマンドは表示できません。

  - `OLECMDF_LATCHED`: コマンドがオンに切り替わって、チェックが入ったように見えます。

  - `OLECMDF_ENABLED`: コマンドが有効です。

  - `OLECMDF_DEFHIDEONCTXTMENU`: ショートカット メニューに表示されている場合は、コマンドを非表示にする必要があります。

  - `OLECMDF_NINCHED`: コマンドはメニュー コントローラであり、有効ではありませんが、ドロップダウン メニュー リストは空で、まだ使用できます。 (このフラグはめったに使用されません。

- コマンドが *.vsct*ファイルで定義されている場合は`TextChanges`、次のパラメーターを設定します。

  - パラメータの`rgwz`要素を`pCmdText`コマンドの新しいテキストに設定します。

  - パラメーターの`cwActual`要素を`pCmdText`コマンド文字列のサイズに設定します。

また、コマンドが特にオートメーション関数を処理することを意図していない限り、現在のコンテキストがオートメーション関数ではないことを確認してください。

特定のコマンドをサポートしていることを示すには、<xref:Microsoft.VisualStudio.VSConstants.S_OK>を返します。 その他のすべてのコマンドについては、<xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED>を返します。

次の例では、`QueryStatus`メソッドはまずコンテキストがオートメーション関数ではないことを確認し、次に正しいコマンド セット GUID とコマンド ID を検索します。 コマンド自体は、有効に設定され、サポートされます。 他のコマンドはサポートされていません。

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
 メソッドの実装`Exec`は、メソッドの実装に`QueryStatus`似ています。 まず、コンテキストがオートメーション関数でないことを確認します。 次に、GUID とコマンド ID の両方をテストします。 GUID またはコマンド ID が認識されない場合<xref:Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_NOTSUPPORTED>は、 を返します。

 コマンドを処理するには、コマンドを実行し<xref:Microsoft.VisualStudio.VSConstants.S_OK>、実行が成功した場合に返します。 コマンドはエラーの検出と通知を行います。したがって、実行が失敗した場合はエラー コードを返します。 実行メソッドを実装する方法を次の例に示します。

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

- [VSPackages がユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
