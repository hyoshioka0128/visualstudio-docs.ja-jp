---
title: IEnumDebugPorts2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPorts2
helpviewer_keywords:
- IEnumDebugPorts2
ms.assetid: 1754eef3-cf62-42e0-b218-1911acba77d4
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 638b17490ba875f8ecab7bf6dcdff7fef161b66e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99967801"
---
# <a name="ienumdebugports2"></a>IEnumDebugPorts2
このインターフェイスは、コンピューターまたはポートの供給元のポートを列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugPorts2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 カスタムポートサプライヤーは、このインターフェイスを実装して、サプライヤーによって作成されたポートの一覧を表します。 Visual Studio は、独自のポート供給業者をサポートするためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [Enumports](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)を呼び出して、ポートサプライヤーによって作成されたポートの一覧を表すこのインターフェイスを取得します。 [EnumPersistedPorts](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md)を呼び出して、ディスクに保存されたポートの一覧を表すこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IEnumDebugPorts2` ます。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugports2-next.md)|列挙シーケンス内の指定された数のポートを取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugports2-skip.md)|列挙シーケンス内の指定された数のポートをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugports2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugports2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugports2-getcount.md)|列挙子内のポートの数を取得します。|

## <a name="remarks"></a>解説
 Visual Studio は、このインターフェイスを使用して、プロセスへのアタッチに使用されるポートの一覧を作成します。

 通常、デバッグエンジンはこのインターフェイスを使用しません。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPorts](../../../extensibility/debugger/reference/idebugcoreserver2-enumports.md)
- [EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)
