---
title: ドキュメントの位置2::IsPositionInDocument |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentPosition2::IsPositionInDocument
helpviewer_keywords:
- IDebugDocumentPosition2::IsPositionInDocument
ms.assetid: d5cf57cb-b93b-4e1d-bec9-185f4fe8668d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4d92dddda8fd9831f5d66b602cd48fdbbc3dbcf1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731659"
---
# <a name="idebugdocumentposition2ispositionindocument"></a>IDebugDocumentPosition2::IsPositionInDocument
ドキュメントの位置が指定されたドキュメントに含まれているかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT IsPositionInDocument( 
   IDebugDocument2* pDoc
);
```

```csharp
int IsPositionInDocument( 
   IDebugDocument2 pDoc
);
```

## <a name="parameters"></a>パラメーター
`pDoc`\
[in]含まれているドキュメント候補を表す[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、主に[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)インターフェイスでブレークポイントを設定するときに使用されます。 ドキュメントが読み込まれると、ブレークポイントの位置が呼び出され、ドキュメントにこの位置が含まれているかどうかを判断します。

## <a name="see-also"></a>関連項目
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
