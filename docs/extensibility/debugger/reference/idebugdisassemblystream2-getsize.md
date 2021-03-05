---
description: この逆アセンブリストリームの命令のサイズを取得します。
title: 'IDebugDisassemblyStream2:: GetSize |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::GetSize
helpviewer_keywords:
- IDebugDisassemblyStream2::GetSize
ms.assetid: 8f512704-12d0-46d2-959a-4f8dffe117b5
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 94207c8e14306049068e838971aa778290de2ba6
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102154367"
---
# <a name="idebugdisassemblystream2getsize"></a>IDebugDisassemblyStream2::GetSize
この逆アセンブリストリームの命令のサイズを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetSize( 
   UINT64* pnSize
);
```

```csharp
int GetSize( 
   out ulong pnSize
);
```

## <a name="parameters"></a>パラメーター
`pnSize`\
入出力は、の指示に従ってサイズを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドから返される値を使用すると、 [Disassemblydata](../../../extensibility/debugger/reference/disassemblydata.md) 構造体の配列を割り当てて、そのデータを [Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md) メソッドに渡すことができます。

## <a name="see-also"></a>関連項目
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
- [読み取り](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)
