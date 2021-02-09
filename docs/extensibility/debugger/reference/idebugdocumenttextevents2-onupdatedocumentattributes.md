---
title: 'IDebugDocumentTextEvents2:: onUpdateDocumentAttributes |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentTextEvents2::OnUpdateDocumentAttributes
helpviewer_keywords:
- IDebugDocumentTextEvents2::onUpdateDocumentAttributes
ms.assetid: 31b7d151-9ce2-438e-b405-f8cc46b9f537
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3e73b4c071f28abf80e9d35da05b0b49c96af265
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99919970"
---
# <a name="idebugdocumenttextevents2onupdatedocumentattributes"></a>IDebugDocumentTextEvents2::onUpdateDocumentAttributes
ドキュメント属性が更新されたことをイベントの受信者に通知します。

## <a name="syntax"></a>構文

```cpp
HRESULT onUpdateDocumentAttributes( 
   TEXT_DOC_ATTR_2 textdocattr
);
```

```csharp
int onUpdateDocumentAttributes( 
   enum_TEXT_DOC_ATTR_2 textdocattr
);
```

## <a name="parameters"></a>パラメーター
`textdocattr`\
からドキュメントの更新された属性を指定する、 [TEXT_DOC_ATTR_2](../../../extensibility/debugger/reference/text-doc-attr-2.md) 列挙のフラグの組み合わせ。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)
- [TEXT_DOC_ATTR_2](../../../extensibility/debugger/reference/text-doc-attr-2.md)
