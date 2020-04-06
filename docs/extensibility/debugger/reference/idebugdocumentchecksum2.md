---
title: 2018年10月11日マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731903"
---
# <a name="idebugdocumentchecksum2"></a>IDebugDocumentChecksum2
デバッグ ドキュメントのチェックサムを表し、コンポーネント間でチェックサムを渡すことを有効にします。

## <a name="syntax"></a>構文

```
IDebugDocumentChecksum2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 このインターフェイスは[、IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)インターフェイスを公開する任意のコンポーネントによって実装できます。 ただし、シンボル ファイル (*.pdb) に埋め込まれているチェックサムを IDE に渡し、ソースを検索するときに使用できるように、主にデバッグ エンジンによって実装されます。

## <a name="methods"></a>メソッド
 次の表に`IDebugDocumentChecksum2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetChecksumAndAlgorithmId](../../../extensibility/debugger/reference/idebugdocumentchecksum2-getchecksumandalgorithmid.md)|使用する最大バイト数を指定して、ドキュメントチェックサムとアルゴリズム識別子を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: を使用します。

 アセンブリ:
