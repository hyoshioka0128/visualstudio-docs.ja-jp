---
title: 'IDebugPendingBreakpoint2:: EnumErrorBreakpoints ポイント |Microsoft Docs'
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
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 34336c51d51c50f6dee7239a38588f36c935edbd
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99934352"
---
# <a name="idebugpendingbreakpoint2enumerrorbreakpoints"></a>IDebugPendingBreakpoint2::EnumErrorBreakpoints
この保留中のブレークポイントが原因で発生したすべてのエラーブレークポイントの一覧を取得します。

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
から列挙するエラーの種類を選択する [BP_ERROR_TYPE](../../../extensibility/debugger/reference/bp-error-type.md) 列挙の値の組み合わせ。

`ppEnum`\
入出力[IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)オブジェクトの一覧を含む[IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 `E_BP_DELETED`ブレークポイントが削除されている場合は、を返します。

## <a name="example"></a>例
 次の例は、IDebugPendingBreakpoint2 インターフェイスを公開する単純なオブジェクトに対してこのメソッドを実装する方法を示して `CPendingBreakpoint` います。 [](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)

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
