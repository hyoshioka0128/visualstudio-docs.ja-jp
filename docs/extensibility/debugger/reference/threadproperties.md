---
title: スレッドプロパティ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- THREADPROPERTIES
helpviewer_keywords:
- THREADPROPERTIES structure
ms.assetid: 7d397207-db03-4ec0-9f79-3794056ed89f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bd0ed4e33b1f8e0e905f3c88493c9f513c177fbc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713432"
---
# <a name="threadproperties"></a>THREADPROPERTIES
スレッドのプロパティを記述します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagTHREADPROPERTIES { 
   THREADPROPERTY_FIELDS dwFields;
   DWORD                 dwThreadId;
   DWORD                 dwSuspendCount;
   DWORD                 dwThreadState;
   BSTR                  bstrPriority;
   BSTR                  bstrName;
   BSTR                  bstrLocation;
} THREADPROPERTIES;
```

```csharp
public struct THREADPROPERTIES { 
   public uint   dwFields;
   public uint   dwThreadId;
   public uint   dwSuspendCount;
   public uint   dwThreadState;
   public string bstrPriority;
   public string bstrName;
   public string bstrLocation;
};
```

## <a name="members"></a>メンバー
 `dwFields`\
 [THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md)列挙体のフラグの組み合わせで、この構造体のどのフィールドが有効かを示します。

 `dwThreadId`\
 スレッド ID。

 `dwSuspendCount`\
 スレッドの中断カウント。

 `dwThreadState`\
 操作スレッドの状態を示す[THREADSTATE](../../../extensibility/debugger/reference/threadstate.md)列挙体の値。

 `bstrPriority`\
 スレッドの優先順位を指定する文字列。たとえば、「標準を上回る」、「正常」、または「時間が重要」です。

 `bstName`\
 スレッド名。

 `bstrLocation`\
 スレッドの場所 (通常は最上位のスタック フレーム) は、通常、現在実行が停止されているメソッドの名前として表されます。

## <a name="remarks"></a>Remarks
 この構造体は、[メソッド](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)の呼び出しによって入力されます。 返される情報は、通常、**スレッド**ウィンドウの設定に使用されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)
- [THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md)
- [THREADSTATE](../../../extensibility/debugger/reference/threadstate.md)
