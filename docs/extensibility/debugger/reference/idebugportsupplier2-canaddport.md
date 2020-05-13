---
title: IDebugポートサプライヤー2::缶ポート |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::CanAddPort
helpviewer_keywords:
- IDebugPortSupplier2::CanAddPort
ms.assetid: 41f69e0a-e82c-473d-8b7a-0c40fc5730fc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5d0c67d62f57076f29f2c2ef60d456f517ae97fd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724748"
---
# <a name="idebugportsupplier2canaddport"></a>IDebugPortSupplier2::CanAddPort
ポートサプライヤーが新しいポートを追加できることを確認します。

## <a name="syntax"></a>構文

```cpp
HRESULT CanAddPort( 
   void 
);
```

```csharp
int CanAddPort();
```

## <a name="return-value"></a>戻り値
 ポートを追加できる場合は、戻`S_OK`ります。それ以外の`S_FALSE`場合は、このポート サプライヤーにポートを追加できることを示す戻り値を返します。

## <a name="remarks"></a>Remarks
 後者のメソッドはポートを作成し、追加するので[、AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)メソッドを呼び出す前にこのメソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
