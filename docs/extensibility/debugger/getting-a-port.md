---
title: ポートを取得する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ports, getting
- debugging [Debugging SDK], ports
ms.assetid: 745c2337-cfff-4d02-b49c-3ca7c4945c5e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7bf4948e7cb2590136774eab76fbafec91dbfa40
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738638"
---
# <a name="get-a-port"></a>ポートを取得する
ポートは、プロセスが実行されているマシンへの接続を表します。 そのマシンは、ローカル マシンまたはリモート マシンである可能性があります (Windows ベース以外のオペレーティング システムを実行している[Ports](../../extensibility/debugger/ports.md)可能性があります。

ポートは[、IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)インターフェイスによって表されます。 ポートが接続されているマシンで実行されているプロセスに関する情報を取得するために使用されます。

デバッグ エンジンは、プログラム ノードをポートに登録し、プロセス情報の要求を満たすために、ポートにアクセスする必要があります。 たとえば、デバッグ エンジンが[IDebugProgramProvider2](../../extensibility/debugger/reference/idebugprogramprovider2.md)インターフェイスを実装している場合[、GetProviderProcessData](../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)メソッドの実装は、必要なプロセス情報を返す必要があるかどうかをポートに要求できます。

Visual Studio は、デバッグ エンジンに必要なポートを提供し、ポートサプライヤーからこのポートを取得します。 プログラムがアタッチされている場合 (デバッガー内から、または例外がスローされたために Just-In-Time [JIT] ダイアログ ボックスがトリガーされた)、ユーザーは使用するトランスポート (ポート サプライヤーの別の名前) の選択を与えられます。 それ以外の場合、ユーザーがデバッガー内からプログラムを起動すると、プロジェクト システムは使用するポートサプライヤーを指定します。 どちらの場合も、Visual Studio は[、IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)インターフェイスで表されるポート サプライヤーをインスタンス化し[、IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)インターフェイスを使用して[AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)を呼び出すことによって新しいポートを要求します。 このポートは、その後、何かの形式でデバッグ エンジンに渡されます。

## <a name="example"></a>例
このコードは[、LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)に提供されたポートを使用して[ResumeProcess](../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)にプログラム ノードを登録する方法を示しています。 この概念に直接関連しないパラメータは、わかりやすくするために省略されています。

> [!NOTE]
> この例では、ポートを使用してプロセスを起動および再開し[、IDebugPortEx2](../../extensibility/debugger/reference/idebugportex2.md)インターフェイスがポートに実装されていることを前提としています。 これは決してこれらのタスクを実行する唯一の方法ではなく、プログラムの[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)を与える以外にポートが関与していない可能性があります。

```cpp
// This is an IDebugEngineLaunch2 method.
HRESULT CDebugEngine::LaunchSuspended(/* omitted parameters */,
                                      IDebugPort2 *pPort,
                                      /* omitted parameters */,
                                      IDebugProcess2**ppDebugProcess)
{
    // do stuff here to set up for a launch (such as handling the other parameters)
    ...

    // Now get the IPortNotify2 interface so we can register a program node
    // in CDebugEngine::ResumeProcess.
    CComPtr<IDebugDefaultPort2> spDefaultPort;
    HRESULT hr = pPort->QueryInterface(&spDefaultPort);
    if (SUCCEEDED(hr))
    {
        CComPtr<IDebugPortNotify2> spPortNotify;
        hr = spDefaultPort->GetPortNotify(&spPortNotify);
        if (SUCCEEDED(hr))
        {
            // Remember the port notify so we can use it in ResumeProcess.
            m_spPortNotify = spPortNotify;

            // Now launch the process in a suspended state and return the
            // IDebugProcess2 interface
            CComPtr<IDebugPortEx2> spPortEx;
            hr = pPort->QueryInterface(&spPortEx);
            if (SUCCEEDED(hr))
            {
                // pass on the parameters we were given (omitted here)
                hr = spPortEx->LaunchSuspended(/* omitted parameters */,ppDebugProcess)
            }
        }
    }
    return(hr);
}

HRESULT CDebugEngine::ResumeProcess(IDebugProcess2 *pDebugProcess)
{
    // Make a program node for this process
    HRESULT hr;
    CComPtr<IDebugProgramNode2> spProgramNode;
    hr = this->GetProgramNodeForProcess(pProcess, &spProgramNode);
    if (SUCCEEDED(hr))
    {
        hr = m_spPortNotify->AddProgramNode(spProgramNode);
        if (SUCCEEDED(hr))
        {
            // resume execution of the process using the port given to us earlier.
            // (Querying for the IDebugPortEx2 interface is valid here since
            // that's how we got the IDebugPortNotify2 interface in the first place.)
            CComPtr<IDebugPortEx2> spPortEx;
            hr = m_spPortNotify->QueryInterface(&spPortEx);
            if (SUCCEEDED(hr))
            {
                hr = spPortEx->ResumeProcess(pDebugProcess);
            }
        }
    }
    return(hr);
}
```

## <a name="see-also"></a>関連項目
- [プログラムの登録](../../extensibility/debugger/registering-the-program.md)
- [プログラムのデバッグの有効化](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
- [港湾サプライヤー](../../extensibility/debugger/port-suppliers.md)
- [ポート](../../extensibility/debugger/ports.md)
