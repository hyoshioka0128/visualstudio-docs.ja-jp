---
title: 特殊化されたデプロイの処理 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- deploying applications [Visual Studio SDK]
- specialized deployment
ms.assetid: de068b6a-e806-45f0-9dec-2458fbb486f7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 972965c3565088af8205d6f7903d7098e568c057
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80708217"
---
# <a name="handle-specialized-deployment"></a>特化した展開を処理する
配置は、プロジェクトのオプションの操作です。 たとえば、Web プロジェクトでは、プロジェクトで Web サーバーを更新できる配置をサポートしています。 同様に、 **スマートデバイス** プロジェクトは、ビルドされたアプリケーションをターゲットデバイスにコピーするための配置をサポートしています。 プロジェクトのサブタイプは、インターフェイスを実装することによって、特殊な配置動作を提供でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> ます。 このインターフェイスは、デプロイ操作の完全なセットを定義します。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.AdviseDeployStatusCallback%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.Commit%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.QueryStartDeploy%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.QueryStatusDeploy%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.Rollback%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.StartDeploy%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.StopDeploy%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.UnadviseDeployStatusCallback%2A>

  実際の配置操作は、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ユーザーの操作に対する応答性をさらに高めるために、個別のスレッドで実行する必要があります。 によって提供されるメソッド <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> は、によって非同期的に呼び出され、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] バックグラウンドで動作します。これにより、環境はいつでもデプロイ操作の状態を照会したり、必要に応じて操作を停止したりできます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>インターフェイス配置操作は、ユーザーが配置コマンドを選択したときに環境によって呼び出されます。

  配置操作が開始または終了したことを環境に通知するには、プロジェクトのサブタイプがメソッドとメソッドを呼び出す必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployStatusCallback.OnStartDeploy%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployStatusCallback.OnEndDeploy%2A> ます。

## <a name="to-handle-a-specialized-deployment-by-a-subtype-project"></a>サブタイププロジェクトによって特殊な配置を処理するには

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.AdviseDeployStatusCallback%2A>デプロイステータスイベントの通知を受信するように環境を登録するには、メソッドを実装します。

    ```vb
    Private adviseSink As Microsoft.VisualStudio.Shell.EventSinkCollection = New Microsoft.VisualStudio.Shell.EventSinkCollection()
    Public Function AdviseDeployStatusCallback(ByVal pIVsDeployStatusCallback As IVsDeployStatusCallback, _
                                               ByRef pdwCookie As UInteger) As Integer

        If pIVsDeployStatusCallback Is Nothing Then
            Throw New ArgumentNullException("pIVsDeployStatusCallback")
        End If

        pdwCookie = adviseSink.Add(pIVsDeployStatusCallback)
        Return VSConstants.S_OK

    End Function
    ```

    ```csharp
    private Microsoft.VisualStudio.Shell.EventSinkCollection adviseSink = new Microsoft.VisualStudio.Shell.EventSinkCollection();
    public int AdviseDeployStatusCallback(IVsDeployStatusCallback pIVsDeployStatusCallback,
                                          out uint pdwCookie)
    {
        if (pIVsDeployStatusCallback == null)
            throw new ArgumentNullException("pIVsDeployStatusCallback");

        pdwCookie = adviseSink.Add(pIVsDeployStatusCallback);
        return VSConstants.S_OK;
    }

    ```

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.UnadviseDeployStatusCallback%2A>デプロイステータスイベントの通知を受信するために、環境の登録をキャンセルするメソッドを実装します。

    ```vb
    Public Function UnadviseDeployStatusCallback(ByVal dwCookie As UInteger) As Integer
        adviseSink.RemoveAt(dwCookie)
        Return VSConstants.S_OK
    End Function
    ```

    ```csharp
    public int UnadviseDeployStatusCallback(uint dwCookie)
    {
        adviseSink.RemoveAt(dwCookie);
        return VSConstants.S_OK;
    }

    ```

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.Commit%2A>アプリケーションに固有のコミット操作を実行するには、メソッドを実装します。  このメソッドは、主にデータベースの配置に使用されます。

    ```vb
    Public Function Commit(ByVal dwReserved As UInteger) As Integer
        'Implement commit operation here.
        Return VSConstants.S_OK
    End Function
    ```

    ```csharp
    public int Commit(uint dwReserved)
    {
         //Implement commit operation here.
         return VSConstants.S_OK;
    }

    ```

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.Rollback%2A>ロールバック操作を実行するには、メソッドを実装します。 このメソッドが呼び出されると、配置プロジェクトは、変更をロールバックし、プロジェクトの状態を復元するために適切な処理を行う必要があります。 このメソッドは、主にデータベースの配置に使用されます。

    ```vb
    Public Function Commit(ByVal dwReserved As UInteger) As Integer
        'Implement commit operation here.
        Return VSConstants.S_OK
    End Function
    ```

    ```csharp
    public int Rollback(uint dwReserved)
    {
        //Implement Rollback operation here.
        return VSConstants.S_OK;
    }

    ```

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.QueryStartDeploy%2A>プロジェクトが配置操作を開始できるかどうかを判断するために、メソッドを実装します。

    ```vb
    Public Function QueryStartDeploy(ByVal dwOptions As UInteger, ByVal pfSupported As Integer(), ByVal pfReady As Integer()) As Integer
        If Not pfSupported Is Nothing AndAlso pfSupported.Length > 0 Then
            pfSupported(0) = 1
        End If
        If Not pfReady Is Nothing AndAlso pfReady.Length > 0 Then
            pfReady(0) = 0
            If Not deploymentThread Is Nothing AndAlso (Not deploymentThread.IsAlive) Then
                pfReady(0) = 1
            End If
        End If
        Return VSConstants.S_OK
    End Function
    ```

    ```csharp
    public int QueryStartDeploy(uint dwOptions, int[] pfSupported, int[] pfReady)
    {
        if (pfSupported != null && pfSupported.Length >0)
            pfSupported[0] = 1;
        if (pfReady != null && pfReady.Length >0)
        {
            pfReady[0] = 0;
            if (deploymentThread != null && !deploymentThread.IsAlive)
                pfReady[0] = 1;
        }
        return VSConstants.S_OK;
    }

    ```

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.QueryStatusDeploy%2A>配置操作が正常に完了したかどうかを確認するには、メソッドを実装します。

    ```vb
    Public Function QueryStatusDeploy(ByRef pfDeployDone As Integer) As Integer
        pfDeployDone = 1
        If Not deploymentThread Is Nothing AndAlso deploymentThread.IsAlive Then
            pfDeployDone = 0
        End If
        Return VSConstants.S_OK
    End Function
    ```

    ```csharp
    public int QueryStatusDeploy(out int pfDeployDone)
    {
        pfDeployDone = 1;
        if (deploymentThread != null && deploymentThread.IsAlive)
            pfDeployDone = 0;
        return VSConstants.S_OK;
    }

    ```

