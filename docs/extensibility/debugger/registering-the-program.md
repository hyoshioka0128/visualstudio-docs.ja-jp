---
title: プログラムの登録 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, registration
- debugging [Debugging SDK], program registration
ms.assetid: d726a161-7db3-4ef4-b258-9f6a5be68418
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b68fa67f784d155288482ad724b632ed5ba5fa41
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713172"
---
# <a name="register-the-program"></a>プログラムの登録
デバッグ エンジンが[IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)インターフェイスで表されるポートを取得した後、デバッグするプログラムを有効にする次の手順は、ポートに登録します。 登録すると、プログラムは次のいずれかの方法でデバッグできるようになります。

- デバッガが実行中のアプリケーションの完全なデバッグ制御を取得できるようにするアタッチプロセス。

- ジャスト イン タイム (JIT) デバッグを使用すると、デバッガーとは独立して実行されるプログラムの事後デバッグが可能になります。 ランタイム アーキテクチャが障害をキャッチすると、オペレーティング システムまたはランタイム環境が障害を起しているプログラムのメモリとリソースを解放する前に、デバッガに通知されます。

## <a name="registering-procedure"></a>登録手続き

### <a name="to-register-your-program"></a>プログラムを登録するには

1. ポートによって実装[されるメソッドを](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)呼び出します。

     `IDebugPortNotify2::AddProgramNode`インターフェイスへの[ポインターが必要](../../extensibility/debugger/reference/idebugprogramnode2.md)です。

     通常、オペレーティング システムまたはランタイム環境がプログラムを読み込むときに、プログラム ノードが作成されます。 デバッグ エンジン (DE) は、プログラムの読み込みを求められた場合、DE は作成し、プログラム ノードを登録します。

     次の例は、プログラムを起動し、ポートに登録するデバッグ エンジンを示しています。

    > [!NOTE]
    > このコード サンプルは、プロセスを起動して再開する唯一の方法ではありません。このコードは、主にポートを使用してプログラムを登録する例です。

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
                    hr  = spPortEx->ResumeProcess(pDebugProcess);
                }
            }
        }
        return(hr);
    }

    ```

## <a name="see-also"></a>関連項目
- [ポートの取得](../../extensibility/debugger/getting-a-port.md)
- [プログラムのデバッグの有効化](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
