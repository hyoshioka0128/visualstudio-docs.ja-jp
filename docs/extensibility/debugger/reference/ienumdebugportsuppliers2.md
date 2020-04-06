---
title: I列挙型ポートサプライヤー2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPortSuppliers2
helpviewer_keywords:
- IEnumDebugPortSuppliers2
ms.assetid: cd0a73dc-dd25-46fd-8c4f-5b011501afeb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: de0bfc5b387df9b347e4a58d97601a5e1e70f1a4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715938"
---
# <a name="ienumdebugportsuppliers2"></a>IEnumDebugPortSuppliers2
このインターフェイスは、ポートサプライヤーを列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugPortSuppliers2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 Visual Studio では、ポートの供給業者の一覧を表すこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 ポート[サプライヤーの](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)リストを取得するには、列挙ポートサプライヤーを呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IEnumDebugPortSuppliers2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-next.md)|列挙体シーケンス内の指定した数のポート 供給元を取得します。|
|[スキップ](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-skip.md)|列挙体シーケンス内の指定した数のポート 供給元をスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-getcount.md)|列挙子のポート サプライヤーの数を取得します。|

## <a name="remarks"></a>Remarks
 デバッグ エンジンは、通常、このインターフェイスを取得する必要はありません。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)
