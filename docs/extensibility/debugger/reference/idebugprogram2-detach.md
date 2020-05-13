---
title: Iデバッグプログラム2::Dエタッハ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Detach
helpviewer_keywords:
- IDebugProgram2::Detach
ms.assetid: 5e8d88b0-a8d4-4746-88c0-ad332ee73f33
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e177b1347981e420223ecafad18eedcf9de30234
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723060"
---
# <a name="idebugprogram2detach"></a>IDebugProgram2::Detach
プログラムからデバッグ エンジンをデタッチします。

## <a name="syntax"></a>構文

```cpp
HRESULT Detach( 
   void 
);
```

```csharp
int Detach();
```

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 デタッチされたプログラムは実行を継続しますが、デバッグ セッションの一部ではなくなります。 デバッグ エンジンがデタッチされると、プログラムのデバッグ イベントは送信されません。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
