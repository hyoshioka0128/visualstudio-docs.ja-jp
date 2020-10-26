---
title: 'IEnumDebugObjects:: GetCount |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugObjects::GetCount
helpviewer_keywords:
- IEnumDebugObjects::GetCount method
ms.assetid: 9cbc5db4-03ae-479f-a664-13cad66ad210
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1475652e340ff793dc900ab11563c0c1ad82c9b1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80716349"
---
# <a name="ienumdebugobjectsgetcount"></a>IEnumDebugObjects::GetCount
このメソッドは、列挙体の要素の数を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCount(
   [out] ULONG* pcelt
);
```

```csharp
int GetCount(
   out uint pcelt
);
```

## <a name="parameters"></a>パラメーター
`pcelt`\
入出力列挙体の要素の数を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドは、次、複製、スキップ、およびリセットのみを実装する必要があることを指定する、慣例的な COM 列挙インターフェイスの一部ではありません。

## <a name="see-also"></a>関連項目
- [IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md)
