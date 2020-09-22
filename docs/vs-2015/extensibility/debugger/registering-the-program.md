---
title: プログラム | を登録していますMicrosoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- programs, registration
- debugging [Debugging SDK], program registration
ms.assetid: d726a161-7db3-4ef4-b258-9f6a5be68418
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 31d03f12a31953cbc0e20d06820dd49b5f9827e6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842101"
---
# <a name="registering-the-program"></a>プログラムの登録
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッグエンジンが [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md) インターフェイスによって表されるポートを取得した後、デバッグ対象のプログラムを有効にするための次の手順として、そのポートをポートに登録します。 登録されると、プログラムは次のいずれかの方法でデバッグできるようになります。  
  
- をアタッチするプロセス。これにより、デバッガーは実行中のアプリケーションの完全なデバッグ制御を取得できます。  
  
- Just-in-time (JIT) デバッグ。これにより、デバッガーとは別に実行されるプログラムの、後でのデバッグが可能になります。 ランタイムアーキテクチャでエラーがキャッチされると、オペレーティングシステムまたはランタイム環境でエラーが発生したプログラムのメモリとリソースが解放される前に、デバッガーに通知されます。  
  
## <a name="registering-procedure"></a>登録 (プロシージャを)  
  
#### <a name="to-register-your-program"></a>プログラムを登録するには  
  
1. ポートによって実装されている [Addprogramnode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md) メソッドを呼び出します。  
  
     `IDebugPortNotify2::AddProgramNode`[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)インターフェイスへのポインターが必要です。  
  
     通常、オペレーティングシステムまたはランタイム環境でプログラムが読み込まれると、プログラムノードが作成されます。 デバッグエンジン (DE) からプログラムの読み込みが求められた場合は、DE によってプログラムノードが作成され、登録されます。  
  
     次の例は、デバッグエンジンがプログラムを起動し、ポートに登録する方法を示しています。  
  
    > [!NOTE]
    > これは、プロセスを起動して再開する唯一の方法ではありません。これは、主に、プログラムをポートに登録する例です。  
  
    ```cpp#  
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
  
## <a name="see-also"></a>参照  
 [ポートを取得する](../../extensibility/debugger/getting-a-port.md)   
 [デバッグするプログラムの有効化](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
