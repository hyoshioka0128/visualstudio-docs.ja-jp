---
description: デバッグドキュメントのチェックサムを表し、コンポーネント間でチェックサムを渡すことができるようにします。
title: IDebugDocumentChecksum2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentChecksum2 interface
ms.assetid: 6d22fa94-21aa-46cb-b5b5-32a6399ebb20
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c5b39f381817cd98fd94b1c746cbdccde31e0b1f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102165567"
---
# <a name="idebugdocumentchecksum2"></a>IDebugDocumentChecksum2
デバッグドキュメントのチェックサムを表し、コンポーネント間でチェックサムを渡すことができるようにします。

## <a name="syntax"></a>構文

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

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
