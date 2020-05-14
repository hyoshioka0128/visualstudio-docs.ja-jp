---
title: ステートメントを設定します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::SetNextStatement
helpviewer_keywords:
- IDebugThread2::SetNextStatement
ms.assetid: 9e2834dd-4ecf-45af-8e6c-f9318ebdac06
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4b390e5c021fa069ae3fb09eef1978caaf9cc8ed
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718653"
---
# <a name="idebugthread2setnextstatement"></a>IDebugThread2::SetNextStatement
現在の命令ポインターを指定されたコード コンテキストに設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetNextStatement ( 
   IDebugStackFrame2*  pStackFrame,
   IDebugCodeContext2* pCodeContext
);
```

```csharp
int SetNextStatement ( 
   IDebugStackFrame2  pStackFrame,
   IDebugCodeContext2 pCodeContext
);
```

## <a name="parameters"></a>パラメーター
`pStackFrame`\
将来の使用のために予約されています。null 値に設定されます。

`pCodeContext`\
[in]実行されるコードの場所とそのコンテキストを記述する[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 次の表に、その他の値を示します。

|[値]|説明|
|-----------|-----------------|
|E_CANNOT_SET_NEXT_STATEMENT_ON_NONLEAF_FRAME|次のステートメントは、フレーム スタックの深いスタック フレームに入れることはできません。|
|E_CANNOT_SETIP_TO_DIFFERENT_FUNCTION|次のステートメントは、スタック内のどのフレームにも関連付けされません。|
|E_CANNOT_SET_NEXT_STATEMENT_ON_EXCEPTION|一部のデバッグ エンジンでは、例外の後に次のステートメントを設定できません。|

## <a name="remarks"></a>Remarks
 命令ポインターは、次に実行する命令またはステートメントを示します。 このメソッドは、ソース コードの行を再試行したり、別の関数で実行を継続するように強制するために使用します。

## <a name="see-also"></a>関連項目
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
