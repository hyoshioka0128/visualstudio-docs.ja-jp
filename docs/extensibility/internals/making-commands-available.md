---
title: コマンドを使用できるようにする |Microsoft Docs
description: 遅延読み込み、コンテキスト、および可視性を使用して、Vspackage で Visual Studio IDE に追加されるコマンドの可用性を制御する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- menus [Visual Studio SDK], commands
- best practices, menu and toolbar commands
- toolbars [Visual Studio], best practices
- menu commands, best practices
ms.assetid: 3ffc4312-c6db-4759-a946-a4bb85f4a17a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4bb44fbb263bb12aba04c06f1248ae25aa9d546f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99839546"
---
# <a name="making-commands-available"></a>コマンドを使用できるようにする

複数の Vspackage が Visual Studio に追加されると、ユーザーインターフェイス (UI) がコマンドで過剰に使用されることがあります。 次のように、この問題を軽減するためにパッケージをプログラミングできます。

- ユーザーが必要としたときにのみ読み込まれるようにパッケージをプログラムします。

- 統合開発環境 (IDE: integrated development environment) の現在の状態のコンテキストで必要になる可能性がある場合にのみ、コマンドが表示されるようにパッケージをプログラミングします。

## <a name="delayed-loading"></a>遅延読み込み

遅延読み込みを有効にする一般的な方法は、UI にコマンドが表示されるように VSPackage をデザインすることですが、ユーザーがいずれかのコマンドをクリックするまでパッケージ自体は読み込まれません。 これを実現するには、vsct ファイルで、コマンドフラグを持たないコマンドを作成します。

次の例は、vsct ファイルからのメニューコマンドの定義を示しています。 これは、テンプレートの **[メニューコマンド** ] オプションが選択されている場合に Visual Studio パッケージテンプレートによって生成されるコマンドです。

```xml
<Button guid="guidTopLevelMenuCmdSet" id="cmdidTestCommand" priority="0x0100" type="Button">
  <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" />
  <Icon guid="guidImages" id="bmpPic1" />
  <Strings>
    <CommandName>cmdidTestCommand</CommandName>
    <ButtonText>Test Command</ButtonText>
  </Strings>
</Button>
```

この例では、親グループが [ `MyMenuGroup` **ツール** ] メニューなどのトップレベルメニューの子である場合、そのメニューにコマンドが表示されますが、コマンドを実行するパッケージは、ユーザーがコマンドをクリックするまで読み込まれません。 ただし、コマンドをプログラミングしてインターフェイスを実装することで、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> コマンドを含むメニューを最初に展開したときにパッケージを読み込むことができます。

遅延読み込みによって起動パフォーマンスが向上する場合もあることに注意してください。

## <a name="current-context-and-the-visibility-of-commands"></a>現在のコンテキストとコマンドの可視性

VSPackage データの現在の状態または現在の関連するアクションに応じて、表示または非表示にする VSPackage コマンドをプログラミングできます。 VSPackage を有効にすると、通常はインターフェイスからのメソッドの実装を使用して、コマンドの状態を設定できます。ただし、そのためには、 <xref:EnvDTE.IDTCommandTarget.QueryStatus%2A> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> コードを実行する前に VSPackage を読み込む必要があります。 代わりに、パッケージを読み込まずにコマンドの可視性を管理するように IDE を有効にすることをお勧めします。 これを行うには、vsct ファイルで、コマンドを1つ以上の特殊な UI コンテキストに関連付けます。 これらの UI コンテキストは、 *コマンドコンテキスト guid* と呼ばれる guid によって識別されます。

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクトの読み込み、編集、ビルドなどのユーザー操作によって発生した変更を監視します。 変更が発生すると、IDE の外観が自動的に変更されます。 次の表は、が監視する IDE 変更の主な4つのコンテキストを示して [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] います。

| コンテキストの種類 | Description |
|-------------------------| - |
| アクティブなプロジェクトの種類 | ほとんどの種類のプロジェクトで `GUID` は、この値は、プロジェクトを実装する VSPackage の GUID と同じになります。 ただし、プロジェクトでは、 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] プロジェクトの種類を `GUID` 値として使用します。 |
| アクティブウィンドウ | 通常、これは、キーバインドの現在の UI コンテキストを確立する最後のアクティブなドキュメントウィンドウです。 ただし、内部の Web ブラウザーに似たキーバインドテーブルを持つツールウィンドウである場合もあります。 HTML エディターなどの複数タブのドキュメントウィンドウでは、すべてのタブに異なるコマンドコンテキストがあり `GUID` ます。 |
| アクティブな言語サービス | テキストエディターで現在表示されているファイルに関連付けられている言語サービス。 |
| アクティブなツールウィンドウ | 開いているツールウィンドウでフォーカスがあります。 |

