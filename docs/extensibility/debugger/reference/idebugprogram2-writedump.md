---
title: 'IDebugProgram2:: WriteDump |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::WriteDump
helpviewer_keywords:
- IDebugProgram2::WriteDump
ms.assetid: 375afb8c-882d-44db-bfa7-e2c9eb555122
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 265c77acdb15069c1fcd7f33d93d4ff74a528eca
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99896150"
---
# <a name="idebugprogram2writedump"></a>IDebugProgram2::WriteDump
ダンプをファイルに書き込みます。

## <a name="syntax"></a>構文

```cpp
HRESULT WriteDump( 
   DUMPTYPE  DumpType,
   LPCOLESTR pszDumpUrl
);
```

```csharp
int WriteDump( 
   enum_DUMPTYPE  DumpType,
   string         pszDumpUrl
);
```

## <a name="parameters"></a>パラメーター
`DumpType`\
からダンプの種類 (short、long など) を指定する [dumptype](../../../extensibility/debugger/reference/dumptype.md) 列挙の値です。

`pszDumpUrl`\
からダンプの書き込み先の URL。 通常、これはの形式です `file://c:\path\filename.ext` が、任意の有効な URL にすることができます。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 通常、プログラムダンプには、現在のスタックフレーム、スタック自体、プログラムで実行されているスレッドの一覧、およびプログラムが所有するメモリが含まれます。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
