---
title: '方法: 入れ子になったプロジェクトを実装する |Microsoft Docs'
description: ソリューションおよび親プロジェクトからのイベントを発生させてプロジェクト階層を構築することにより、Visual Studio で入れ子になったプロジェクトを実装する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- nested projects, implementing
- projects [Visual Studio SDK], nesting
ms.assetid: d20b8d6a-f0e0-4115-b3a3-edda893ae678
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a1b02fca5d37d7e75cd7c32527bb09358425e626
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99932541"
---
# <a name="how-to-implement-nested-projects"></a>方法: 入れ子になったプロジェクトを実装する

入れ子になったプロジェクトの種類を作成する場合は、いくつかの追加の手順を実装する必要があります。 親プロジェクトは、その入れ子になった (子) プロジェクトに対してソリューションと同じ役割を担います。 親プロジェクトは、ソリューションに似たプロジェクトのコンテナーです。 特に、入れ子になったプロジェクトの階層を構築するために、ソリューションおよび親プロジェクトによって発生する必要があるいくつかのイベントがあります。 これらのイベントについては、入れ子になったプロジェクトを作成するための次のプロセスで説明します。

## <a name="create-nested-projects"></a>入れ子になったプロジェクトの作成

1. 統合開発環境 (IDE: integrated development environment) は、インターフェイスを呼び出すことによって、親プロジェクトのプロジェクトファイルとスタートアップ情報を読み込み <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory> ます。 親プロジェクトが作成され、ソリューションに追加されます。

    > [!NOTE]
    > この時点では、子プロジェクトを作成する前に親プロジェクトを作成する必要があるため、親プロジェクトが入れ子になったプロジェクトを作成するプロセスは早すぎます。 このシーケンスに従うと、親プロジェクトは設定を子プロジェクトに適用でき、子プロジェクトは必要に応じて親プロジェクトから情報を取得できます。 このシーケンスは、ソースコード管理 (SCC) や **ソリューションエクスプローラー** などのクライアントによってで必要とされる場合にあります。

     親プロジェクトは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren%2A> 入れ子になった (子) プロジェクトまたはプロジェクトを作成する前に、IDE によってメソッドが呼び出されるまで待機する必要があります。

2. IDE は、 `QueryInterface` の親プロジェクトでを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject> ます。 この呼び出しが成功した場合、IDE は親のメソッドを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren%2A> 親プロジェクトのすべての入れ子になったプロジェクトを開きます。

3. 親プロジェクトはメソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnBeforeOpeningChildren%2A> て、入れ子になったプロジェクトが作成されようとしていることをリスナーに通知します。 たとえば、SCC では、これらのイベントをリッスンして、ソリューションとプロジェクトの作成プロセスのステップが順番に実行されているかどうかを確認します。 順序が正しくない場合は、ソリューションがソースコード管理に正しく登録されていない可能性があります。

4. 親プロジェクトは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AddVirtualProject%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AddVirtualProjectEx%2A> それぞれの子プロジェクトに対してメソッドまたはメソッドを呼び出します。

     <xref:Microsoft.VisualStudio.Shell.Interop.__VSADDVPFLAGS>メソッドにを渡して、 `AddVirtualProject` 仮想 (入れ子になった) プロジェクトをプロジェクトウィンドウに追加し、ビルドから除外して、ソースコード管理に追加する必要があることを示します。 `VSADDVPFLAGS` 入れ子になったプロジェクトの表示を制御し、関連付けられている機能を示すことができます。

     プロジェクト GUID が親プロジェクトのプロジェクトファイルに格納されている既存の子プロジェクトを再度読み込むと、親プロジェクトはを呼び出し `AddVirtualProjectEx` ます。 との唯一の違いは、にはパラメーターがあり、これを使用すると、 `AddVirtualProject` `AddVirtualProjectEX` `AddVirtualProjectEX` 親プロジェクトで子プロジェクトが有効になり、 `guidProjectID` <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProjectOfGuid%2A> 正常に機能するように、インスタンスごとにを指定できるようになり <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProjectOfProjref%2A> ます。

     新しい入れ子になったプロジェクトを追加するときなど、使用可能な GUID がない場合、ソリューションは親に追加されたときにプロジェクト用にプロジェクトを作成します。 そのプロジェクトの GUID をプロジェクトファイルに保存するのは、親プロジェクトの役割です。 入れ子になったプロジェクトを削除すると、そのプロジェクトの GUID を削除することもできます。

