---
description: このデバッグイベントの属性を取得します。
title: 'IDebugEvent2:: GetAttributes |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEvent2::GetAttributes
helpviewer_keywords:
- IDebugEvent2::GetAttributes
ms.assetid: 2ac5b5fb-da17-43f7-811a-313f677e60d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b41e3f50b73c16c9acb28a809b8c33b535370c47
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065854"
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

## <a name="remarks"></a>注釈
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、すべてのイベントに共通です。 このメソッドは、イベントの種類を表します。たとえば、イベントは同期または非同期であり、イベントは停止イベントです。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md)
