---
title: ソリューションでのプロジェクトの読み込みの管理 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- solutions, managing project loading
ms.assetid: 097c89d0-f76a-4aaf-ada9-9a778bd179a0
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a6598e2f1a178845b3ad2017716576439185379e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841449"
---
# <a name="managing-project-loading-in-a-solution"></a>ソリューションでのプロジェクトの読み込みの管理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio ソリューションには、多数のプロジェクトを含めることができます。 Visual Studio の既定の動作では、ソリューションを開いたときにソリューション内のすべてのプロジェクトが読み込まれます。また、すべてのプロジェクトの読み込みが完了するまで、ユーザーはどのプロジェクトにもアクセスできません。 プロジェクトの読み込みプロセスが2分以上経過すると、読み込まれたプロジェクトの数とプロジェクトの合計数を示す進行状況バーが表示されます。 ユーザーは、複数のプロジェクトを含むソリューションで作業しているときにプロジェクトをアンロードできますが、この手順にはいくつかの欠点があります。アンロードされたプロジェクトは、リビルドソリューションコマンドの一部としてビルドされず、閉じられたプロジェクトの型とメンバーの IntelliSense 記述は表示されません。  
  
 ソリューションロードマネージャーを作成することで、開発者はソリューションの読み込み時間を短縮し、プロジェクトの読み込み動作を管理できます。 ソリューションロードマネージャーでは、特定のプロジェクトまたはプロジェクトの種類に対してさまざまなプロジェクト読み込みの優先順位を設定したり、バックグラウンドビルドを開始する前にプロジェクトが読み込まれるようにしたり、他のバックグラウンドタスクが完了するまでバックグラウンド読み込みを遅らせたり、その他のプロジェクト読み込み管理タスクを実行したりすることができます。  
  
## <a name="project-loading-priorities"></a>プロジェクト読み込みの優先順位  
 Visual Studio では、次の4つの異なるプロジェクト読み込みの優先順位を定義します。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop._VSProjectLoadPriority> (既定値): ソリューションが開かれると、プロジェクトは非同期に読み込まれます。 ソリューションが既に開いている状態でアンロードされたプロジェクトにこの優先順位が設定されている場合、プロジェクトは次のアイドルポイントで読み込まれます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop._VSProjectLoadPriority>: ソリューションを開くと、プロジェクトがバックグラウンドで読み込まれます。これにより、ユーザーは、プロジェクトが読み込まれるまで待機することなく、プロジェクトにアクセスできるようになります。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop._VSProjectLoadPriority>: プロジェクトは、アクセスされると読み込まれます。 プロジェクトにアクセスするには、ユーザーがソリューションエクスプローラー内のプロジェクトノードを展開するときに、プロジェクトに属するファイルが開いているドキュメントの一覧 (ソリューションのユーザーオプションファイルに保存されます) にあるか、または読み込まれている別のプロジェクトがプロジェクトに依存しているときに、そのプロジェクトに属するファイルが開かれます。 この種類のプロジェクトは、ビルドプロセスを開始する前に自動的に読み込まれません。ソリューションロードマネージャーは、すべての必要なプロジェクトが読み込まれるようにする役割を担います。 また、ソリューション全体でファイル内の検索/置換を開始する前に、これらのプロジェクトも読み込まれる必要があります。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop._VSProjectLoadPriority>: ユーザーが明示的に要求しない限り、プロジェクトは読み込まれません。 プロジェクトが明示的にアンロードされた場合は、次のようになります。  
  
## <a name="creating-a-solution-load-manager"></a>ソリューションロードマネージャーの作成  
 開発者は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager> ソリューションロードマネージャーがアクティブであることを Visual Studio に実装して通知することで、ソリューションロードマネージャーを作成できます。  
  
#### <a name="activating-a-solution-load-manager"></a>ソリューションロードマネージャーのアクティブ化  
 Visual Studio では、一度に1つのソリューションロードマネージャーのみが許可されます。そのため、ソリューションロードマネージャーをアクティブ化する場合は、Visual Studio にアドバイスする必要があります。 2つ目のソリューションロードマネージャーを後でアクティブにすると、ソリューションロードマネージャーが切断されます。  
  
 サービスを取得し、プロパティを設定する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution> <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4> ます。  
  
