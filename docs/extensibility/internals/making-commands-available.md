---
title: コマンドを使用可能にする |マイクロソフトドキュメント
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
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2d64df85516e0a1ac326f8d40558755718c4644c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707335"
---
# <a name="making-commands-available"></a>コマンドを使用可能にする

複数の VS パッケージが Visual Studio に追加されると、ユーザー インターフェイス (UI) がコマンドで混雑することがあります。 次のように、この問題を軽減するためにパッケージをプログラムできます。

- パッケージは、ユーザーが必要としている場合にのみ読み込まれるようにプログラムします。

- 統合開発環境 (IDE) の現在の状態のコンテキストで必要とされる場合にのみ、そのコマンドが表示されるようにパッケージをプログラムします。

## <a name="delayed-loading"></a>遅延ローディング

遅延読み込みを有効にする一般的な方法は、コマンドが UI に表示されるように VSPackage を設計することですが、ユーザーがコマンドのいずれかをクリックするまでパッケージ自体は読み込まれません。 これを実現するには、.vsct ファイルで、コマンド フラグを持たないコマンドを作成します。

次の例は、.vsct ファイルからのメニュー コマンドの定義を示しています。 これは、テンプレートのメニュー コマンド オプションが選択されている場合に Visual Studio パッケージ テンプレートによって生成される**コマンド**です。

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

この例では、親グループの`MyMenuGroup`が **[ツール]** メニューなどのトップレベル メニューの子である場合、コマンドはそのメニューに表示されますが、コマンドを実行するパッケージは、ユーザーがクリックするまで読み込まれません。 ただし、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>インターフェイスを実装するコマンドをプログラミングすることで、コマンドを含むメニューが最初に展開されたときにパッケージを読み込むようにできます。

読み込みが遅れると、起動のパフォーマンスが向上する場合もあります。

## <a name="current-context-and-the-visibility-of-commands"></a>現在のコンテキストとコマンドの可視性

VSPackage データの現在の状態または現在関連するアクションに応じて、表示または非表示にする VSPackage コマンドをプログラムできます。 通常は、インターフェイスからメソッドの実装を使用して、VSPackage を有効にしてコマンドの<xref:EnvDTE.IDTCommandTarget.QueryStatus%2A>状態を<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>設定できますが、コードを実行する前に VSPackage を読み込む必要があります。 代わりに、パッケージをロードせずにコマンドの表示を管理する IDE を有効にすることをお勧めします。 これを行うには、.vsct ファイルで、1 つ以上の特殊な UI コンテキストにコマンドを関連付けます。 これらの UI コンテキストは、 コマンド コンテキスト*GUID*と呼ばれる GUID によって識別されます。

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]プロジェクトの読み込みや編集からビルドへの変更など、ユーザーの操作に起因する変更を監視します。 変更が発生すると、IDE の外観が自動的に変更されます。 次の表は、監視する IDE 変更の[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]4 つの主要なコンテキストを示しています。

| コンテキストのタイプ | 説明 |
|-------------------------| - |
| アクティブなプロジェクトの種類 | ほとんどのプロジェクトの種類では、`GUID`この値は、プロジェクトを実装する VSPackage の GUID と同じです。 ただし、[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]プロジェクトでは、値として`GUID`プロジェクトの種類を使用します。 |
| アクティブ ウィンドウ | 通常、これは、キー バインドの現在の UI コンテキストを確立する最後のアクティブなドキュメント ウィンドウです。 ただし、内部 Web ブラウザーのようなキー バインド テーブルを持つツール ウィンドウである場合もあります。 HTML エディターなどの複数タブのドキュメント ウィンドウでは、各タブには異なるコマンド コンテキスト`GUID`があります。 |
| アクティブ言語サービス | テキスト エディターに現在表示されているファイルに関連付けられている言語サービス。 |
| アクティブなツール ウィンドウ | 開いていてフォーカスのあるツール ウィンドウ。 |

5 番目の主要なコンテキスト領域は、IDE の UI 状態です。 UI コンテキストは、次のようにアクティブな`GUID`コマンド コンテキスト s によって識別されます。

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

これらの GUID は、IDE の現在の状態に応じてアクティブまたは非アクティブとしてマークされます。 複数の UI コンテキストを同時にアクティブにできます。

### <a name="hide-and-display-commands-based-on-context"></a>コンテキストに基づいてコマンドを表示/非表示にする

パッケージ自体をロードせずに、IDE でパッケージコマンドを表示または非表示にできます。 これを行うには、パッケージの .vsct`DefaultDisabled`ファイルで、コマンド フラグ 、`DefaultInvisible`および`DynamicVisibility`コマンド フラグを使用して、1 つ以上の[VisibilityItem](../../extensibility/visibilityitem-element.md)要素を[VisibilityConstraints](../../extensibility/visibilityconstraints-element.md)セクションに追加して、コマンドを定義します。 指定したコマンド コンテキスト`GUID`がアクティブになると、パッケージを読み込まずにコマンドが表示されます。

### <a name="custom-context-guids"></a>カスタム コンテキスト GUID

適切なコマンド コンテキスト GUID が定義されていない場合は、VSPackage で定義し、コマンドの表示を制御するために必要に応じてアクティブまたは非アクティブにプログラムできます。 サービスを<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>使用して、次の場合に使用します。

- コンテキスト GUID を登録します (<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCmdUIContextCookie%2A>メソッドを呼び出します)。

- (メソッドを呼び出`GUID`すことによって) コンテキスト<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>の状態を取得します。

- コンテキスト`GUID`をオンまたはオフにします(メソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.SetCmdUIContext%2A>呼び出します)。

    > [!CAUTION]
    > 他の VSPackage が依存する可能性があるため、VSPackage が既存のコンテキスト GUID の状態に影響を与えないことを確認します。

## <a name="example"></a>例

次の例では、VSPackage コマンドは、コマンド コンテキストによって管理されているコマンドの動的な可視性を示します。

このコマンドは、ソリューションが存在する場合は常に有効に設定され、表示されます。つまり、次のいずれかのコマンド コンテキスト GUID がアクティブである場合は常に、次のコマンド コンテキスト GUID がアクティブになります。

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.EmptySolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasMultipleProjects_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasSingleProject_guid>

この例では、すべてのコマンド フラグが個別の[コマンド フラグ](../../extensibility/command-flag-element.md)要素であることに注意してください。

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

また、次のように、すべての UI コンテキストを個別`VisibilityItem`の要素で指定する必要があることにも注意してください。

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

- [ソリューション エクスプローラーのツール バーにコマンドを追加する](../../extensibility/adding-a-command-to-the-solution-explorer-toolbar.md)
- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Vspackage のコマンド ルーティング](../../extensibility/internals/command-routing-in-vspackages.md)
- [メニュー項目の動的な追加](../../extensibility/dynamically-adding-menu-items.md)
