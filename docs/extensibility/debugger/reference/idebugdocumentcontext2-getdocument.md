---
title: 'IDebugDocumentContext2:: GetDocument |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::GetDocument
helpviewer_keywords:
- IDebugDocumentContext2::GetDocument
ms.assetid: c6d46c5d-ade8-4dc8-9862-8fc7876658c4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6bb93fe3efb4bc114cf583e8e2c066c337109d12
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80731841"
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

## <a name="remarks"></a>解説
 このメソッドは、IDE に直接ドキュメントを提供するデバッグエンジンを対象としています。 それ以外の場合、このメソッドはを返し `E_NOTIMPL` ます。

## <a name="see-also"></a>関連項目
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
