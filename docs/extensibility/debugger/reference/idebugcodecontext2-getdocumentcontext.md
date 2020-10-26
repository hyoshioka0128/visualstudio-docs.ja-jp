---
title: 'IDebugCodeContext2:: GetDocumentContext |Microsoft Docs'
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80734349"
---
# <a name="idebugcodecontext2getdocumentcontext"></a>IDebugCodeContext2::GetDocumentContext
このコードコンテキストに対応するドキュメントコンテキストを取得します。 ドキュメントコンテキストは、この命令を生成したソースコードに対応するソースファイル内の位置を表します。

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
入出力コードコンテキストに対応する [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) オブジェクトを返します。 が返された場合 `S_OK` 、は以外である必要があり `null` ます。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 デバッグエンジンは、 `E_FAIL` `out` `null` コードコンテキストにソース位置が関連付けられていない場合など、パラメーターがの場合などのエラーコードを返す必要があります。

## <a name="remarks"></a>解説
 一般に、コードコンテキストは実行ストリーム内のコード命令の位置であるのに対し、ドキュメントコンテキストはソースファイル内の位置と考えることができます。

## <a name="see-also"></a>関連項目
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
