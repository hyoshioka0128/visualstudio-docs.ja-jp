---
title: IDebugDocumentChecksum2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentChecksum2 interface
ms.assetid: 6d22fa94-21aa-46cb-b5b5-32a6399ebb20
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 03cfb29cc54a2f0ab18bce3ec0761cfab62e20df
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80731903"
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

|Method|説明|
|------------|-----------------|
|[GetChecksumAndAlgorithmId](../../../extensibility/debugger/reference/idebugdocumentchecksum2-getchecksumandalgorithmid.md)|使用する最大バイト数を指定して、ドキュメントのチェックサムとアルゴリズム識別子を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
