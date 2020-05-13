---
title: メッセージタイプ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MESSAGETYPE
helpviewer_keywords:
- MESSAGETYPE enumeration
ms.assetid: 800cc77d-3c27-4763-a9df-552a9384bd49
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b4d0fd12495a59427500c16ef6f37d9f8b6e61f5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714498"
---
# <a name="messagetype"></a>MESSAGETYPE
メッセージの種類と理由を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_MESSAGETYPE { 
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
public enum enum_MESSAGETYPE { 
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
 メッセージを出力ウィンドウに送信することを示します。 これは、 から`MT_MESSAGEBOX`相互に排他的です。

 `MT_MESSAGEBOX`\
 メッセージをメッセージ ボックスに表示することを示します。 これは、 から`MT_OUTPUTSTRING`相互に排他的です。

 `MT_TYPE_MASK`\
 メッセージの宛先を分離するためのマスク値。

 `MT_REASON_EXCEPTION`\
 例外の結果としてメッセージ ボックスが表示されることを示します。 これは、 から`MT_REASON_TRACEPOINT`相互に排他的です。

 `MT_REASON_TRACEPOINT`\
 トレース ポイントをヒットした結果、メッセージ ボックスが表示されることを示します。 これは相互に排他的です`MT_REASON_EXCEPTION`。

 `MT_REASON_MASK`\
 メッセージが表示される理由を分離するためのマスク値。

## <a name="remarks"></a>Remarks
 これらの値は、[メソッド](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)から返されます。 [GetErrorMessage](../../../extensibility/debugger/reference/idebugerrorevent2-geterrormessage.md)

 理由の値の 1 つは、ビットごとの`OR`を使用して出力先の値の 1 つと組み合わせることができます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)
- [GetErrorMessage](../../../extensibility/debugger/reference/idebugerrorevent2-geterrormessage.md)
