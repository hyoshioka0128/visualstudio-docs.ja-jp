---
description: このメソッドは、フィールドに関する拡張情報を取得します。
title: 'IDebugField:: GetExtendedInfo |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetExtendedInfo
helpviewer_keywords:
- IDebugField::GetExtendedInfo method
ms.assetid: 46c0dd4d-4fd5-4efd-a908-71e4248e8e8d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3e17c824d2be7ff12e3e967b953e25359b650b1c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077071"
---
# <a name="idebugfieldgetextendedinfo"></a>IDebugField::GetExtendedInfo
このメソッドは、フィールドに関する拡張情報を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetExtendedInfo( 
   REFGUID guidExtendedInfo,
   BYTE**  prgBuffer,
   DWORD*  pdwLen
);
```

```csharp
int GetExtendedInfo(
   ref Guid guidExtendedInfo,
   IntPtr[] prgBuffer,
   ref uint pdwLen
);
```

## <a name="parameters"></a>パラメーター
`guidExtendedInfo`\
から返される情報を選択します。 次の値を指定できます。

|値|説明|
|-----------|-----------------|
|`guidConstantValue`|バイトシーケンスとしての値。|
|`guidConstantType`|型のシグネチャとしての型。|

`prgBuffer`\
入出力拡張された情報を返します。

`pdwLen`\
[入力、出力]拡張情報のサイズをバイト単位で返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 現在、このメソッドは定数の型または値のみを返します。 呼び出し元は、 `prgBuffer` COM の `CoTaskMemFree` 関数 (C++) または (C#) を呼び出すことによって、で返されたバッファーを解放する必要があり <xref:System.Runtime.InteropServices.Marshal.FreeCoTaskMem%2A> ます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
