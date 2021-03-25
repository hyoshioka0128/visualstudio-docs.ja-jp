---
description: デバッグドキュメントのチェックサムを表し、コンポーネント間でチェックサムを渡すことができるようにします。
title: IDebugDocumentChecksum2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentChecksum2 interface
ms.assetid: 6d22fa94-21aa-46cb-b5b5-32a6399ebb20
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 518e5b089d0d34e2492297b27dd0829e5f00ef2f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066738"
---
# <a name="idebugdocumentchecksum2"></a>IDebugDocumentChecksum2
デバッグドキュメントのチェックサムを表し、コンポーネント間でチェックサムを渡すことができるようにします。

## <a name="syntax"></a>Syntax

```
IDebugDocumentChecksum2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) インターフェイスを公開する任意のコンポーネントによって実装できます。 ただし、これは主にデバッグエンジンによって実装されるため、シンボルファイル (* .pdb) に埋め込まれているチェックサムを IDE に渡して、ソースの検索時に使用できます。

## <a name="methods"></a>メソッド
 次の表に、のメソッドを示し `IDebugDocumentChecksum2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetChecksumAndAlgorithmId](../../../extensibility/debugger/reference/idebugdocumentchecksum2-getchecksumandalgorithmid.md)|使用する最大バイト数を指定して、ドキュメントのチェックサムとアルゴリズム識別子を取得します。|

## <a name="requirements"></a>要件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
