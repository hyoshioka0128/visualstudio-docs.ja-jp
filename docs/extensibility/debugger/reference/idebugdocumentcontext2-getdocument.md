---
description: このドキュメントコンテキストを含むドキュメントを取得します。
title: 'IDebugDocumentContext2:: GetDocument |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::GetDocument
helpviewer_keywords:
- IDebugDocumentContext2::GetDocument
ms.assetid: c6d46c5d-ade8-4dc8-9862-8fc7876658c4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c554f43b596d9114153c3806340434e12206a80a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066660"
---
# <a name="idebugdocumentcontext2getdocument"></a>IDebugDocumentContext2::GetDocument
このドキュメントコンテキストを含むドキュメントを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetDocument( 
   IDebugDocument2** ppDocument
);
```

```csharp
int GetDocument( 
   out IDebugDocument2 ppDocument
);
```

## <a name="parameters"></a>パラメーター
`ppDocument`\
入出力このドキュメントコンテキストを含むドキュメントを表す [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドは、IDE に直接ドキュメントを提供するデバッグエンジンを対象としています。 それ以外の場合、このメソッドはを返し `E_NOTIMPL` ます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