```csharp  
IVsSolution pSolution = GetService(typeof(SVsSolution)) as IVsSolution;  
object objLoadMgr = this;   //the class that implements IVsSolutionManager  
pSolution.SetProperty((int)__VSPROPID4.VSPROPID_ActiveSolutionLoadManager, objLoadMgr);  
```  
  
#### <a name="implementing-ivssolutionloadmanager"></a>IVsSolutionLoadManager の実装  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager.OnBeforeOpenProject%2A>メソッドは、ソリューションを開く処理中に呼び出されます。 このメソッドを実装するには、サービスを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManagerSupport> 管理するプロジェクトの種類の読み込み優先順位を設定します。 たとえば、次のコードでは、C# プロジェクトの種類をバックグラウンドで読み込むように設定しています。  
  
```csharp  
Guid guidCSProjectType = new Guid("{FAE04EC0-301F-11d3-BF4B-00C04F79EFBC}");  
pSLMgrSupport.SetProjectLoadPriority(guidProjectID, (uint)_VSProjectLoadPriority.PLP_BackgroundLoad);  
```  
  
 メソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager.OnDisconnect%2A> Visual Studio がシャットダウンされるとき、またはプロパティを使用してを呼び出すことによって別のパッケージがアクティブソリューションロードマネージャーとして引き継がれるときに呼び出され <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.SetProperty%2A> <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4> ます。  
  
#### <a name="strategies-for-different-kinds-of-solution-load-manager"></a>さまざまな種類のソリューションロードマネージャーの戦略  
 ソリューションロードマネージャーは、管理対象のソリューションの種類に応じて、さまざまな方法で実装できます。  
  
 ソリューションロードマネージャーが一般にソリューションの読み込みを管理する場合は、VSPackage の一部として実装できます。 パッケージは、値がである VSPackage にを追加することによって、自動読み込みに設定する必要があり <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionOpening_guid> ます。 その後、ソリューションロードマネージャーをメソッドでアクティブ化でき <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> ます。  
  
> [!NOTE]
> 自動読み込みパッケージの詳細については、「 [vspackage の読み込み](../extensibility/loading-vspackages.md)」を参照してください。  
  
 Visual Studio では、最後にアクティブ化されるソリューションロードマネージャーのみが認識されるため、一般的なソリューションロードマネージャーでは、自身をアクティブ化する前に、既存のロードマネージャーがあるかどうかを常に検出する必要があります。 ソリューションサービスで GetProperty () を呼び出して <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4> が返さ `null` れた場合、アクティブなソリューションロードマネージャーは存在しません。 Null が返されない場合は、オブジェクトがソリューションロードマネージャーと同じであるかどうかを確認します。  
  
 ソリューションロードマネージャーが、いくつかの種類のソリューションのみを管理するように設計されている場合、VSPackage はを呼び出すことによってソリューション読み込みイベントをサブスクライブ <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A> し、のイベントハンドラーを使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A> ソリューションロードマネージャーをアクティブ化できます。  
  
 ソリューションロードマネージャーが特定のソリューションのみを管理するように指定されている場合は、ソリューションファイルの一部としてアクティベーション情報を永続化できます。 これを行うには、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A> ソリューション前のセクションに対してを呼び出します。  
  
 特定のソリューションロードマネージャーは <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents.OnAfterCloseSolution%2A> 、他のソリューションロードマネージャーと競合しないように、イベントハンドラーで自身を非アクティブ化する必要があります。  
  
 グローバルプロジェクトの負荷の優先順位 (たとえば [オプション] ページで設定されたプロパティ) を永続化するためだけにソリューションロードマネージャーを使用する必要がある場合は、イベントハンドラーでソリューションロードマネージャーをアクティブにし <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents2.OnAfterOpenProject%2A> 、ソリューションのプロパティで設定を永続化してから、ソリューションロードマネージャーを非アクティブ化します。  
  
