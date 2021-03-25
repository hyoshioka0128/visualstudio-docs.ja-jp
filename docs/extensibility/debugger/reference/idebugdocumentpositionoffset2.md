---
description: ソースファイル内の文字オフセットとしての位置を表します。
title: IDebugDocumentPositionOffset2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentPositionOffset2 interface
ms.assetid: f1b05db3-50d8-453f-a72f-e68b239236a4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 01815a7dcae5a469db20b9288918b4e2aaf9ffed
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066322"
---
# <a name="idebugdocumentpositionoffset2"></a>IDebugDocumentPositionOffset2
ソースファイル内の文字オフセットとしての位置を表します。

## <a name="syntax"></a>Syntax

```
IDebugDocumentPositionOffset2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 IDE によって実装され、デバッグエンジンによって使用されます。

## <a name="methods"></a>メソッド
 次の表に、のメソッドを示し `IDebugDocumentPositionOffset2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetRange](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2-getrange.md)|現在のドキュメントの位置の範囲を取得します。|

## <a name="remarks"></a>注釈
 これは、 [GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md) と同じ情報を返し `char` ますが、ドキュメントの先頭からのオフセットで返されます。 これにより、通常返される行と列の情報ではなく、ディスク上に存在するようなドキュメント、つまり1次元の文字配列が示されます。

## <a name="requirements"></a>要件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
