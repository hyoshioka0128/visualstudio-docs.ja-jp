---
title: 'IDebugStackFrame2:: GetPhysicalStackRange |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetPhysicalStackRange
helpviewer_keywords:
- IDebugStackFrame2::GetPhysicalStackRange
ms.assetid: 2f6992e2-ac1c-433f-83b7-a7f83a4ce63d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3df924c6c8a4373082d61575e4ad8a7ec3f161d1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80719670"
---
# <a name="idebugstackframe2getphysicalstackrange"></a>IDebugStackFrame2::GetPhysicalStackRange
スタックフレームに関連付けられている物理アドレスの範囲のコンピューターに依存する表現を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetPhysicalStackRange ( 
   UINT64* paddrMin,
   UINT64* paddrMax
);
```

```csharp
int GetPhysicalStackRange ( 
   out ulong paddrMin,
   out ulong paddrMax
);
```

## <a name="parameters"></a>パラメーター
`paddrMin`\
入出力このスタックフレームに関連付けられている最も低い物理アドレスを返します。

`paddrMax`\
入出力このスタックフレームに関連付けられている最も高い物理アドレスを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドによって返される情報は、スタックフレームを並べ替えるためにセッションデバッグマネージャー (SDM) によって使用されます。

 呼び出し履歴が増加していることを前提としています。つまり、新しいスタックフレームはより低いメモリアドレスに追加されます。 実行時アーキテクチャは、この前提に一致する物理的なスタック範囲を提供する必要があります。

## <a name="see-also"></a>関連項目
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
