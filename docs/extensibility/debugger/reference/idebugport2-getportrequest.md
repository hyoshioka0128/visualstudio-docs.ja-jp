---
description: ポートの作成に使用されたポート (使用可能な場合) の説明を取得します。
title: 'IDebugPort2:: GetPortRequest |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPort2::GetPortRequest
helpviewer_keywords:
- IDebugPort2::GetPortRequest
ms.assetid: 14abf847-0675-4fa8-872e-971e00c84224
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 084e8bb94356ea4e2cff1fa83e83e7e08b35134e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102142870"
---
# <a name="idebugport2getportrequest"></a>IDebugPort2::GetPortRequest
ポートの作成に使用されたポート (使用可能な場合) の説明を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetPortRequest( 
   IDebugPortRequest2** ppRequest
);
```

```csharp
int GetPortRequest( 
   out IDebugPortRequest2 ppRequest
);
```

## <a name="parameters"></a>パラメーター
`ppRequest`\
入出力ポートの作成に使用された要求を表す [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  `E_PORT_NO_REQUEST`ポートが[IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) port 要求を使用して作成されなかった場合は、を返します。

## <a name="see-also"></a>関連項目
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
- [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
