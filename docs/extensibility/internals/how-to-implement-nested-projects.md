---
title: '方法 : 入れ子になったプロジェクトを実装する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- nested projects, implementing
- projects [Visual Studio SDK], nesting
ms.assetid: d20b8d6a-f0e0-4115-b3a3-edda893ae678
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8d9dfe567db0b8788b93b13aeb760d45f4c05b57
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707982"
---
# <a name="how-to-implement-nested-projects"></a>方法 : 入れ子になったプロジェクトを実装する

入れ子になったプロジェクトの種類を作成する場合、追加の手順を実装する必要があります。 親プロジェクトは、入れ子になった (子) プロジェクトに対してソリューションが持つのと同じ責任の一部を担います。 親プロジェクトは、ソリューションに似たプロジェクトのコンテナーです。 特に、入れ子になったプロジェクトの階層を構築するために、ソリューションと親プロジェクトによって発生する必要があるいくつかのイベントがあります。 これらのイベントは、入れ子になったプロジェクトを作成するための次のプロセスで説明されています。

## <a name="create-nested-projects"></a>入れ子になったプロジェクトを作成する

1. 統合開発環境 (IDE) は、インターフェイスを呼び出すことによって、親プロジェクトのプロジェクト<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>ファイルとスタートアップ情報を読み込みます。 親プロジェクトが作成され、ソリューションに追加されます。

    > [!NOTE]
    > この時点では、親プロジェクトを作成するプロセスの初期の作業は、親プロジェクトを作成する前に親プロジェクトを作成する必要があるためです。 このシーケンスに従って、親プロジェクトは子プロジェクトに設定を適用でき、子プロジェクトは必要に応じて親プロジェクトから情報を取得できます。 このシーケンスは、ソース コード管理 (SCC) や**ソリューション エクスプローラ**などのクライアントが必要とする場合です。

     親プロジェクトは、IDE が<xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren%2A>メソッドを呼び出すのを待ってから、入れ子になった (子) プロジェクトを作成する必要があります。

2. IDE は`QueryInterface`、親プロジェクトを<xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject>を 呼び出します。 この呼び出しが成功すると、親<xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren%2A>プロジェクトのすべての入れ子になったプロジェクトを開く親のメソッドが呼び出されます。

3. 親プロジェクトは、メソッド<xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnBeforeOpeningChildren%2A>を呼び出して、入れ子になったプロジェクトが作成されることをリスナーに通知します。 たとえば、SCC は、ソリューションとプロジェクトの作成プロセスの手順が順番に発生しているかどうかを知るために、これらのイベントをリッスンしています。 手順が正しく動作しない場合、ソリューションがソース コード管理に正しく登録されていない可能性があります。

4. 親プロジェクトは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AddVirtualProject%2A>それぞれの子プロジェクト<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AddVirtualProjectEx%2A>でメソッドまたはメソッドを呼び出します。

     `AddVirtualProject`メソッドに渡<xref:Microsoft.VisualStudio.Shell.Interop.__VSADDVPFLAGS>すと、仮想 (入れ子になった) プロジェクトをプロジェクト ウィンドウに追加し、ビルドから除外し、ソース コード管理に追加するなどのことを示します。 `VSADDVPFLAGS`ネストされたプロジェクトの表示設定を制御し、そのプロジェクトに関連付けられている機能を示すことができます。

     親プロジェクトのプロジェクト ファイルに格納されているプロジェクト GUID を持つ既存の子プロジェクトを再ロードすると、親プロジェクト`AddVirtualProjectEx`が呼び出されます。 と`AddVirtualProject``AddVirtualProjectEX`の唯一の違`AddVirtualProjectEX`いは、親プロジェクトが子プロジェクトのインスタンス`guidProjectID`ごとに有効<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProjectOfGuid%2A>にし、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProjectOfProjref%2A>正常に機能するように指定できるようにするパラメータを持つ点です。

     新しい入れ子になったプロジェクトを追加する場合など、使用できる GUID がない場合、ソリューションは、親に追加されたときにプロジェクトの GUID を作成します。 プロジェクト ファイル内でそのプロジェクト GUID を永続化するのは、親プロジェクトの役割です。 入れ子になったプロジェクトを削除すると、そのプロジェクトの GUID も削除できます。

