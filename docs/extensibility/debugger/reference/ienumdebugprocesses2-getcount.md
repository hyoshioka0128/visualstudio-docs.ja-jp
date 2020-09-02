---
title: 'IEnumDebugProcesses2:: GetCount |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugProcesses2::GetCount
helpviewer_keywords:
- IEnumDebugProcesses2::GetCount
ms.assetid: 5dc3e36c-46e5-4556-bf41-1870aa67d2a0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ae0d6541bd2dc33b751087dc2ca8ee8dfeabba8c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80715859"
---
# <a name="ienumdebugprocesses2getcount"></a>IEnumDebugProcesses2::GetCount
列挙体の要素の数を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCount(
   ULONG* pcelt
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
 このメソッドは `Next` 、、、 `Clone` `Skip` 、およびメソッドのみを `Reset` 実装する必要があることを指定する、慣例的な COM 列挙インターフェイスの一部ではありません。

## <a name="see-also"></a>関連項目
- [IEnumDebugProcesses2](../../../extensibility/debugger/reference/ienumdebugprocesses2.md)
