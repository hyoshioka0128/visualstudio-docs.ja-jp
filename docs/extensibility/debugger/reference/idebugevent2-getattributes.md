---
title: 'IDebugEvent2:: GetAttributes |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEvent2::GetAttributes
helpviewer_keywords:
- IDebugEvent2::GetAttributes
ms.assetid: 2ac5b5fb-da17-43f7-811a-313f677e60d7
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 64f4b404938143e5b1531798b1cded7ac6218de6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99888278"
---
# <a name="idebugevent2getattributes"></a>IDebugEvent2::GetAttributes
このデバッグイベントの属性を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAttribute( 
   DWORD* pdwAttrib
);
```

```csharp
int GetAttribute( 
   out uint pdwAttrib
);
```

## <a name="parameters"></a>パラメーター
`pdwAttrib`\
入出力 [Eventattributes](../../../extensibility/debugger/reference/eventattributes.md) 列挙のフラグの組み合わせ。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、すべてのイベントに共通です。 このメソッドは、イベントの種類を表します。たとえば、イベントは同期または非同期であり、イベントは停止イベントです。

## <a name="see-also"></a>関連項目
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md)
