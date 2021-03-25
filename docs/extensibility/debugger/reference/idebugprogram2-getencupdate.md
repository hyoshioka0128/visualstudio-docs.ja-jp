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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6d6b60c8b17a8db1420222a7242164ce1c0eedd1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075927"
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

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
