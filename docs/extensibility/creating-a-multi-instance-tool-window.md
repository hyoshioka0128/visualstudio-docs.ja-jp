---
title: マルチインスタンス ツール ウィンドウを作成する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- multi
- tool windows
ms.assetid: 4a7872f1-acc9-4f43-8932-5a526b36adea
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 33585f623f846e16200d430ad2c886fe0874b537
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739627"
---
# <a name="create-a-multi-instance-tool-window"></a>マルチインスタンス ツール ウィンドウを作成する
ツール ウィンドウをプログラムして、複数のインスタンスを同時に開くことができます。 既定では、ツール ウィンドウで開くことができるインスタンスは 1 つだけです。

複数インスタンスツール ウィンドウを使用すると、関連する複数の情報ソースを同時に表示できます。 たとえば、複数行<xref:System.Windows.Forms.TextBox>のコントロールを複数インスタンス のツール ウィンドウに配置して、プログラミング セッション中に複数のコード スニペットを同時に使用できるようにすることができます。 また、複数のリアルタイム データ ソース<xref:System.Windows.Forms.DataGrid>を同時に追跡できるように、複数のインスタンスのツール ウィンドウにコントロールとドロップダウン リスト ボックスを配置することもできます。

## <a name="create-a-basic-single-instance-tool-window"></a>基本的な (単一インスタンス) ツール ウィンドウを作成する

1. VSIX テンプレートを使用して**MultiInstanceToolWindow**という名前のプロジェクトを作成し **、MIToolWindow**という名前のカスタム ツール ウィンドウ項目テンプレートを追加します。

    > [!NOTE]
    > ツール ウィンドウを使用した拡張機能の作成の詳細については、「ツール[ウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。

## <a name="make-a-tool-window-multi-instance"></a>ツール ウィンドウをマルチインスタンスにする

1. *MIToolWindowPackage.cs*ファイルを開き、属性`ProvideToolWindow`を見つけます。 次の`MultiInstances=true`例に示すように、パラメーターを使用します。

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
        [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About
        [ProvideMenuResource("Menus.ctmenu", 1)]
        [ProvideToolWindow(typeof(MultiInstanceToolWindow.MIToolWindow), MultiInstances = true)]
        [Guid(MIToolWindowPackage.PackageGuidString)]
        public sealed class MIToolWindowPackage : Package
    {. . .}
    ```

2. *MIToolWindowCommand.cs*ファイルで、メソッドを`ShowToolWindos()`見つけます。 このメソッドでは、メソッドを<xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A>呼び出し`create`、その`false`フラグを設定して、使用可能なインスタンスが見つかるまで既存の`id`ツール ウィンドウ インスタンスを反復処理します。

3. ツール ウィンドウ インスタンスを作成するには、<xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A>メソッドを呼び`id`出し、使用可能な値`create`に設定`true`し、フラグを に設定します。

    既定では、メソッドの`id`パラメーターの<xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A>値は`0`です。 この値は、単一インスタンスのツール ウィンドウになります。 複数のインスタンスをホストするには、すべてのインスタンスに固有の`id`.

4. ツール<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A>ウィンドウ インスタンス<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>の<xref:Microsoft.VisualStudio.Shell.ToolWindowPane.Frame%2A>プロパティによって返されるオブジェクトのメソッドを呼び出します。

5. 既定では、ツール`ShowToolWindow`ウィンドウ項目テンプレートによって作成されるメソッドは、単一インスタンスのツール ウィンドウを作成します。 次の例は、メソッドを変更`ShowToolWindow`して複数のインスタンスを作成する方法を示しています。

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
