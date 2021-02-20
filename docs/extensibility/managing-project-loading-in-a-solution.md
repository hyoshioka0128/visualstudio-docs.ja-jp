---
title: ソリューションでのプロジェクトの読み込みの管理 |Microsoft Docs
description: ソリューションロードマネージャーを作成することによって、開発者がソリューションの読み込み時間を短縮し、プロジェクトの読み込み動作を管理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, managing project loading
ms.assetid: 097c89d0-f76a-4aaf-ada9-9a778bd179a0
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ca17eae2b4f21e9705788faa1a2371a066be6475
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99952162"
---
# <a name="manage-project-loading-in-a-solution"></a>ソリューションでのプロジェクトの読み込みの管理
Visual Studio ソリューションには、多数のプロジェクトを含めることができます。 Visual Studio の既定の動作では、ソリューションを開いたときにソリューション内のすべてのプロジェクトが読み込まれます。また、すべてのプロジェクトの読み込みが完了するまで、ユーザーはどのプロジェクトにもアクセスできません。 プロジェクトの読み込みプロセスが2分以上経過すると、読み込まれたプロジェクトの数とプロジェクトの合計数を示す進行状況バーが表示されます。 ユーザーは、複数のプロジェクトを含むソリューションで作業しているときにプロジェクトをアンロードできますが、この手順にはいくつかの欠点があります。アンロードされたプロジェクトは、リビルドソリューションコマンドの一部としてビルドされず、閉じられたプロジェクトの型とメンバーの IntelliSense 記述は表示されません。

 ソリューションロードマネージャーを作成することで、開発者はソリューションの読み込み時間を短縮し、プロジェクトの読み込み動作を管理できます。 ソリューションロードマネージャーでは、バックグラウンドビルドを開始する前にプロジェクトが読み込まれるようにしたり、他のバックグラウンドタスクが完了するまでバックグラウンド読み込みを遅らせたり、その他のプロジェクトの読み込み管理タスクを実行したりすることができます。

## <a name="create-a-solution-load-manager"></a>ソリューションロードマネージャーを作成する
 開発者は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager> ソリューションロードマネージャーがアクティブであることを Visual Studio に実装して通知することで、ソリューションロードマネージャーを作成できます。

### <a name="activate-a-solution-load-manager"></a>ソリューションロードマネージャーのアクティブ化
 Visual Studio では、一度に1つのソリューションロードマネージャーのみが許可されます。そのため、ソリューションロードマネージャーをアクティブ化する場合は、Visual Studio にアドバイスする必要があります。 2つ目のソリューションロードマネージャーを後でアクティブにすると、ソリューションロードマネージャーが切断されます。

 サービスを取得し、__VSPROPID4 を設定する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution> [ます。VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>) プロパティ:

```csharp
IVsSolution pSolution = GetService(typeof(SVsSolution)) as IVsSolution;
object objLoadMgr = this;   //the class that implements IVsSolutionManager
pSolution.SetProperty((int)__VSPROPID4.VSPROPID_ActiveSolutionLoadManager, objLoadMgr);
```

 メソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager.OnDisconnect%2A> Visual Studio がシャットダウンされているとき、または __VSPROPID4 を使用してを呼び出すことによって別のパッケージがアクティブソリューションロードマネージャーとして引き継がれたときに呼び出され <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.SetProperty%2A> [ます。VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>) プロパティです。

#### <a name="strategies-for-different-kinds-of-solution-load-manager"></a>さまざまな種類のソリューションロードマネージャーの戦略
 ソリューションロードマネージャーは、管理対象のソリューションの種類に応じて、さまざまな方法で実装できます。

 ソリューションロードマネージャーが一般にソリューションの読み込みを管理する場合は、VSPackage の一部として実装できます。 パッケージは、値がである VSPackage にを追加することによって、自動読み込みに設定する必要があり <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionOpening_guid> ます。 その後、ソリューションロードマネージャーをメソッドでアクティブ化でき <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> ます。

> [!NOTE]
> 自動読み込みパッケージの詳細については、「 [vspackage の読み込み](../extensibility/loading-vspackages.md)」を参照してください。

 Visual Studio では、最後にアクティブ化されるソリューションロードマネージャーのみが認識されるため、一般的なソリューションロードマネージャーでは、自身をアクティブ化する前に、既存のロードマネージャーがあるかどうかを常に検出する必要があります。 `GetProperty()`__VSPROPID4 のソリューションサービスでを呼び出す場合は[。VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>) `null` が返されると、アクティブなソリューションロードマネージャーが存在しません。 Null が返されない場合は、オブジェクトがソリューションロードマネージャーと同じであるかどうかを確認します。

 ソリューションロードマネージャーが、いくつかの種類のソリューションのみを管理するように設計されている場合、VSPackage はを呼び出すことによってソリューション読み込みイベントをサブスクライブ <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A> し、のイベントハンドラーを使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A> ソリューションロードマネージャーをアクティブ化できます。

 ソリューションロードマネージャーが特定のソリューションのみを管理するように指定されている場合、ソリューションファイルの一部としてアクティブ化情報を永続化するには、ソリューションの前のセクションを呼び出す必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A> ます。

 特定のソリューションロードマネージャーは <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents.OnAfterCloseSolution%2A> 、他のソリューションロードマネージャーと競合しないように、イベントハンドラーで自身を非アクティブ化する必要があります。

 グローバルプロジェクトの読み込みプロパティ (オプションページで設定されたプロパティなど) を永続化するためだけにソリューションロードマネージャーが必要な場合は、イベントハンドラーでソリューションロードマネージャーをアクティブ化し、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> ソリューションのプロパティで設定を永続化してから、ソリューションロードマネージャーを非アクティブ化することができます。

