---
title: プログラムの公開を解除する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2::UnpublishProgram
helpviewer_keywords:
- IDebugProgramPublisher2::UnpublishProgram
ms.assetid: 627e7d38-b2ac-4873-9a40-37ff7f47cd1d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1fa3d111559a2c82fe36def202e5c1cf120c5202
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721589"
---
# <a name="idebugprogrampublisher2unpublishprogram"></a>IDebugProgramPublisher2::UnpublishProgram
プログラムをデバッグ不可にします。

## <a name="syntax"></a>構文

```cpp
HRESULT UnpublishProgram(
   IUnknown* pDebuggeeInterface
);
```

```csharp
int UnpublishProgram(
   object pDebuggeeInterface
);
```

## <a name="parameters"></a>パラメーター
`pDebuggeeInterface`\
[in]プログラム`IUnknown`へのインターフェイス。 これは[PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)メソッドに指定された値と同じであり、削除されるプログラムを一意に識別します (つまり、Cookie として使用されます)。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 デバッグ エンジンとセッション デバッグ マネージャーでプログラムを使用できるようにするには[、PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)メソッドを使用します。

## <a name="see-also"></a>関連項目
- [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)
- [PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)
