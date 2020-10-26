---
title: 'IDebugExceptionEvent2:: GetExceptionDescription |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::GetExceptionDescription
helpviewer_keywords:
- IDebugExceptionEvent2::GetExceptionDescription
ms.assetid: d07d458f-5729-47e4-9b77-1bd59c61a75a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7a6ea64540eaeef5ec258bc54b118b3a0600584c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80729851"
---
# <a name="idebugexceptionevent2getexceptiondescription"></a>IDebugExceptionEvent2::GetExceptionDescription
例外のわかり可能な説明を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetExceptionDescription( 
   BSTR* pbstrDescription
);
```

```csharp
int GetExceptionDescription( 
   out string pbstrDescription
);
```

## <a name="parameters"></a>パラメーター
`pbstrDescription`\
入出力例外のわかり可能な説明を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドから返される文字列は、通常、例外の名前であり、例外が発生したときに [ **出力** ] ウィンドウに表示されます。

## <a name="see-also"></a>関連項目
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