## <a name="handle-solution-load-events"></a>ソリューションの読み込みイベントの処理
 ソリューション読み込みイベントをサブスクライブするには、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A> ソリューションロードマネージャーをアクティブ化するときにを呼び出します。 を実装すると <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents> 、さまざまなプロジェクトの読み込みプロパティに関連するイベントに応答できます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A>: このイベントは、ソリューションが開かれる前に発生します。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeBackgroundSolutionLoadBegins%2A>: このイベントは、ソリューションが完全に読み込まれた後、バックグラウンドプロジェクトの読み込みが開始される前に発生します。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterBackgroundSolutionLoadComplete%2A>: このイベントは、ソリューションロードマネージャーがあるかどうかにかかわらず、ソリューションが最初に完全に読み込まれた後に発生します。 また、ソリューションが完全に読み込まれたときに、バックグラウンド読み込みまたは要求読み込みの後にも発生します。 同時に、が再 <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExistsAndFullyLoaded_guid> アクティブ化されます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnQueryBackgroundLoadProjectBatch%2A>: このイベントは、プロジェクト (またはプロジェクト) が読み込まれる前に発生します。 プロジェクトが読み込まれる前に他のバックグラウンドプロセスが完了するようにするには、を `pfShouldDelayLoadToNextIdle` **true** に設定します。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeLoadProjectBatch%2A>: このイベントは、プロジェクトのバッチが読み込まれるときに発生します。 `fIsBackgroundIdleBatch`が true の場合、プロジェクトはバックグラウンドで読み込まれます。が false の場合、ユーザーが `fIsBackgroundIdleBatch` ソリューションエクスプローラーで保留中のプロジェクトを展開するなど、ユーザー要求の結果としてプロジェクトが同期的に読み込まれます。 このイベントを処理して、で実行する必要がある高額な作業を行うことができ <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> ます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterLoadProjectBatch%2A>: このイベントは、プロジェクトのバッチが読み込まれた後に発生します。

## <a name="detect-and-manage-solution-and-project-loading"></a>ソリューションとプロジェクトの読み込みを検出して管理する
 プロジェクトとソリューションの読み込み状態を検出するには、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProperty%2A> 次の値を指定してを呼び出します。

- [__VSPROPID4。VSPROPID_IsSolutionFullyLoaded](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsSolutionFullyLoaded>): `var` `true` ソリューションとそのすべてのプロジェクトが読み込まれている場合はを返します。それ以外の場合はを返し `false` ます。

- [__VSPROPID4。VSPROPID_IsInBackgroundIdleLoadProjectBatch](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsInBackgroundIdleLoadProjectBatch>): `var` `true` プロジェクトのバッチが現在バックグラウンドで読み込まれている場合はを返します。それ以外の場合はを返し `false` ます。

- [__VSPROPID4。VSPROPID_IsInSyncDemandLoadProjectBatch](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsInSyncDemandLoadProjectBatch>): `var` `true` ユーザーコマンドまたはその他の明示的な読み込みの結果として、プロジェクトのバッチが現在同期的に読み込まれている場合はを返します。それ以外の場合はを返し `false` ます。

- [__VSPROPID2。VSPROPID_IsSolutionClosing](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2.VSPROPID_IsSolutionClosing>): `var` `true` ソリューションが現在閉じられている場合はを返します。それ以外の場合はを返し `false` ます。

- [__VSPROPID。VSPROPID_IsSolutionOpening](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID.VSPROPID_IsSolutionOpening>): `var` `true` ソリューションが現在開かれている場合はを返します。それ以外の場合はを返し `false` ます。

次のいずれかのメソッドを呼び出すことによって、プロジェクトとソリューションが読み込まれるようにすることもできます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureSolutionIsLoaded%2A>: このメソッドを呼び出すと、メソッドが返される前に、ソリューション内のプロジェクトが強制的に読み込まれます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectIsLoaded%2A>: このメソッドを呼び出すと、メソッドが返される前に、にプロジェクトが強制的に `guidProject` 読み込まれます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectsAreLoaded%2A>: このメソッドを呼び出すと、メソッドが返される前に、にプロジェクトが強制的に `guidProjectID` 読み込まれます。
