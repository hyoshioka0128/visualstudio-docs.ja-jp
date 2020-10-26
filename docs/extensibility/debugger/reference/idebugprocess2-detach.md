---
title: IDebugProcess2::D etach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::Detach
helpviewer_keywords:
- IDebugProcess2::Detach
ms.assetid: ee2b9084-2db1-4e49-a1d9-387284b7c3f8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9036ebc44835ab6c3ebd08b9fad4408d9cb97461
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80724124"
---
# <a name="idebugprocess2detach"></a>IDebugProcess2::Detach
プロセス内のすべてのプログラムをデタッチして、このプロセスからデバッガーをデタッチします。

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
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 すべてのプログラムとプロセスは引き続き実行されますが、デバッグセッションの一部ではなくなります。 デタッチ操作が完了すると、このプロセス (およびそのプログラム) のデバッグイベントは送信されなくなります。

## <a name="see-also"></a>関連項目
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
