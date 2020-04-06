---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugProcesses2
helpviewer_keywords:
- IEnumDebugProcesses2
ms.assetid: 06a1368f-10f0-44eb-af61-e388c2327111
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8b9fe0e96ade081e8da11b5e1c06c5b45279b10b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715756"
---
# <a name="ienumdebugprocesses2"></a>IEnumDebugProcesses2
このインターフェイスは、デバッグ ポートで実行されているプロセスを列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugProcesses : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 カスタム ポート サプライヤーは、ポートで実行されているプロセスの一覧を提供するために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスを取得するために[列挙プロセス](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md)を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IEnumDebugProcesses2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugprocesses2-next.md)|列挙シーケンス内の指定した数のプロセスを取得します。|
|[スキップ](../../../extensibility/debugger/reference/ienumdebugprocesses2-skip.md)|列挙シーケンス内の指定した数のプロセスをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugprocesses2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugprocesses2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugprocesses2-getcount.md)|列挙子のプロセスの数を取得します。|

## <a name="remarks"></a>Remarks
 Visual Studio では、このインターフェイスを使用して **[プロセス]ウィンドウにデータを**設定します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumProcesses](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md)
