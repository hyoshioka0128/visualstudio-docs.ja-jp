---
title: 'IDebugProcess3:: Getenc State |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::GetENCAvailableState
helpviewer_keywords:
- IDebugProcess3::GetENCAvailableState
ms.assetid: 98a5d527-8a72-476c-8e92-0bff3d97c195
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dce751223c4513733c5cd9ce815155b7f659b54a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99915272"
---
# <a name="idebugprocess3getencavailablestate"></a>IDebugProcess3::GetENCAvailableState
このメソッドは、プロセスの現在のエディットコンティニュの状態を取得します。 カスタムポート供給業者は常にを返す必要があり `E_NOTIMPL` ます。

## <a name="syntax"></a>構文

```cpp
HRESULT GetENCAvailableState(
   EncUnavailableReason* pReason
);
```

```csharp
int GetENCAvailableState(
   EncUnavailableReason[] pReason
);
```

## <a name="parameters"></a>パラメーター
`pReason`\
入出力 [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md) 列挙の値です。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

> [!NOTE]
> カスタムポート供給業者は常にを返す必要があり `E_NOTIMPL` ます。

## <a name="remarks"></a>解説
 この状態は、 [Disableenc](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)によって影響を受ける可能性があります。

## <a name="see-also"></a>関連項目
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)
- [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md)
