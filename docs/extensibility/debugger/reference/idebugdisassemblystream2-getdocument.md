---
title: 'IDebugDisassemblyStream2:: GetDocument |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::GetDocument
helpviewer_keywords:
- IDebugDisassemblyStream2::GetDocument
ms.assetid: 3d039a44-ebaa-4413-ac18-7cfd92c408bd
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6ad0b4d4fcb316447ca836fbc5ac15170a71270e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99901767"
---
# <a name="idebugdisassemblystream2getdocument"></a>IDebugDisassemblyStream2::GetDocument
この入力ストリームに関連付けられているソースドキュメントを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetDocument( 
   BSTR              bstrDocumentUrl,
   IDebugDocument2** ppDocument
);
```

```csharp
int GetDocument( 
   string              bstrDocumentUrl,
   out IDebugDocument2 ppDocument
);
```

## <a name="parameters"></a>パラメーター
`bstrDocumentUrl`\
からドキュメントの URL。

`ppDocument`\
入出力ドキュメントを表す [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは、実際のファイルに格納されていないテキストドキュメントを含むデバッグエンジンによって実装されます。

## <a name="see-also"></a>関連項目
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