5. IDE は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren> 親プロジェクトの各子プロジェクトでメソッドを呼び出します。

     プロジェクトを入れ子にする場合は、親プロジェクトでを実装する必要があり `IVsParentProject` ます。 ただし、親プロジェクト `QueryInterface` `IVsParentProject` がその下に親プロジェクトがある場合でも、親プロジェクトがを呼び出すことはありません。 ソリューションは、の呼び出しを処理し、 `IVsParentProject` 実装されている場合は、を呼び出して `OpenChildren` 入れ子になったプロジェクトを作成します。 `AddVirtualProjectEX` は常にから呼び出され `OpenChildren` ます。 階層作成イベントを順番に保持するために、親プロジェクトからは呼び出さないでください。

6. IDE は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> 子プロジェクトでメソッドを呼び出します。

7. 親プロジェクトは、メソッドを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnAfterOpeningChildren%2A> 親の子プロジェクトが作成されたことをリスナーに通知します。

8. IDE は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnAfterOpenProject%2A> すべての子プロジェクトが開かれた後に、親プロジェクトのメソッドを呼び出します。

     入れ子になっていない場合は、を呼び出すことによって、入れ子になった各プロジェクトの GUID が作成され `CoCreateGuid` ます。

    > [!NOTE]
    > `CoCreateGuid` は、GUID が作成されるときに呼び出される COM API です。 詳細については、MSDN ライブラリの「」および「Guid」を参照してください `CoCreateGuid` 。

     親プロジェクトは、この GUID を IDE で次に開いたときに取得されるプロジェクトファイルに格納します。 を呼び出して `AddVirtualProjectEX` 子プロジェクトのを取得する方法の詳細については、手順4を参照してください `guidProjectID` 。

9. 次に、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> 規則によって、入れ子になったプロジェクトにデリゲートするときに、親 ItemID に対してメソッドが呼び出されます。 は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> 親で呼び出されるときに、デリゲートするプロジェクトを入れ子にするノードのプロパティを取得します。

     親プロジェクトと子プロジェクトはプログラムによってインスタンス化されるため、この時点で入れ子になったプロジェクトのプロパティを設定できます。

    > [!NOTE]
    > 入れ子になったプロジェクトからコンテキスト情報を受け取るだけでなく、__VSHPROPID をチェックすることによって、親プロジェクトにその項目のコンテキストがあるかどうかを確認することもでき [ます。VSHPROPID_UserContext](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_UserContext>)。 このようにして、入れ子になった個々のプロジェクトに固有の追加の動的なヘルプ属性とメニューオプションを追加できます。

10. 階層は、メソッドを呼び出すことによって **ソリューションエクスプローラー** に表示するように構築されてい <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetNestedHierarchy%2A> ます。

     を使用して階層を環境に渡し、 `GetNestedHierarchy` ソリューションエクスプローラーに表示する階層を構築します。 この方法では、プロジェクトが存在し、ビルドマネージャーでビルドできるように管理できること、またはプロジェクト内のファイルをソースコード管理下に配置できることがソリューションによって認識されます。

11. Project1 の入れ子になったすべてのプロジェクトが作成されると、コントロールがソリューションに戻され、プロセスが Project2 に対して繰り返されます。

     入れ子になったプロジェクトを作成する場合も、子を持つ子プロジェクトに対して同じプロセスが実行されます。 この場合、Project1 の子である BuildProject1 には子プロジェクトがあったので、BuildProject1 と Project2 の前に作成されます。 プロセスは再帰的で、階層は上から順に構築されます。

     ユーザーがソリューションまたは特定のプロジェクト自体を閉じたために入れ子になったプロジェクトが閉じられると、のもう1つのメソッド `IVsParentProject` <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.CloseChildren%2A> が呼び出されます。 親プロジェクトは、メソッドの呼び出しをとメソッドでラップして、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.RemoveVirtualProject%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeClosingChildren%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterClosingChildren%2A> 入れ子になったプロジェクトが閉じられていることを示すソリューションイベントにリスナーに通知します。

次のトピックでは、入れ子になったプロジェクトを実装する際に考慮する必要があるいくつかの概念について説明します。

- [入れ子になったプロジェクトのアンロードと再読み込みに関する考慮事項](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)
- [入れ子になったプロジェクトに対するウィザードのサポート](../../extensibility/internals/wizard-support-for-nested-projects.md)
- [入れ子になったプロジェクトのコマンド処理を実装する](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)
- [入れ子になったプロジェクトの [AddItem] ダイアログボックスをフィルター処理する](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)

## <a name="see-also"></a>関連項目

- [[新しい項目の追加] ダイアログボックスへの項目の追加](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)
- [チェックリスト: 新しいプロジェクトの種類を作成する](../../extensibility/internals/checklist-creating-new-project-types.md)
- [コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)
- [ウィザード (.vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
