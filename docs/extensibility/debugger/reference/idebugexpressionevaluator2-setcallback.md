---
title: 検証評価関数2::セットコールバック |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugExpressionEvaluator2::SetCallback
- SetCallback
ms.assetid: 31e3a99e-e784-44a3-8b19-cc5ef31ed546
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 907fdaa928b3f84f6ff37490d5c54a9d48515053
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729334"
---
# <a name="idebugexpressionevaluator2setcallback"></a>IDebugExpressionEvaluator2::SetCallback
式エバリュエーター (EE) が、デバッガー エンジン (DE) がメトリック設定の読み取りに使用するコールバック インターフェイスを指定できるようにします。

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
[in]設定コールバックに使用するインターフェイス。

## <a name="return-value"></a>戻り値
成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
このメソッドは、式エバリュエーターがメトリック設定を読み取るために使用できるセッション デバッグ マネージャーへのインターフェイスを提供します。 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]リモート デバッグでは、コンピューターのメトリックを読み取るのに役立ちます。

## <a name="example"></a>例
次の例は、[インターフェイス](../../../extensibility/debugger/reference/idebugsettingscallback2.md)を公開する**CEE**オブジェクトに対してこのメソッドを実装する方法を示しています。

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
