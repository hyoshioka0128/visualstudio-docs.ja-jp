---
description: 属性情報をバイトの blob として取得します。
title: 'IDebugCustomAttribute:: GetAttributeBytes |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute::GetAttributeBytes
helpviewer_keywords:
- IDebugCustomAttribute::GetAttributeBytes
ms.assetid: cf34583b-6530-4dcc-89f8-eb27e4e8d594
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d7cfc3ba650ff8277bb6cb85f5d1530d202bd426
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102163084"
---
# <a name="idebugcustomattributegetattributebytes"></a>IDebugCustomAttribute::GetAttributeBytes
属性情報をバイトの blob として取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAttributeBytes( 
   BYTE*  ppBlob,
   DWORD* pdwLen
);
```

```csharp
int GetAttributeBytes(
   ref byte[] ppBlob,
   ref uint   pdwLen
);
```

## <a name="parameters"></a>パラメーター
`ppBlob`\
[入力、出力]属性バイトで埋められる配列。

`pdwLen`\
[入力、出力]配列に返す最大バイト数を指定し、 `ppBlob` 実際に配列に書き込まれたバイト数を返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 パラメーターを `ppBlob` null 値に設定すると、使用可能な属性の数を返すことができます。 次に、配列を割り当て、その配列をパラメーターに対して渡し `ppBlob` ます。

 属性バイトは、カスタム属性の生データを表します。

## <a name="see-also"></a>関連項目
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
