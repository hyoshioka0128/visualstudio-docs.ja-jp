---
title: をクリックして配置を変更します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentPositionOffset2 interface
ms.assetid: f1b05db3-50d8-453f-a72f-e68b239236a4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d967ec9cf406f7dae691c3f05eda514e0907c7e3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731604"
---
# <a name="idebugdocumentpositionoffset2"></a>IDebugDocumentPositionOffset2
ソース ファイル内の位置を文字オフセットとして表します。

## <a name="syntax"></a>構文

```
IDebugDocumentPositionOffset2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 IDE によって実装され、デバッグ エンジンによって使用されます。

## <a name="methods"></a>メソッド
 次の表に`IDebugDocumentPositionOffset2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetRange](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2-getrange.md)|現在のドキュメントの位置の範囲を取得します。|

## <a name="remarks"></a>Remarks
 これは[、GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md)と同じ情報を`char`返しますが、ドキュメントの先頭からのオフセットで返します。 これは、通常は返される行と列の情報の代わりに、ディスク上に存在するドキュメント、つまり文字の 1 次元配列を示します。

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
