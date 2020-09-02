---
title: IEnumDebugPortSuppliers2 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80715938"
---
# <a name="ienumdebugportsuppliers2"></a>IEnumDebugPortSuppliers2
このインターフェイスは、ポートサプライヤーを列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugPortSuppliers2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 Visual Studio は、このインターフェイスを実装して、ポートサプライヤーのリストを表します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [Enumportsuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)を呼び出して、ポートサプライヤーの一覧を取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IEnumDebugPortSuppliers2` ます。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-next.md)|列挙シーケンス内の指定された数のポート供給元を取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-skip.md)|列挙シーケンス内の指定された数のポートサプライヤーをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-getcount.md)|列挙子内のポートサプライヤーの数を取得します。|

## <a name="remarks"></a>注釈
 通常、デバッグエンジンでは、このインターフェイスを取得する必要はありません。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)
