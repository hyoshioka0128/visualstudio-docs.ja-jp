---
title: プログラム | を登録していますMicrosoft Docs
description: デバッグエンジンがポートを取得した後に、デバッグ対象のプログラムをポートに登録する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, registration
- debugging [Debugging SDK], program registration
ms.assetid: d726a161-7db3-4ef4-b258-9f6a5be68418
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8326bb2c3938ce76d777c73d0d0f24da145d8ef5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99961067"
---
# <a name="register-the-program"></a>プログラムを登録する
デバッグエンジンが [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md) インターフェイスによって表されるポートを取得した後、デバッグ対象のプログラムを有効にするための次の手順として、そのポートをポートに登録します。 登録されると、プログラムは次のいずれかの方法でデバッグできるようになります。

- をアタッチするプロセス。これにより、デバッガーは実行中のアプリケーションの完全なデバッグ制御を取得できます。

- Just-in-time (JIT) デバッグ。これにより、デバッガーとは別に実行されるプログラムの、後でのデバッグが可能になります。 ランタイムアーキテクチャでエラーがキャッチされると、オペレーティングシステムまたはランタイム環境でエラーが発生したプログラムのメモリとリソースが解放される前に、デバッガーに通知されます。

## <a name="registering-procedure"></a>登録 (プロシージャを)

### <a name="to-register-your-program"></a>プログラムを登録するには

1. ポートによって実装されている [Addprogramnode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md) メソッドを呼び出します。

     `IDebugPortNotify2::AddProgramNode`[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)インターフェイスへのポインターが必要です。

     通常、オペレーティングシステムまたはランタイム環境でプログラムが読み込まれると、プログラムノードが作成されます。 デバッグエンジン (DE) からプログラムの読み込みが求められた場合、DE はプログラムノードを作成し、登録します。

     次の例は、デバッグエンジンがプログラムを起動し、ポートに登録する方法を示しています。

    > [!NOTE]
    > このコードサンプルは、プロセスを起動して再開する唯一の方法ではありません。このコードは、主に、プログラムをポートに登録する例です。

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
- [ポートを取得する](../../extensibility/debugger/getting-a-port.md)
- [プログラムのデバッグを有効にする](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
