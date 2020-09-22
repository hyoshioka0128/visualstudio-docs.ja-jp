---
title: ポートを取得する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- ports, getting
- debugging [Debugging SDK], ports
ms.assetid: 745c2337-cfff-4d02-b49c-3ca7c4945c5e
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f980c9d14bc2d0c9728f87374828cf690737429c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842108"
---
# <a name="getting-a-port"></a>ポートの取得
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ポートは、プロセスが実行されているコンピューターへの接続を表します。 このコンピューターは、ローカルコンピューターまたはリモートコンピューターである可能性があります (Windows ベース以外のオペレーティングシステムを実行している可能性があります。詳細については、「 [ポート](../../extensibility/debugger/ports.md) 」を参照してください)。  
  
 ポートは、 [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md) インターフェイスによって表されます。 これは、ポートが接続されているコンピューターで実行中のプロセスに関する情報を取得するために使用されます。  
  
 デバッグエンジンは、プログラムノードをポートに登録し、プロセス情報の要求を満たすために、ポートへのアクセスを必要とします。 たとえば、デバッグエンジンが [IDebugProgramProvider2](../../extensibility/debugger/reference/idebugprogramprovider2.md) インターフェイスを実装している場合、 [Getproviderprocessdata](../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md) メソッドの実装では、必要なプロセス情報を返すようにポートに要求できます。  
  
 Visual Studio では、必要なポートがデバッグエンジンに提供され、ポート供給元からこのポートが取得されます。 プログラムがにアタッチされている場合 (デバッガー内から、または例外がスローされ、Just-in-time [JIT] ダイアログボックスがトリガーされる)、ユーザーには、使用するトランスポート (別の名前) が与えられます。 そうしないと、ユーザーがデバッガー内からプログラムを起動した場合、使用するポート供給業者がプロジェクトシステムによって指定されます。 どちらのイベントでも、Visual Studio は[IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)インターフェイスによって表されるポート供給元をインスタンス化し、 [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)インターフェイスを使用して[addport](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)を呼び出すことによって新しいポートを要求します。 このポートは、1つまたは別の形式でデバッグエンジンに渡されます。  
  
## <a name="example"></a>例  
 このコード片では、 [Launchsuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) に指定されたポートを使用して、 [ResumeProcess](../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)でプログラムノードを登録する方法を示します。 この概念に直接関係のないパラメーターは、わかりやすくするために省略されています。  
  
> [!NOTE]
> この例では、ポートを使用してプロセスを起動および再開し、 [IDebugPortEx2](../../extensibility/debugger/reference/idebugportex2.md) インターフェイスがポートに実装されていることを前提としています。 これは、これらのタスクを実行する唯一の方法ではなく、プログラムの [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) が与えられていなくても、そのポートが関係していない可能性があります。  
  
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
 [プログラムを登録しています](../../extensibility/debugger/registering-the-program.md)   
 [プログラムのデバッグを有効にする](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)   
 [ポートサプライヤー](../../extensibility/debugger/port-suppliers.md)   
 [ポート](../../extensibility/debugger/ports.md)
