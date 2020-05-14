---
title: ソリューションでのプロジェクトの読み込みの管理 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, managing project loading
ms.assetid: 097c89d0-f76a-4aaf-ada9-9a778bd179a0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 21cd5e7e557e795db49aea7a14e8e4cc7caa0422
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702732"
---
# <a name="manage-project-loading-in-a-solution"></a>ソリューションでのプロジェクトの読み込みを管理する
Visual Studio ソリューションには、多数のプロジェクトを含めることができます。 既定の Visual Studio の動作では、ソリューションが開かれた時点でソリューション内のすべてのプロジェクトが読み込まれ、すべてのプロジェクトの読み込みが完了するまで、ユーザーがどのプロジェクトにもアクセスできないようにします。 プロジェクトの読み込みプロセスが 2 分以上続くと、読み込まれたプロジェクトの数とプロジェクトの合計数を示す進行状況バーが表示されます。 ユーザーは複数のプロジェクトを含むソリューションで作業しているときにプロジェクトをアンロードできますが、この手順には、アンロードされたプロジェクトがソリューションの再構築コマンドの一部としてビルドされず、閉じているプロジェクトの型とメンバーの IntelliSense の説明は表示されないといういくつかの欠点があります。

 開発者は、ソリューションの読み込み時間を短縮し、ソリューション の読み込みマネージャーを作成することでプロジェクトの読み込み動作を管理できます。 ソリューションの読み込みマネージャーは、バックグラウンド ビルドを開始する前にプロジェクトが読み込まれるようにし、他のバックグラウンド タスクが完了するまでバックグラウンドの読み込みを遅延させ、他のプロジェクトの負荷管理タスクを実行できます。

## <a name="create-a-solution-load-manager"></a>ソリューション の読み込みマネージャーを作成します。
 開発者は、ソリューション の読み込<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager>みマネージャーがアクティブであることを Visual Studio を実装して助言することで、ソリューション の読み込みマネージャーを作成できます。

### <a name="activate-a-solution-load-manager"></a>ソリューションの読み込みマネージャーをアクティブ化する
 Visual Studio では、一度に 1 つのソリューション 読み込みマネージャーしか使用できるため、ソリューション の読み込みマネージャーをアクティブ化する場合は、Visual Studio に通知する必要があります。 2 番目のソリューションの読み込みマネージャーが後でアクティブ化された場合、ソリューションの負荷マネージャーは切断されます。

 サービスを取得し<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>、__VSPROPID4を設定する必要があります[。VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>)プロパティ:

```csharp
IVsSolution pSolution = GetService(typeof(SVsSolution)) as IVsSolution;
object objLoadMgr = this;   //the class that implements IVsSolutionManager
pSolution.SetProperty((int)__VSPROPID4.VSPROPID_ActiveSolutionLoadManager, objLoadMgr);
```

 この<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager.OnDisconnect%2A>メソッドは、Visual Studio がシャットダウンされるとき、または別のパッケージが__VSPROPID4を呼び出すことによってアクティブなソリューション の<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.SetProperty%2A>読み込みマネージャーとして引き継がれたときに呼び出されます[。VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>)プロパティ。

#### <a name="strategies-for-different-kinds-of-solution-load-manager"></a>さまざまな種類のソリューション・ロード・マネージャーの戦略
 ソリューション・ロード・マネージャーは、管理するソリューションのタイプに応じて、さまざまな方法で実装できます。

 ソリューションの読み込みマネージャーは、一般的にソリューションの読み込みを管理する場合、VSPackage の一部として実装できます。 VSPackage の値<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute><xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionOpening_guid>を . ソリューションのロード マネージャーは<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>、メソッドでアクティブ化できます。

> [!NOTE]
> パッケージの自動読み込みの詳細については、「 [VSPackages の読み込み](../extensibility/loading-vspackages.md)」を参照してください。

 Visual Studio はアクティブ化される最後のソリューション の読み込みマネージャーのみを認識するため、一般的なソリューションの読み込みマネージャーは、アクティブ化する前に、常に既存の負荷マネージャーがあるかどうかを検出する必要があります。 __VSPROPID4の`GetProperty()`ソリューション サービスを呼び出す場合[。VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>)返`null`しますが、アクティブなソリューションの読み込みマネージャはありません。 null が返されない場合は、オブジェクトがソリューションの読み込みマネージャーと同じかどうかを確認します。

 ソリューションの読み込みマネージャーが、いくつかの種類のソリューションのみを管理する場合、VSPackage はソリューションの読み込み<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A>イベントをサブスクライブ (呼び<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A>出し) し、イベント ハンドラーを使用してソリューション の読み込みマネージャーをアクティブ化できます。

 ソリューションの負荷マネージャーが特定のソリューションのみを管理する場合は、ソリューションの前のセクションを呼び出<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A>すことによって、アクティブ化情報をソリューション ファイルの一部として保持できます。

 他のソリューションのロード マネージャーと競合<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents.OnAfterCloseSolution%2A>しないように、特定のソリューションの読み込みマネージャーは、イベント ハンドラーで自分自身を非アクティブ化する必要があります。

 ソリューション の負荷マネージャーがグローバル プロジェクトの読み込みプロパティ (たとえば、[オプション] ページで設定されたプロパティ) を永続化するためだけに必要<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A>な場合は、イベント ハンドラーでソリューション の読み込みマネージャーをアクティブにし、ソリューション プロパティで設定を保持し、ソリューション の読み込みマネージャーを非アクティブ化します。

