---
title: IDebug ドキュメント コンテキスト2::比較 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::Compare
helpviewer_keywords:
- IDebugDocumentContext2::Compare
ms.assetid: 2327b1ba-52d0-42fb-a01e-63cb4b332d2f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b0e46f765c8e4c0e12c3bb9447e0713919fae7b8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731883"
---
# <a name="idebugdocumentcontext2compare"></a>IDebugDocumentContext2::Compare
このドキュメント コンテキストを、指定されたドキュメント コンテキストの配列と比較します。

## <a name="syntax"></a>構文

```cpp
HRESULT Compare( 
   DOCCONTEXT_COMPARE       compare,
   IDebugDocumentContext2** rgpDocContextSet,
   DWORD                    dwDocContextSetLen,
   DWORD*                   pdwDocContext
);
```

```csharp
int Compare( 
   enum_ DOCCONTEXT_COMPARE compare,
   IDebugDocumentContext2[] rgpDocContextSet,
   uint                     dwDocContextSetLen,
   out uint                 pdwDocContext
);
```

## <a name="parameters"></a>パラメーター
`compare`\
[in]比較の種類を指定する[DOCCONTEXT_COMPARE](../../../extensibility/debugger/reference/doccontext-compare.md)列挙体の値。

`rgpDocContextSet`\
[in]比較されるドキュメント コンテキストを表す[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)オブジェクトの配列。

`dwDocContextSetLen`\
[in]比較するドキュメント コンテキストの配列の長さ。

`pdwDocContext`\
[アウト]比較を満たす最初`rgpDocContextSet`のドキュメント コンテキストの配列にインデックスを返します。

## <a name="return-value"></a>戻り値
 一`S_OK`致が見つかったかどうかを返します。 一`S_FALSE`致するものが見つからなかった場合に返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>Remarks
 配列で渡される[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)オブジェクトは、呼び出される`IDebugDocumentContext2`オブジェクトを実装するのと同じデバッグ エンジンによって実装する必要があります。それ以外の場合、比較は無効です。

## <a name="see-also"></a>関連項目
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [DOCCONTEXT_COMPARE](../../../extensibility/debugger/reference/doccontext-compare.md)