5. IDE は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren>親プロジェクトの各子プロジェクトでメソッドを呼び出します。

     プロジェクトを入れ子`IVsParentProject`にする場合は、親プロジェクトを実装する必要があります。 しかし、親プロジェクトは、`QueryInterface`その`IVsParentProject`下に親プロジェクトがあっても呼び出すことはありません。 ソリューションは、呼び出`IVsParentProject`しを処理し、それが実装されている場合`OpenChildren`は、入れ子になったプロジェクトを作成する呼び出しを処理します。 `AddVirtualProjectEX`は 常に`OpenChildren`から呼び出されます。 階層作成イベントを順番に維持するために、親プロジェクトによって呼び出されることはありません。

6. IDE は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A>子プロジェクトのメソッドを呼び出します。

7. 親プロジェクトは、親<xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnAfterOpeningChildren%2A>の子プロジェクトが作成されたことをリスナーに通知するメソッドを呼び出します。

8. IDE は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnAfterOpenProject%2A>すべての子プロジェクトが開かれた後、親プロジェクトのメソッドを呼び出します。

     存在しない場合、親プロジェクトは、 を呼び出`CoCreateGuid`して入れ子になった各プロジェクトの GUID を作成します。

    > [!NOTE]
    > `CoCreateGuid`は、GUID が作成されるときに呼び出される COM API です。 詳細については、MSDN`CoCreateGuid`ライブラリの「GUID」を参照してください。

     親プロジェクトは、この GUID をプロジェクト ファイルに格納し、次回 IDE で開いたときに取得されます。 子プロジェクトの を取得`AddVirtualProjectEX`するための 呼び出しに関`guidProjectID`する詳細については、ステップ 4 を参照してください。

9. メソッド<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>は、親 ItemID に対して呼び出され、このメソッドは、入れ子になったプロジェクトに委譲する規則によって呼び出されます。 親<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>で呼び出されたときに委任するプロジェクトを入れ子にするノードのプロパティを取得します。

     親プロジェクトと子プロジェクトはプログラムによってインスタンス化されるため、この時点で入れ子になったプロジェクトのプロパティを設定できます。

    > [!NOTE]
    > ネストされたプロジェクトからコンテキスト情報を受け取るだけでなく、__VSHPROPIDをチェックして、親プロジェクトにその項目のコンテキストがあるかどうかを確認することもできます[。VSHPROPID_UserContext](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_UserContext>). このようにして、個々のネストされたプロジェクトに固有のダイナミックヘルプ属性とメニューオプションを追加できます。

10. 階層は、メソッドの呼び出しを**使用してソリューション**<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetNestedHierarchy%2A>エクスプローラーに表示するために構築されます。

     階層を環境`GetNestedHierarchy`に渡して、ソリューション エクスプローラーに表示する階層を構築します。 このようにして、ソリューションはプロジェクトが存在することを認識し、ビルド マネージャーによってビルドを管理できる、またはプロジェクト内のファイルをソース コード管理下に置くことを許可できます。

11. Project1 のすべての入れ子になったプロジェクトが作成されると、コントロールがソリューションに渡され、Project2 のプロセスが繰り返されます。

     入れ子になったプロジェクトを作成する場合と同じプロセスが、子プロジェクトを持つ子プロジェクトに対して発生します。 この場合、プロジェクト 1 の子である BuildProject1 に子プロジェクトがある場合、それらはビルドプロジェクト1の後と Project2 の前に作成されます。 プロセスは再帰的で、階層は上から下に構築されます。

     ユーザーがソリューションまたは特定のプロジェクト自体を閉じたために、入れ子になったプロジェクトが閉じられた場合は`IVsParentProject`、<xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.CloseChildren%2A>の他のメソッドが呼び出されます。 親プロジェクトは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.RemoveVirtualProject%2A>メソッドの呼び出<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeClosingChildren%2A>しを、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterClosingChildren%2A>およびメソッドを使用して、入れ子になったプロジェクトが閉じられていることをソリューション イベントにリスナーに通知するメソッドと共にラップします。

以下のトピックでは、入れ子になったプロジェクトを実装するときに考慮すべきその他の概念について説明します。

- [入れ子になったプロジェクトのアンロードと再ロードに関する考慮事項](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)
- [入れ子になったプロジェクトのウィザードサポート](../../extensibility/internals/wizard-support-for-nested-projects.md)
- [入れ子になったプロジェクトのコマンド処理を実装する](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)
- [入れ子になったプロジェクトの [AddItem] ダイアログ ボックスをフィルタ処理する](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)

## <a name="see-also"></a>関連項目

- [[新しい項目の追加] ダイアログ ボックスに項目を追加する](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [プロジェクトおよび項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [チェックリスト: 新しいプロジェクトの種類を作成する](../../extensibility/internals/checklist-creating-new-project-types.md)
- [コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)
- [ウィザード (.vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