5番目の主要なコンテキスト領域は、IDE の UI 状態です。 UI コンテキストは、次のように、アクティブなコマンドコンテキストによって識別され `GUID` ます。

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionBuilding_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Debugging_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Dragging_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.FullScreenMode_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.DesignMode_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.NoSolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.EmptySolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasSingleProject_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasMultipleProjects_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.CodeWindow_guid>

これらの Guid は、IDE の現在の状態に応じて、アクティブまたは非アクティブとしてマークされます。 複数の UI コンテキストを同時にアクティブにすることができます。

### <a name="hide-and-display-commands-based-on-context"></a>コンテキストに基づいてコマンドを非表示にして表示する

パッケージ自体を読み込まずに、IDE でパッケージコマンドを表示または非表示にすることができます。 これを行うには、パッケージの vsct ファイルで `DefaultDisabled` 、、、およびの各コマンドフラグを使用し、 `DefaultInvisible` `DynamicVisibility` 1 つ以上の [VisibilityItem](../../extensibility/visibilityitem-element.md) 要素を [VisibilityConstraints](../../extensibility/visibilityconstraints-element.md) セクションに追加して、コマンドを定義します。 指定されたコマンドコンテキストがアクティブになると、 `GUID` パッケージを読み込まずにコマンドが表示されます。

### <a name="custom-context-guids"></a>カスタムコンテキスト Guid

適切なコマンドコンテキスト GUID がまだ定義されていない場合は、VSPackage で定義してから、コマンドの可視性を制御するために必要に応じてアクティブまたは非アクティブにするようにプログラムを設定できます。 サービスを使用して次のこと <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> を行います。

- (メソッドを呼び出すことによって) コンテキスト Guid を登録 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCmdUIContextCookie%2A> します。

- `GUID`(メソッドを呼び出すことによって) コンテキストの状態を取得 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A> します。

- コンテキストをオン `GUID` またはオフにします (メソッドを呼び出すことによって <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.SetCmdUIContext%2A> )。

    > [!CAUTION]
    > VSPackage が既存のコンテキスト GUID の状態に影響しないことを確認してください。これは、他の Vspackage が依存している可能性があるためです。

## <a name="example"></a>例

次の VSPackage コマンドの例は、VSPackage を読み込まずにコマンドコンテキストによって管理されるコマンドを動的に表示する方法を示しています。

このコマンドは、ソリューションが存在するときに有効になり、表示されるように設定されています。つまり、次のいずれかのコマンドコンテキスト Guid がアクティブになっているとします。

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.EmptySolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasMultipleProjects_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasSingleProject_guid>

この例では、すべてのコマンドフラグが個別の [コマンドフラグ](../../extensibility/command-flag-element.md) 要素であることに注意してください。

```xml
<Button guid="guidDynamicVisibilityCmdSet" id="cmdidMyCommand"
        priority="0x0100" type="Button">
  <Parent guid="guidDynamicVisibilityCmdSet" id="MyMenuGroup" />
  <Icon guid="guidImages" id="bmpPic1" />
  <CommandFlag>DefaultDisabled</CommandFlag>
  <CommandFlag>DefaultInvisible</CommandFlag>
  <CommandFlag>DynamicVisibility</CommandFlag>
  <Strings>
    <CommandName>cmdidMyCommand</CommandName>
    <ButtonText>My Command name</ButtonText>
  </Strings>
</Button>
```

また、次のように、すべての UI コンテキストに個別の要素を指定する必要があることにも注意し `VisibilityItem` てください。

```xml
<VisibilityConstraints>
  <VisibilityItem guid="guidDynamicVisibilityCmdSet"
                  id="cmdidMyCommand" context="UICONTEXT_EmptySolution" />
  <VisibilityItem guid="guidDynamicVisibilityCmdSet"
                      id="cmdidMyCommand" context="UICONTEXT_SolutionHasSingleProject" />
  <VisibilityItem guid="guidDynamicVisibilityCmdSet"
                  id="cmdidMyCommand" context="UICONTEXT_SolutionHasMultipleProjects" />
</VisibilityConstraints>
```

## <a name="see-also"></a>関連項目

- [ソリューションエクスプローラーツールバーにコマンドを追加する](../../extensibility/adding-a-command-to-the-solution-explorer-toolbar.md)
- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Vspackage のコマンド ルーティング](../../extensibility/internals/command-routing-in-vspackages.md)
- [メニュー項目の動的な追加](../../extensibility/dynamically-adding-menu-items.md)
