---
description: ソースファイル内の文字オフセットとしての位置を表します。
title: IDebugDocumentPositionOffset2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentPositionOffset2 interface
ms.assetid: f1b05db3-50d8-453f-a72f-e68b239236a4
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1dee28d7f19f6398863476afbab8eb9b3cdbbb60
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167322"
---
# <a name="idebugdocumentpositionoffset2"></a>IDebugDocumentPositionOffset2
ソースファイル内の文字オフセットとしての位置を表します。

## <a name="syntax"></a>構文

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

## <a name="remarks"></a>解説
 これは、 [GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md) と同じ情報を返し `char` ますが、ドキュメントの先頭からのオフセットで返されます。 これにより、通常返される行と列の情報ではなく、ディスク上に存在するようなドキュメント、つまり1次元の文字配列が示されます。

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
