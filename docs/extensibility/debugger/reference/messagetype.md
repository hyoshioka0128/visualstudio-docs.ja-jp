---
title: MESSAGETYPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MESSAGETYPE
helpviewer_keywords:
- MESSAGETYPE enumeration
ms.assetid: 800cc77d-3c27-4763-a9df-552a9384bd49
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9735c394e0b88dbe7ea3a5113026d4012839b8fd
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99961990"
---
# <a name="messagetype"></a>MESSAGETYPE
メッセージの種類と理由を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_MESSAGETYPE { 
   MT_OUTPUTSTRING      = 0x0000001,
   MT_MESSAGEBOX        = 0x00000002,
   MT_TYPE_MASK         = 0x000000FF,
   MT_REASON_EXCEPTION  = 0x00000100,
   MT_REASON_TRACEPOINT = 0x00000200,
   MT_REASON_MASK       = 0x0000FF00
};
typedef DWORD MESSAGETYPE;
```

```csharp
public enum enum_MESSAGETYPE { 
   MT_OUTPUTSTRING      = 0x0000001,
   MT_MESSAGEBOX        = 0x00000002,
   MT_TYPE_MASK         = 0x000000FF,
   MT_REASON_EXCEPTION  = 0x00000100,
   MT_REASON_TRACEPOINT = 0x00000200,
   MT_REASON_MASK       = 0x0000FF00
};
```

## <a name="fields"></a>フィールド
 `MT_OUTPUTSTRING`\
 メッセージを出力ウィンドウに送信することを示します。 これは、とは相互に排他的です `MT_MESSAGEBOX` 。

 `MT_MESSAGEBOX`\
 メッセージがメッセージボックスに表示されることを示します。 これは、とは相互に排他的です `MT_OUTPUTSTRING` 。

 `MT_TYPE_MASK`\
 メッセージの送信先を分離するマスク値。

 `MT_REASON_EXCEPTION`\
 メッセージボックスが例外の結果として表示されていることを示します。 これは、とは相互に排他的です `MT_REASON_TRACEPOINT` 。

 `MT_REASON_TRACEPOINT`\
 トレースポイントをヒットした結果としてメッセージボックスが表示されていることを示します。 これは、とは相互に排他的です `MT_REASON_EXCEPTION` 。

 `MT_REASON_MASK`\
 表示されるメッセージの理由を特定するマスク値。

## <a name="remarks"></a>解説
 これらの値は、 [GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md) メソッドと [GetErrorMessage](../../../extensibility/debugger/reference/idebugerrorevent2-geterrormessage.md) メソッドから返されます。

 いずれかの理由値を、ビットごとのを使用して出力先の値の1つと組み合わせることができ `OR` ます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)
- [GetErrorMessage](../../../extensibility/debugger/reference/idebugerrorevent2-geterrormessage.md)
