---
title: 'IDebugExceptionEvent2:: GetException |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::GetException
helpviewer_keywords:
- IDebugExceptionEvent2::GetException
ms.assetid: 7c98f41d-322b-4e72-a514-cbd4823eb70d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 332cbb28bd175aa5c3b4187ae735a479ba9de6b0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80729863"
---
# <a name="idebugexceptionevent2getexception"></a>IDebugExceptionEvent2::GetException
このイベントを発生させた例外の詳細な説明を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetException( 
   EXCEPTION_INFO* pExceptionInfo
);
```

```csharp
int GetException( 
   EXCEPTION_INFO[] pExceptionInfo
);
```

## <a name="parameters"></a>パラメーター
`pExceptionInfo`\
[入力、出力]例外の説明と共に入力される [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) 構造体。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説

 [C++ のみ]呼び出し元は、構造内の[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)オブジェクトを解放するだけでなく、 [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)構造体内の任意の文字列を解放する役割も担います。

## <a name="see-also"></a>関連項目
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
