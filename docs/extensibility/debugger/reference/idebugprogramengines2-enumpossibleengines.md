---
title: IDebugプログラムエンジン2::列挙可能なエンジン |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEngines2::EnumPossibleEngines
helpviewer_keywords:
- IDebugProgramEngines2::EnumPossibleEngines
ms.assetid: 993d70a4-f6a5-4e47-a603-0b162b9fde00
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 45916edbef4368c58f83426d6c73f3c692236cb9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722434"
---
# <a name="idebugprogramengines2enumpossibleengines"></a>IDebugProgramEngines2::EnumPossibleEngines
このプログラムをデバッグできるすべての使用可能なデバッグ エンジン (DE) の GUID を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumPossibleEngines( 
   DWORD  celtBuffer,
   GUID*  rgguidEngines,
   DWORD* pceltEngines
);
```

```csharp
int EnumPossibleEngines( 
   uint      celtBuffer,
   GUID[]    rgguidEngines,
   ref DWORD pceltEngines
);
```

## <a name="parameters"></a>パラメーター
`celtBuffer`\
[in]返す DE GUID の数。 これは、配列の最大サイズも指定`rgguidEngines`します。

`rgguidEngines`\
[イン、アウト]入力する DE GUID の配列。

`pceltEngines`\
[アウト]返される実際の DE GUID の数を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 バッファーの大きさが`HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)`十分でない場合は、[C++] または [C#] 0x8007007A を返します。

## <a name="remarks"></a>Remarks
 エンジンの数を確認するには、パラメータを 0 に設定し、`celtBuffer`パラメータを`rgguidEngines`null 値に設定して、このメソッドを 1 回呼び出します。 これは(C# の場合は 0x8007007A)を返`HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)`し、パラメータは`pceltEngines`バッファの必要なサイズを返します。

## <a name="see-also"></a>関連項目
- [IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)