- メソッドを実装して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.StartDeploy%2A> 別のスレッドで配置操作を開始します。 アプリケーションの配置に固有のコードをメソッド内に配置し `Deploy` ます。

    ```vb
    Public Function StartDeploy(ByVal pIVsOutputWindowPane As IVsOutputWindowPane, ByVal dwOptions As UInteger) As Integer
        If pIVsOutputWindowPane Is Nothing Then
            Throw New ArgumentNullException("pIVsOutputWindowPane")
        End If

        If Not deploymentThread Is Nothing AndAlso deploymentThread.IsAlive Then
            Throw New NotSupportedException("Cannot start deployment operation when it is already started; Call QueryStartDeploy first")
        End If

        outputWindow = pIVsOutputWindowPane

        ' Notify that deployment is about to begin and see if any user wants to cancel.
        If (Not NotifyStart()) Then
            Return VSConstants.E_ABORT
        End If

        operationCanceled = False

        ' Create and start our thread
        deploymentThread = New Thread(AddressOf Me.Deploy)
        deploymentThread.Name = "Deployment Thread"
        deploymentThread.Start()

        Return VSConstants.S_OK
    End Function
    ```

    ```csharp
    public int StartDeploy(IVsOutputWindowPane pIVsOutputWindowPane, uint dwOptions)
    {
        if (pIVsOutputWindowPane == null)
            throw new ArgumentNullException("pIVsOutputWindowPane");

        if (deploymentThread != null && deploymentThread.IsAlive)
            throw new NotSupportedException("Cannot start deployment operation when it is already started; Call QueryStartDeploy first");

        outputWindow = pIVsOutputWindowPane;

        // Notify that deployment is about to begin and see if any user wants to cancel.
        if (!NotifyStart())
            return VSConstants.E_ABORT;

        operationCanceled = false;

        // Create and start our thread
        deploymentThread = new Thread(new ThreadStart(this.Deploy));
        deploymentThread.Name = "Deployment Thread";
        deploymentThread.Start();

        return VSConstants.S_OK;
    }

    ```

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg.StopDeploy%2A>配置操作を停止するには、メソッドを実装します。 このメソッドは、展開プロセス中にユーザーが **[キャンセル** ] ボタンをクリックしたときに呼び出されます。

    ```vb
    Public Function StopDeploy(ByVal fSync As Integer) As Integer
        If Not deploymentThread Is Nothing AndAlso deploymentThread.IsAlive Then
            Return VSConstants.S_OK
        End If

        outputWindow.OutputStringThreadSafe("Canceling deployment")
        operationCanceled = True
        If fSync <> 0 Then
            ' Synchronous request, wait for the thread to terminate.
            If (Not deploymentThread.Join(10000)) Then
                Debug.Fail("Deployment thread did not terminate before the timeout, Aborting thread")
                deploymentThread.Abort()
            End If
        End If

        Return VSConstants.S_OK
    End Function
    ```

    ```csharp
    public int StopDeploy(int fSync)
    {
        if (deploymentThread != null && deploymentThread.IsAlive)
            return VSConstants.S_OK;

        outputWindow.OutputStringThreadSafe("Canceling deployment");
        operationCanceled = true;
        if (fSync != 0)
        {
            // Synchronous request, wait for the thread to terminate.
            if (!deploymentThread.Join(10000))
            {
                Debug.Fail("Deployment thread did not terminate before the timeout, Aborting thread");
                deploymentThread.Abort();
            }
        }

        return VSConstants.S_OK;
    }

    ```

> [!NOTE]
> このトピックで説明するすべてのコード例は、 [Vssdk サンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)の大きな例の一部です。

## <a name="see-also"></a>関連項目
- [プロジェクトのサブタイプ](../../extensibility/internals/project-subtypes.md)
