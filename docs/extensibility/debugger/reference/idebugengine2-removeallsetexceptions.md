---
title: 'IDebugEngine2:: RemoveAllSetExceptions |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::RemoveAllSetExceptions
helpviewer_keywords:
- IDebugEngine2::RemoveAllSetExceptions
ms.assetid: 165fbe89-802d-4d99-85ca-c10fd6cccc09
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ae5ac703f1d0bd374131a4f5de397f39cf0ba209
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80731031"
---
# <a name="idebugengine2removeallsetexceptions"></a>IDebugEngine2::RemoveAllSetExceptions
IDE が特定のランタイムアーキテクチャまたは言語に対して設定した例外の一覧を削除します。

## <a name="syntax"></a>構文

```cpp
HRESULT RemoveAllSetExceptions( 
   REFGUID guidType
);
```

```csharp
int RemoveAllSetExceptions( 
   ref Guid guidType
);
```

## <a name="parameters"></a>パラメーター
`guidType`\
から言語の GUID、または実行時アーキテクチャに固有のデバッグエンジンの GUID のいずれかです。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドによって削除された例外は、 [Setexception](../../../extensibility/debugger/reference/idebugengine2-setexception.md) メソッドの以前の呼び出しによって設定されています。

 特定の例外を削除するには、 [Removesetexception](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md) メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)
