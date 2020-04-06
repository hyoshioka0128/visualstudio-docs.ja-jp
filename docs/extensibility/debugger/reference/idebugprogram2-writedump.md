---
title: プログラム2::書き込みダンプ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::WriteDump
helpviewer_keywords:
- IDebugProgram2::WriteDump
ms.assetid: 375afb8c-882d-44db-bfa7-e2c9eb555122
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 333535a727d88f66346ba4c94cb08b4917b8acfd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722741"
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
[in]ダンプの種類を指定する[DUMPTYPE](../../../extensibility/debugger/reference/dumptype.md)列挙体の値。たとえば、短いまたは長い。

`pszDumpUrl`\
[in]ダンプを書き込む先の URL。 通常、これは の形式ですが、`file://c:\path\filename.ext`任意の有効な URL を使用できます。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 プログラム ダンプには、通常、現在のスタック フレーム、スタック自体、プログラムで実行されているスレッドのリスト、およびプログラムが所有するメモリが含まれます。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
