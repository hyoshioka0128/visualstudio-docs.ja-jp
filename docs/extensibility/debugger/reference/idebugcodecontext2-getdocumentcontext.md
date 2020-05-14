---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCodeContext2::GetDocumentContext
helpviewer_keywords:
- IDebugCodeContext2::GetDocumentContext
ms.assetid: d552cc92-963f-43c1-949f-ae6b63a427b8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 46510ce794ea30fdd365a77007b962a1eafd5d31
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734349"
---
# <a name="idebugcodecontext2getdocumentcontext"></a>IDebugCodeContext2::GetDocumentContext
このコード コンテキストに対応するドキュメント コンテキストを取得します。 ドキュメント コンテキストは、この命令を生成したソース コードに対応するソース ファイル内の位置を表します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetDocumentContext( 
   IDebugDocumentContext2** ppSrcCxt
);
```

```csharp
int GetDocumentContext( 
   out IDebugDocumentContext2 ppSrcCxt
);
```

## <a name="parameters"></a>パラメーター
`ppSrcCxt`\
[アウト]コード コンテキストに対応する[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)オブジェクトを返します。 返`S_OK`された場合は、ths は非`null`- である必要があります。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 デバッグ エンジンは、`E_FAIL``out`コード コンテキストにソースの位置が関連`null`付けられていない場合など、パラメーターが存在する場合など、エラー コードを返す必要があります。

## <a name="remarks"></a>Remarks
 一般に、ドキュメント コンテキストはソース ファイル内の位置と見なすことができますが、コード コンテキストは実行ストリーム内のコード命令の位置です。

## <a name="see-also"></a>関連項目
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
