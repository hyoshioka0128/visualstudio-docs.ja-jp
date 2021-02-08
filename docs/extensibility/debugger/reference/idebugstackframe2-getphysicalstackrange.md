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
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8c4c4bbc468403aaf94aca1b5133a732e0c050b2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99837477"
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

## <a name="remarks"></a>解説
 このメソッドによって返される情報は、スタックフレームを並べ替えるためにセッションデバッグマネージャー (SDM) によって使用されます。

 呼び出し履歴が増加していることを前提としています。つまり、新しいスタックフレームはより低いメモリアドレスに追加されます。 実行時アーキテクチャは、この前提に一致する物理的なスタック範囲を提供する必要があります。

## <a name="see-also"></a>関連項目
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
