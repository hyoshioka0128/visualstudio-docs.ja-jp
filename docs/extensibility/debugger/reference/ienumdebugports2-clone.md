---
title: 'IEnumDebugPorts2:: Clone |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPorts2::Clone
helpviewer_keywords:
- IEnumDebugPorts2::Clone
ms.assetid: d5ce77e8-bb99-409a-98fa-20fe5a0de25e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 87842dfdb3de6ce120967bbbff785a1ec84f9ba4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80716225"
---
# <a name="ienumdebugports2clone"></a>IEnumDebugPorts2::Clone
現在の列挙体のコピーを別のオブジェクトとして返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Clone(
   IEnumDebugPorts2** ppEnum
);
```

```csharp
int Clone(
   out IEnumDebugPorts2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
入出力この列挙体のコピーを別のオブジェクトとして返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 列挙体のコピーは、このメソッドが呼び出されたときの元の状態と同じ状態になります。 ただし、コピーと元の状態は別々であり、個別に変更できます。

## <a name="see-also"></a>関連項目
- [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md)
