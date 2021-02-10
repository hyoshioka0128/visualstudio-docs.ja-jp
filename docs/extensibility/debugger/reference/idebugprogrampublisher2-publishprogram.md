---
title: IDebugProgramPublisher2::P ublishProgram |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2::PublishProgram
helpviewer_keywords:
- IDebugProgramPublisher2::PublishProgram
ms.assetid: 92ff63f0-e869-4040-b3ae-b2c899e708ff
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1d13154f172fdd92ea4a3d4c96321e884516a74c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99959559"
---
# <a name="idebugprogrampublisher2publishprogram"></a>IDebugProgramPublisher2::PublishProgram
このメソッドにより、プログラムがデバッグエンジン (DEs) とセッションデバッグマネージャーで使用できるようになります。

## <a name="syntax"></a>構文

```cpp
HRESULT PublishProgram(
   CONST_GUID_ARRAY Engines,
   LPCOLESTR        szFriendlyName,
   IUnknown*        pDebuggeeInterface
);
```

```csharp
int PublishProgram(
   CONST_GUID_ARRAY Engines,
   string           szFriendlyName,
   object           pDebuggeeInterface
);
```

## <a name="parameters"></a>パラメーター
`Engines`\
からこのプログラムに対して起動またはアタッチできる DEs の Guid の配列。

`szFriendlyName`\
からプログラムのフレンドリ名です (これは、ユーザーに表示されるメニューまたはダイアログで表示されます)。

`pDebuggeeInterface`\
[入力] `IUnknown` プログラムのインターフェイス (この値はプログラムを一意に識別するためにクッキーとして使用されます。この同じ値を使用してプログラムを "発行解除" します)

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 プログラムをデバッグに使用できないようにするには、 [Unpublishprogram](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogram.md)を呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)
- [UnpublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogram.md)
