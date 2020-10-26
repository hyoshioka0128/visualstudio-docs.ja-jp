---
title: 'IDebugExpressionEvaluator2:: SetCallback |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugExpressionEvaluator2::SetCallback
- SetCallback
ms.assetid: 31e3a99e-e784-44a3-8b19-cc5ef31ed546
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8d6f715bb33afe051cdccffbf3219e062b606f57
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68179924"
---
# <a name="idebugexpressionevaluator2setcallback"></a>IDebugExpressionEvaluator2::SetCallback
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

式エバリュエーター (EE) が、デバッガーエンジン (DE) がメトリック設定の読み取りに使用するコールバックインターフェイスを指定できるようにします。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT SetCallback (  
   IDebugSettingsCallback2* pCallback  
);  
```  
  
```csharp  
int SetCallback (  
   IDebugSettingsCallback2 pCallback  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pCallback`  
 から設定コールバックに使用するインターフェイス。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドは、式エバリュエーターがメトリック設定を読み取るために使用できるセッションデバッグマネージャーへのインターフェイスを提供します。 リモートデバッグでコンピューターのメトリックを読み取る場合に便利です [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 。  
  
## <a name="example"></a>例  
 次の例は、 [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)インターフェイスを公開する**CEE**オブジェクトに対してこのメソッドを実装する方法を示しています。  
  
```cpp#  
HRESULT CEE::SetCallback(IDebugSettingsCallback2* in_pCallback)  
{  
    // precondition  
    INVARIANT( this );  
  
    // function body  
    if (NULL != this->m_LanguageSpecificUseCases.pfSetCallback)  
    {  
        EEDomain::fSetCallback DomainVal =  
        {  
            in_pCallback  
        };  
  
        BOOL bSuccess = (*this->m_LanguageSpecificUseCases.pfSetCallback)(DomainVal);  
        ENSURE( bSuccess );  
    }  
  
    // postcondition  
    INVARIANT( this );  
  
    return S_OK;  
}  
```  
  
## <a name="see-also"></a>参照  
 [IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)
