---
description: このメソッドは、このプログラムのエディットコンティニュ (ENC) 更新プログラムを取得します。
title: 'IDebugProgram2:: GetENCUpdate |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetENCUpdate
helpviewer_keywords:
- IDebugProgram2::GetENCUpdate
ms.assetid: 9832aac8-6320-4fd8-91dd-2a0852febb00
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 02446dba5450b89b769e773563f77cd6d8c1659f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102159901"
---
# <a name="idebugprogram2getencupdate"></a>IDebugProgram2::GetENCUpdate
このメソッドは、このプログラムのエディットコンティニュ (ENC) 更新プログラムを取得します。 カスタムデバッグエンジンは常にを返し `E_NOTIMPL` ます。

## <a name="syntax"></a>構文

```cpp
HRESULT GetENCUpdate( 
   IUnknown** ppUpdate
);
```

```csharp
int GetENCUpdate(
   out object ppUpdate
);
```

## <a name="parameters"></a>パラメーター
`ppUpdate`\
入出力このプログラムを更新するために使用できる内部インターフェイスを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

> [!NOTE]
> カスタムデバッグエンジンは常にを返す必要があり `E_NOTIMPL` ます。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
