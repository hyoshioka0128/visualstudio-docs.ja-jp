---
title: 'IDebugBreakpointErrorEvent2:: GetErrorBreakpoint |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBreakpointErrorEvent2::GetErrorBreakpoint
helpviewer_keywords:
- IDebugBreakpointErrorEvent2::GetErrorBreakpoint
ms.assetid: e5acfd19-ac17-47f3-a31a-b2aa8baca36d
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0ddfe31af1287cd46683aa3a423bf0fd594915eb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68158822"
---
# <a name="idebugbreakpointerrorevent2geterrorbreakpoint"></a>IDebugBreakpointErrorEvent2::GetErrorBreakpoint
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ブレークポイントがバインドされなかった理由を説明する [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) オブジェクトを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetErrorBreakpoint(   
   IDebugErrorBreakpoint2** ppErrorBP  
);  
```  
  
```csharp  
int GetErrorBreakpoint(   
   out IDebugErrorBreakpoint2 ppErrorBP  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppErrorBP`  
 入出力警告またはエラーを説明する [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 インターフェイスを取得した後 `IDebugErrorBreakpoint2` 、 [Getbreakpointresolution](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md) メソッドを呼び出して、 [IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md) オブジェクトを取得します。 次に、 [Get解決情報](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md) メソッドを使用して、無効な場所、無効な式、または保留中のブレークポイントがバインドされていない理由 (まだ読み込まれていないコードなど) を判断できます。  
  
## <a name="example"></a>例  
 次の例は、 [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)インターフェイスを公開する**Cbreakpointsetdebugeventbase**オブジェクトに対してこのメソッドを実装する方法を示しています。  
  
```cpp#  
STDMETHODIMP CBreakpointErrorDebugEventBase::GetErrorBreakpoint(  
    IDebugErrorBreakpoint2 **ppbp)  
{  
    HRESULT hRes = E_FAIL;  
  
    if ( ppbp )  
    {  
        if ( m_pError )  
        {  
            *ppbp = m_pError;  
  
            m_pError->AddRef();  
  
            hRes = S_OK;  
        }  
        else  
            hRes = E_FAIL;  
    }  
    else  
        hRes = E_INVALIDARG;  
  
    return ( hRes );  
}  
```  
  
## <a name="see-also"></a>参照  
 [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)   
 [IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)   
 [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
