---
description: 式エバリュエーター (EE) が、デバッガーエンジン (DE) がメトリック設定の読み取りに使用するコールバックインターフェイスを指定できるようにします。
title: 'IDebugExpressionEvaluator2:: SetCallback |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugExpressionEvaluator2::SetCallback
- SetCallback
ms.assetid: 31e3a99e-e784-44a3-8b19-cc5ef31ed546
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fc858ab5d26ccffe33d26296e033ac577ddba440
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102152391"
---
# <a name="idebugexpressionevaluator2setcallback"></a>IDebugExpressionEvaluator2::SetCallback
式エバリュエーター (EE) が、デバッガーエンジン (DE) がメトリック設定の読み取りに使用するコールバックインターフェイスを指定できるようにします。

## <a name="syntax"></a>構文

```cpp
HRESULT SetCallback (
    IDebugSettingsCallback2* pCallback
);
```

```csharp
int SetCallback (
    IDebugSettingsCallback2 pCallback
);
```

## <a name="parameters"></a>パラメーター
`pCallback`\
から設定コールバックに使用するインターフェイス。

## <a name="return-value"></a>戻り値
成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
このメソッドは、式エバリュエーターがメトリック設定を読み取るために使用できるセッションデバッグマネージャーへのインターフェイスを提供します。 リモートデバッグでコンピューターのメトリックを読み取る場合に便利です [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 。

## <a name="example"></a>例
次の例は、 [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)インターフェイスを公開する **CEE** オブジェクトに対してこのメソッドを実装する方法を示しています。

```cpp
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

## <a name="see-also"></a>関連項目
- [IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)