## <a name="handle-solution-load-events"></a>ソリューションの読み込みイベントを処理する
 ソリューションの読み込みイベントを<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A>サブスクライブするには、ソリューションの読み込みマネージャーをアクティブ化するときに呼び出します。 を実装<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents>すると、さまざまなプロジェクト読み込みプロパティに関連するイベントに応答できます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A>: このイベントは、ソリューションが開かれる前に発生します。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeBackgroundSolutionLoadBegins%2A>: このイベントは、ソリューションが完全に読み込まれた後、バックグラウンド プロジェクトの読み込みが再開される前に発生します。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterBackgroundSolutionLoadComplete%2A>: このイベントは、ソリューションの読み込みマネージャーが存在するかどうかに関係なく、ソリューションが最初に完全に読み込まれた後に発生します。 また、ソリューションが完全に読み込まれるたびに、バックグラウンド読み込みまたは需要の読み込み後に起動されます。 同時に、<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExistsAndFullyLoaded_guid>再アクティブ化されます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnQueryBackgroundLoadProjectBatch%2A>: このイベントは、プロジェクト (またはプロジェクト) の読み込み前に発生します。 プロジェクトが読み込まれる前に他のバックグラウンド プロセスが完了していることを`pfShouldDelayLoadToNextIdle`確認するには **、true**に設定します。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeLoadProjectBatch%2A>: このイベントは、プロジェクトのバッチが読み込まれようとしているときに発生します。 true`fIsBackgroundIdleBatch`の場合、プロジェクトはバックグラウンドで読み込まれます。false`fIsBackgroundIdleBatch`の場合、ユーザーがソリューション エクスプローラーで保留中のプロジェクトを展開した場合など、ユーザーの要求の結果としてプロジェクトが同期的に読み込まれます。 このイベントを処理して、それ以外の<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A>場合は で行う必要がある高価な作業を行うことができます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterLoadProjectBatch%2A>: このイベントは、プロジェクトのバッチが読み込まれた後に発生します。

## <a name="detect-and-manage-solution-and-project-loading"></a>ソリューションとプロジェクトの読み込みを検出および管理する
 プロジェクトおよびソリューションのロード状態を検出するには、次の値<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProperty%2A>を指定して呼び出します。

- [__VSPROPID4。VSPROPID_IsSolutionFullyLoaded](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsSolutionFullyLoaded>) `var` :`true`ソリューションとそのすべてのプロジェクトが読み込まれている場合`false`は返されます。

- [__VSPROPID4。VSPROPID_IsInBackgroundIdleLoadProjectBatch](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsInBackgroundIdleLoadProjectBatch>) `var` :`true`プロジェクトのバッチが現在バックグラウンドで読み込まれている場合は`false`返されます。

- [__VSPROPID4。VSPROPID_IsInSyncDemandLoadProjectBatch](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsInSyncDemandLoadProjectBatch>) `var` :`true`ユーザー コマンドまたはその他の明示的な読み込みの結果として、プロジェクトのバッチが同期的に読`false`み込まれている場合は、その他の場合は返します。

- [__VSPROPID2。VSPROPID_IsSolutionClosing](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2.VSPROPID_IsSolutionClosing>) `var` :`true`ソリューションが現在閉じられている場合は返`false`します。

- [__VSPROPID。VSPROPID_IsSolutionOpening](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID.VSPROPID_IsSolutionOpening>) `var` :`true`ソリューションが現在開いている場合は返`false`します。

次のいずれかのメソッドを呼び出して、プロジェクトとソリューションが読み込まれるようにすることもできます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureSolutionIsLoaded%2A>: このメソッドを呼び出すと、メソッドが返される前に、ソリューション内のプロジェクトが強制的に読み込まれます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectIsLoaded%2A>: このメソッドを呼び出`guidProject`すと、メソッドが返される前にプロジェクトが強制的に読み込まれます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectsAreLoaded%2A>: このメソッドを呼び出`guidProjectID`すと、メソッドが返される前にプロジェクトが強制的に読み込まれます。
