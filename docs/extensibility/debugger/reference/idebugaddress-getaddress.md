---
title: Iデバッグアドレス::ゲットアドレス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress::GetAddress
helpviewer_keywords:
- IDebugAddress:GetAddress method
ms.assetid: 2590387b-5d36-4116-9a75-737957b8898e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 162a64c9118bdcde23208082350005e607a237b8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736608"
---
# <a name="idebugaddressgetaddress"></a>IDebugAddress::GetAddress
オブジェクトとそのスコープまたはコンテナー内の位置を記述する構造体を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAddress (
   DEBUG_ADDRESS * pAddress
);
```

```csharp
int GetAddress(
   DEBUG_ADDRESS[] pAddress
);
```

## <a name="parameters"></a>パラメーター
`pAddress`\
[イン、アウト]このメソッドによって入力される[DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)構造体。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)構造体がこのメソッドに渡され、適切な情報が入力されます。 この情報がどのように解釈されるかは、返される情報の種類とシンボル ハンドラ自体によって異なります。 詳細については[DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)を参照してください。

## <a name="see-also"></a>関連項目
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
