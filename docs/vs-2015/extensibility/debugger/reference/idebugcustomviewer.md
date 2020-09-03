---
title: IDebugCustomViewer |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCustomViewer
helpviewer_keywords:
- IDebugCustomViewer interface
ms.assetid: 7aca27d3-c7b8-470f-b42c-d1e9d9115edd
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5f94fe0301777a615fa6dc567311c493ff55a90a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196295"
---
# <a name="idebugcustomviewer"></a>IDebugCustomViewer
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスにより、式エバリュエーター (EE) は、必要な形式でプロパティの値を表示できます。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugCustomViewer : IUknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 EE は、このインターフェイスを実装して、プロパティの値をカスタム書式で表示します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 COM の関数を呼び出すと、 `CoCreateInstance` このインターフェイスがインスタンス化されます。 に渡されたは、 `CLSID` `CoCreateInstance` レジストリから取得されます。 [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)を呼び出すと、レジストリ内の場所が取得されます。 詳細と例については、「解説」を参照してください。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 このインターフェイスは、次のメソッドを実装します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[DisplayValue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)|指定された値を表示するために必要なすべてのことを行います。|  
  
## <a name="remarks"></a>注釈  
 このインターフェイスは、通常の方法でプロパティの値を表示できない場合に使用されます。たとえば、データテーブルやその他の複合プロパティ型を使用します。 インターフェイスによって表されるカスタムビューアー `IDebugCustomViewer` は、型ビジュアライザーとは異なります。これは、EE に関係なく特定の型のデータを表示するための外部プログラムです。 EE には、その EE に固有のカスタムビューアーが実装されています。 ユーザーは、使用するビジュアライザーの種類として、型ビジュアライザーまたはカスタムビューアーを選択します。 このプロセスの詳細については [、「データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md) 」を参照してください。  
  
 カスタムビューアーは、EE と同じ方法で登録されるため、言語 GUID とベンダー GUID が必要です。 正確なメトリック (またはレジストリエントリ名) は、EE にのみ認識されます。 このメトリックは [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md) 構造で返され、 [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)の呼び出しによって返されます。 メトリックに格納される値は、 `CLSID` COM の関数に渡されるです `CoCreateInstance` (例を参照)。  
  
 [デバッグ機能の SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) () を使用して、 `SetEEMetric` カスタムビューアーを登録できます。 `Debugging SDK Helpers`カスタムビューアーで必要な特定のレジストリキーについては、「」の「式エバリュエーター」レジストリセクションを参照してください。 カスタムビューアーに必要なメトリックは1つだけで、式エバリュエーターにはいくつかの定義済みのメトリックが必要です。  
  
 通常、カスタムビューアーには、データの読み取り専用ビューが用意されています。 [Displayvalue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)に渡される[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)インターフェイスには、文字列以外のプロパティ値を変更するためのメソッドがないためです。 データの任意のブロックの変更をサポートするために、EE は、インターフェイスを実装するのと同じオブジェクトにカスタムインターフェイスを実装し `IDebugProperty3` ます。 このカスタムインターフェイスは、任意のデータブロックを変更するために必要なメソッドを提供します。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="example"></a>例  
 この例では、プロパティにカスタムビューアーが含まれている場合に、プロパティから最初のカスタムビューアーを取得する方法を示します。  
  
```cpp#  
IDebugCustomViewer *GetFirstCustomViewer(IDebugProperty2 *pProperty)  
{  
    // This string is typically defined globally.  For this example, it  
    // is defined here.  
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";  
    IDebugCustomViewer *pViewer = NULL;  
    if (pProperty != NULL) {  
        CComQIPtr<IDebugProperty3> pProperty3(pProperty);  
        if (pProperty3 != NULL) {  
            HRESULT hr;  
            ULONG viewerCount = 0;  
            hr = pProperty3->GetCustomViewerCount(&viewerCount);  
            if (viewerCount > 0) {  
                ULONG viewersFetched = 0;  
                DEBUG_CUSTOM_VIEWER viewerInfo = { 0 };  
                hr = pProperty3->GetCustomViewerList(0,  
                                                     1,  
                                                     &viewerInfo,  
                                                     &viewersFetched);  
                if (viewersFetched == 1) {  
                    CLSID clsidViewer = { 0 };  
                    CComPtr<IDebugCustomViewer> spCustomViewer;  
                    // Get the viewer's CLSID from the registry.  
                    ::GetEEMetric(viewerInfo.guidLang,  
                                  viewerInfo.guidVendor,  
                                  viewerInfo.bstrMetric,  
                                  &clsidViewer,  
                                  strRegistrationRoot);  
                    if (!IsEqualGUID(clsidViewer,GUID_NULL)) {  
                        // Instantiate the custom viewer.  
                        spCustomViewer.CoCreateInstance(clsidViewer);  
                        if (spCustomViewer != NULL) {  
                            pViewer = spCustomViewer.Detach();  
                        }  
                    }  
                }  
            }  
        }  
    }  
    return(pViewer);  
}  
```  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)   
 [デバッグ用の SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)   
 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
