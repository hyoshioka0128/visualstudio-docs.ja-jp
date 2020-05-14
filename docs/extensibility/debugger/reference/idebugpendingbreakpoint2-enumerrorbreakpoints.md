---
title: を次の 2::列挙エラーブレークポイント |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::EnumErrorBreakpoints
helpviewer_keywords:
- IDebugPendingBreakpoint2::EnumErrorBreakpoints method
- EnumErrorBreakpoints method
ms.assetid: 2f9a9720-c1ac-4430-8f28-200d85360452
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 11caf8c2af92a14e001d7403f2457f0fc66ff3ed
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725851"
---
# <a name="idebugpendingbreakpoint2enumerrorbreakpoints"></a>IDebugPendingBreakpoint2::EnumErrorBreakpoints
この保留中のブレークポイントから発生したすべてのエラー ブレークポイントの一覧を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumErrorBreakpoints( 
   BP_ERROR_TYPE                 bpErrorType,
   IEnumDebugErrorBreakpoints2** ppEnum
);
```

```csharp
int EnumErrorBreakpoints( 
   enum_BP_ERROR_TYPE              bpErrorType,
   out IEnumDebugErrorBreakpoints2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`bpErrorType`\
[in]列挙するエラーの種類を選択する[BP_ERROR_TYPE](../../../extensibility/debugger/reference/bp-error-type.md)列挙体の値の組み合わせ。

`ppEnum`\
[アウト]オブジェクトの一覧[を](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)含むオブジェクト[を](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 ブレークポイント`E_BP_DELETED`が削除されたかどうかを返します。

## <a name="example"></a>例
 次の例は[、IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)インターフェイス`CPendingBreakpoint`を公開する単純なオブジェクトに対してこのメソッドを実装する方法を示しています。

```cpp
HRESULT CPendingBreakpoint::EnumErrorBreakpoints(
   BP_ERROR_TYPE bpErrorType,
   IEnumDebugErrorBreakpoints2** ppEnum)
{
   HRESULT hr;

   // Verify that the passed IEnumDebugErrorBreakpoints2 interface pointer
   // is valid.
   if (ppEnum)
   {
      // Verify that the pending breakpoint has not been deleted. If
      // deleted, then return hr = E_BP_DELETED.
      if (m_state.state != PBPS_DELETED)
      {
         // Verify that this error is not a warning.
         // All errors supported by this DE are errors, not warnings.
         if (IsFlagSet(bpErrorType, BPET_TYPE_ERROR) && m_pErrorBP)
         {
            // Get the error breakpoint.
            CComPtr<IDebugErrorBreakpoint2> spErrorBP;
            hr = m_pErrorBP->QueryInterface(&spErrorBP);
            assert(hr == S_OK);
            if (hr == S_OK)
            {
               // Create the error breakpoint enumerator.
               CComObject<CEnumDebugErrorBreakpoints>* pErrorEnum;
               hr = CComObject<CEnumDebugErrorBreakpoints>::CreateInstance(&pErrorEnum);
               assert(hr == S_OK);
               if (hr == S_OK)
               {
                  // Initialize the enumerator of error breakpoints with
                  // the IDebugErrorBreakpoint2 information.
                  IDebugErrorBreakpoint2* rgpErrorBP[] = { spErrorBP.p };
                  hr = pErrorEnum->Init(rgpErrorBP, &(rgpErrorBP[1]), NULL, AtlFlagCopy);
                  if (hr == S_OK)
                  {
                     // Verify that the passed IEnumDebugErrorBreakpoints2
                     // interface can be queried by the created
                     // CEnumDebugErrorBreakpoints object.
                     hr = pErrorEnum->QueryInterface(ppEnum);
                     assert(hr == S_OK);
                  }

                  // Otherwise, delete the CEnumDebugErrorBreakpoints
                  // object.
                  if (FAILED(hr))
                  {
                     delete pErrorEnum;
                  }
               }
            }
         }
         else
         {
            hr = S_FALSE;
         }
      }
      else
      {
         hr = E_BP_DELETED;
      }
   }
   else
   {
      hr = E_INVALIDARG;
   }

   return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [BP_ERROR_TYPE](../../../extensibility/debugger/reference/bp-error-type.md)
- [IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)
- [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
