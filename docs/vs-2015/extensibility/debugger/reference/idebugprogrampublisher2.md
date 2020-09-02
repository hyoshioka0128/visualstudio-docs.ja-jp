---
title: IDebugProgramPublisher2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2
helpviewer_keywords:
- IDebugProgramPublisher2 interface
ms.assetid: b1d17f63-7146-4076-a588-034cfc6858b9
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d49173a4c1f10be1544cf07b0b01640321d6d181
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697296"
---
# <a name="idebugprogrampublisher2"></a>IDebugProgramPublisher2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスにより、デバッグエンジン (DE) またはカスタムポート供給者は、デバッグ用のプログラムを登録できます。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugProgramPublisher2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 Visual Studio では、デバッグ中のプログラムを複数のプロセスにわたって表示できるようにするために、このインターフェイスを実装しています。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 `CoCreateInstance`このインターフェイスを取得するには、を使用して COM の関数を呼び出し `CLSID_ProgramPublisher` ます (例を参照)。 DE またはカスタムポート供給業者は、このインターフェイスを使用して、デバッグ対象のプログラムを表すプログラムノードを登録します。  
  
## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド  
 このインターフェイスは、次のメソッドを実装します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[PublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)|プログラムノードを DEs およびセッションデバッグマネージャー (SDM) で使用できるようにします。|  
|[UnpublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogramnode.md)|プログラムノードが使用できなくなるように削除します。|  
|[PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)|プログラムを DEs および SDM で使用できるようにします。|  
|[UnpublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogram.md)|使用できなくなったプログラムを削除します。|  
|[SetDebuggerPresent](../../../extensibility/debugger/reference/idebugprogrampublisher2-setdebuggerpresent.md)|デバッガーが存在することを示すフラグを設定します。|  
  
## <a name="remarks"></a>注釈  
 このインターフェイスにより、プログラムとプログラムノードが使用できるようになります (つまり "発行")。 DEs およびセッションデバッグマネージャー (SDM) によって使用されます。 公開されているプログラムとプログラムノードにアクセスするには、 [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md) インターフェイスを使用します。 これは、プログラムがデバッグ中であることを Visual Studio が認識する唯一の方法です。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="example"></a>例  
 この例では、プログラムの発行元をインスタンス化し、プログラムノードを登録する方法を示します。 これは、「 [プログラムノードを公開](https://msdn.microsoft.com/d0100e02-4e2b-4e72-9e90-f7bc11777bae)する」のチュートリアルから引用しています。  
  
```cpp#  
// This is how m_srpProgramPublisher is defined in the class definition:  
// CComPtr<IDebugProgramPublisher2> m_srpProgramPublisher.  
  
void CProgram::Start(IDebugEngine2 * pEngine)  
{  
    m_spEngine = pEngine;  
  
    HRESULT hr = m_srpProgramPublisher.CoCreateInstance(CLSID_ProgramPublisher);  
    if ( FAILED(hr) )  
    {  
        ATLTRACE("Failed to create the program publisher: 0x%x.", hr);  
        return;  
    }  
  
    // Register ourselves with the program publisher. Note that  
    // CProgram implements the IDebgProgramNode2 interface, hence  
    // the static cast on "this".  
    hr = m_srpProgramPublisher->PublishProgramNode(  
        static_cast<IDebugProgramNode2*>(this));  
    if ( FAILED(hr) )  
    {  
        ATLTRACE("Failed to publish the program node: 0x%x.", hr);  
        m_srpProgramPublisher.Release();  
        return;  
    }  
  
    ATLTRACE("Added program node.\n");  
}  
```  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
