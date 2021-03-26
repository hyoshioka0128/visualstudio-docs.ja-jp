---
description: このメソッドにより、プログラムがデバッグエンジン (DEs) とセッションデバッグマネージャーで使用できるようになります。
title: IDebugProgramPublisher2::P ublishProgram |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2::PublishProgram
helpviewer_keywords:
- IDebugProgramPublisher2::PublishProgram
ms.assetid: 92ff63f0-e869-4040-b3ae-b2c899e708ff
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ba1ac74813ea0c3ae5b7eadb26d540b7bfe20707
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065230"
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

## <a name="remarks"></a>注釈
 プログラムをデバッグに使用できないようにするには、 [Unpublishprogram](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogram.md)を呼び出します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)
- [UnpublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogram.md)
