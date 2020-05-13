---
title: 2::オン更新テキスト属性 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentTextEvents2::OnUpdateTextAttributes
helpviewer_keywords:
- IDebugDocumentTextEvents2::onUpdateTextAttributes
ms.assetid: eb68d69a-1ad9-4ce4-84e1-40979ef16634
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 82cda44c50319ef76efbc8fa3ae2712c3a4ae8f2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731381"
---
# <a name="idebugdocumenttextevents2onupdatetextattributes"></a>IDebugDocumentTextEvents2::onUpdateTextAttributes
ドキュメント内でテキスト属性が更新されたことをデバッグ パッケージに通知します。

## <a name="syntax"></a>構文

```cpp
HRESULT onUpdateTextAttributes( 
   TEXT_POSITION pos,
   DWORD         dwNumToUpdate
);
```

```csharp
int onUpdateTextAttributes( 
   enum_TEXT_POSITION pos,
   uint               dwNumToUpdate
);
```

## <a name="parameters"></a>パラメーター
`pos`\
[in]テキスト属性が更新された場所を示す[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)構造。

`dwNumToUpdate`\
[in]更新されたテキストの文字数を指定します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
