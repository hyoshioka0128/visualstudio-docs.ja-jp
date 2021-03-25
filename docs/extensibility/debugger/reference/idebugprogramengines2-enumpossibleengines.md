---
description: このプログラムをデバッグできるすべてのデバッグエンジン (DE) の Guid を返します。
title: 'IDebugProgramEngines2:: Enumengine |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEngines2::EnumPossibleEngines
helpviewer_keywords:
- IDebugProgramEngines2::EnumPossibleEngines
ms.assetid: 993d70a4-f6a5-4e47-a603-0b162b9fde00
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2a49a0590a1ec2f0b0e7d2be59fe2161b438154a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084208"
---
# <a name="idebugprogramengines2enumpossibleengines"></a>IDebugProgramEngines2::EnumPossibleEngines
このプログラムをデバッグできるすべてのデバッグエンジン (DE) の Guid を返します。

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
から返される DE の Guid の数。 配列の最大サイズも指定し `rgguidEngines` ます。

`rgguidEngines`\
[入力、出力]入力する DE Guid の配列。

`pceltEngines`\
入出力返される逆 Guid の実際の数を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 `HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)`バッファーのサイズが十分でない場合は、[C++] または [C#] 0x8007007A を返します。

## <a name="remarks"></a>注釈
 存在するエンジンの数を確認するには、 `celtBuffer` パラメーターを0に設定し、 `rgguidEngines` パラメーターを null 値に設定して、このメソッドを1回呼び出します。 これは `HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)` (C# の場合は 0X8007007A) を返し、 `pceltEngines` パラメーターはバッファーに必要なサイズを返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)
