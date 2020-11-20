---
title: 複数インスタンスのツールウィンドウを作成する |Microsoft Docs
description: ツールウィンドウを変更して、複数のインスタンスを同時に開くことができるようにする方法について説明します。 既定では、ツールウィンドウで開くことができるインスタンスは1つだけです。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- multi
- tool windows
ms.assetid: 4a7872f1-acc9-4f43-8932-5a526b36adea
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 10de60620bcd0b56f251955f478d4d06c984d021
ms.sourcegitcommit: 5027eb5c95e1d2da6d08d208fd6883819ef52d05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94973994"
---
# <a name="create-a-multi-instance-tool-window"></a>複数インスタンスのツールウィンドウを作成する
ツールウィンドウをプログラミングして、複数のインスタンスを同時に開くことができるようにすることができます。 既定では、ツールウィンドウで開くことができるインスタンスは1つだけです。

複数インスタンスのツールウィンドウを使用すると、複数の関連する情報ソースを同時に表示できます。 たとえば、複数のインスタンスのツールウィンドウに複数行のコントロールを配置して、 <xref:System.Windows.Forms.TextBox> プログラミングセッション中に複数のコードスニペットを同時に使用できるようにすることができます。 また、たとえば、複数 <xref:System.Windows.Forms.DataGrid> インスタンスのツールウィンドウにコントロールとドロップダウンリストボックスを配置して、複数のリアルタイムデータソースを同時に追跡できるようにすることもできます。

## <a name="create-a-basic-single-instance-tool-window"></a>基本 (単一インスタンス) ツールウィンドウを作成する

1. VSIX テンプレートを使用して **MultiInstanceToolWindow** という名前のプロジェクトを作成し、 **MIToolWindow** という名前のカスタムツールウィンドウ項目テンプレートを追加します。

    > [!NOTE]
    > ツールウィンドウを使用した拡張機能の作成の詳細については、「 [ツールウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。

## <a name="make-a-tool-window-multi-instance"></a>ツールウィンドウを複数インスタンスにする

1. *MIToolWindowPackage.cs* ファイルを開き、属性を見つけ `ProvideToolWindow` ます。 次の `MultiInstances=true` 例に示すように、パラメーターとパラメーターを指定します。

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
        [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About
        [ProvideMenuResource("Menus.ctmenu", 1)]
        [ProvideToolWindow(typeof(MultiInstanceToolWindow.MIToolWindow), MultiInstances = true)]
        [Guid(MIToolWindowPackage.PackageGuidString)]
        public sealed class MIToolWindowPackage : Package
    {. . .}
    ```

2. *MIToolWindowCommand.cs* ファイルで、メソッドを見つけ `ShowToolWindos()` ます。 このメソッドでは、メソッドを呼び出し、 <xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> その `create` フラグをに設定し `false` ます。これにより、使用可能なが見つかるまで、既存のツールウィンドウインスタンスが反復処理されるようになり `id` ます。

3. ツールウィンドウのインスタンスを作成するには、メソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> て、 `id` を使用可能な値に設定し、 `create` フラグをに設定し `true` ます。

    既定で `id` は、メソッドのパラメーターの値 <xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A> は `0` です。 この値により、単一インスタンスのツールウィンドウが作成します。 複数のインスタンスをホストするには、すべてのインスタンスが独自の一意である必要があり `id` ます。

4. <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> ツールウィンドウインスタンスのプロパティによって返されるオブジェクトに対してメソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.ToolWindowPane.Frame%2A> ます。

5. 既定では、 `ShowToolWindow` ツールウィンドウ項目テンプレートによって作成されたメソッドによって、単一インスタンスのツールウィンドウが作成されます。 次の例は、メソッドを変更して複数のインスタンスを作成する方法を示して `ShowToolWindow` います。

    ```csharp
    private void ShowToolWindow(object sender, EventArgs e)
    {
        for (int i = 0; i < 10; i++)
        {
            ToolWindowPane window = this.package.FindToolWindow(typeof(MIToolWindow), i, false);
            if (window == null)
            {
                // Create the window with the first free ID.
                window = (ToolWindowPane)this.package.FindToolWindow(typeof(MIToolWindow), i, true);
                if ((null == window) || (null == window.Frame))
                {
                    throw new NotSupportedException("Cannot create tool window");
                }

            IVsWindowFrame windowFrame = (IVsWindowFrame)window.Frame;
            Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(windowFrame.Show());
            break;
            }
        }
    }
    ```
