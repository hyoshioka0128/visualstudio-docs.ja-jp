---
title: 'IEnumDebugModules2:: Clone |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugModules2::Clone
helpviewer_keywords:
- IEnumDebugModules2::Clone
ms.assetid: fd6d3abc-20d9-4f6f-9c8e-5bd29f68d47d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f008cef55d45257ddd18dec69d6e72be8095ed57
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99932829"
---
# <a name="ienumdebugmodules2clone"></a>IEnumDebugModules2::Clone
現在の列挙体のコピーを別のオブジェクトとして返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Clone(
   IEnumDebugModules2** ppEnum
);
```

```csharp
int Clone(
   out IEnumDebugModules2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
入出力この列挙体のコピーを別のオブジェクトとして返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 列挙体のコピーは、このメソッドが呼び出されたときの元の状態と同じ状態になります。 ただし、コピーと元の状態は別々であり、個別に変更できます。

## <a name="see-also"></a>関連項目
- [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)
