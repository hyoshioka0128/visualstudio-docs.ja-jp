---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPorts2
helpviewer_keywords:
- IEnumDebugPorts2
ms.assetid: 1754eef3-cf62-42e0-b218-1911acba77d4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f3cc46ef8abb6ef1fbb8f072d97b0fc4a537af1a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716106"
---
# <a name="ienumdebugports2"></a>IEnumDebugPorts2
このインターフェイスは、マシンまたはポートサプライヤーのポートを列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugPorts2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 カスタム ポート サプライヤーは、このインターフェイスを実装して、サプライヤによって作成されたポートの一覧を表します。 Visual Studio は、独自のポートサプライヤーをサポートするために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)を呼び出して、ポート サプライヤーによって作成されたポートの一覧を表すこのインターフェイスを取得します。 呼び出し[EnumPersistedPort](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md)ディスクに保存されたポートの一覧を表すこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IEnumDebugPorts2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugports2-next.md)|列挙体シーケンス内の指定した数のポートを取得します。|
|[スキップ](../../../extensibility/debugger/reference/ienumdebugports2-skip.md)|列挙体シーケンス内の指定した数のポートをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugports2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugports2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugports2-getcount.md)|列挙子のポート数を取得します。|

## <a name="remarks"></a>Remarks
 Visual Studio では、このインターフェイスを使用して、プロセスへのアタッチに使用するポートの一覧を作成します。

 通常、デバッグ エンジンはこのインターフェイスを使用しません。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPorts](../../../extensibility/debugger/reference/idebugcoreserver2-enumports.md)
- [EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)