## <a name="handling-solution-load-events"></a>ソリューションの読み込みイベントの処理  
 ソリューション読み込みイベントをサブスクライブするには、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A> ソリューションロードマネージャーをアクティブ化するときにを呼び出します。 を実装すると <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents> 、異なるプロジェクトの読み込み優先順位に関連するイベントに応答できます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A>: これは、ソリューションが開かれる前に発生します。 これを使用すると、ソリューション内のプロジェクトのプロジェクトの読み込み優先度を変更できます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeBackgroundSolutionLoadBegins%2A>: ソリューションが完全に読み込まれた後、バックグラウンドプロジェクトの読み込みが再び開始される前に発生します。 たとえば、負荷の優先度が LoadIfNeeded に設定されているプロジェクトにユーザーがアクセスした場合、または solution load manager がプロジェクトの読み込みの優先順位を BackgroundLoad に変更した場合、そのプロジェクトのバックグラウンド読み込みが開始されます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterBackgroundSolutionLoadComplete%2A>: ソリューションロードマネージャーがあるかどうかにかかわらず、ソリューションが最初に完全に読み込まれた後に発生します。 また、ソリューションが完全に読み込まれたときに、バックグラウンド読み込みまたは要求読み込みの後にも発生します。 同時に、が再 <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExistsAndFullyLoaded_guid> アクティブ化されます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnQueryBackgroundLoadProjectBatch%2A>: これは、プロジェクト (またはプロジェクト) が読み込まれる前に発生します。 プロジェクトが読み込まれる前に他のバックグラウンドプロセスが完了するようにするには、を `pfShouldDelayLoadToNextIdle` **true**に設定します。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeLoadProjectBatch%2A>: プロジェクトのバッチが読み込まれるときに発生します。 `fIsBackgroundIdleBatch`が true の場合、プロジェクトはバックグラウンドで読み込まれます。が false の場合、ユーザーが `fIsBackgroundIdleBatch` ソリューションエクスプローラーで保留中のプロジェクトを展開するなど、ユーザー要求の結果としてプロジェクトが同期的に読み込まれます。 これを実装すると、で実行する必要がある高額な作業を行うことができ <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> ます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterLoadProjectBatch%2A>: プロジェクトのバッチが読み込まれた後に発生します。  
  
## <a name="detecting-and-managing-solution-and-project-loading"></a>ソリューションとプロジェクトの読み込みの検出と管理  
 プロジェクトとソリューションの読み込み状態を検出するには、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProperty%2A> 次の値を指定してを呼び出します。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4>: `var` `true` ソリューションとそのすべてのプロジェクトが読み込まれている場合はを返します。それ以外の場合はを返し `false` ます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4>: `var` `true` プロジェクトのバッチが現在バックグラウンドで読み込まれている場合はを返します。それ以外の場合はを返し `false` ます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4>: `var` `true` ユーザーコマンドまたはその他の明示的な読み込みの結果として、プロジェクトのバッチが現在同期的に読み込まれている場合はを返します。それ以外の場合はを返し `false` ます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2>: `var` `true` ソリューションが現在閉じられている場合はを返します。それ以外の場合はを返し `false` ます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID>: `var` `true` ソリューションが現在開かれている場合はを返します。それ以外の場合はを返し `false` ます。  
  
  次のいずれかの方法を呼び出すことによって、プロジェクトとソリューションが読み込まれていることを確認することもできます (プロジェクトの読み込みの優先度に関係なく)。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureSolutionIsLoaded%2A>: このメソッドを呼び出すと、メソッドが返される前に、ソリューション内のプロジェクトが強制的に読み込まれます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectIsLoaded%2A>: このメソッドを呼び出すと、メソッドが返される前に、にプロジェクトが強制的に `guidProject` 読み込まれます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectsAreLoaded%2A>: このメソッドを呼び出すと、メソッドが返される前に、にプロジェクトが強制的に `guidProjectID` 読み込まれます。  
  
> [!NOTE]
> . 既定では、要求読み込みとバックグラウンド読み込みの優先順位を持つプロジェクトのみが読み込まれますが、 <xref:Microsoft.VisualStudio.Shell.Interop.__VSBSLFLAGS> フラグがメソッドに渡されると、明示的に読み込まれるようにマークされているプロジェクトを除き、すべてのプロジェクトが読み込まれます。
