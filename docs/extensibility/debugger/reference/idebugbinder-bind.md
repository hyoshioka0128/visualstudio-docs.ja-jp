---
title: バインダーのバインド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder::Bind
helpviewer_keywords:
- IDebugBinder::Bind method
ms.assetid: 15a11ad7-0fcc-4e80-ae34-8a7dd7bae3c3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7a783025c96053a89956a1c77d46b5e417938a2b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736016"
---
# <a name="idebugbinderbind"></a>IDebugBinder::Bind
このメソッドは、シンボルの現在の値を格納しているメモリ コンテキストまたはオブジェクトを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT Bind( 
   IDebugObject*  pContainer,
   IDebugField*   pField,
   IDebugObject** ppObject
);
```

```csharp
int Bind(
   IDebugObject     pContainer,
   IDebugField      pField,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>パラメーター
`pContainer`\
[in]によって`pField`参照される子を含む[IDebug オブジェクト](../../../extensibility/debugger/reference/idebugobject.md)。

`pField`\
[in]シンボルを表す[IDebugField。](../../../extensibility/debugger/reference/idebugfield.md)

`ppObject`\
[アウト]シンボルの`IDebugObject`インスタンスを表す を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
