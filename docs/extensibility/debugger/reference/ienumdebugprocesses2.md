---
description: このインターフェイスは、デバッグポートで実行されているプロセスを列挙します。
title: IEnumDebugProcesses2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugProcesses2
helpviewer_keywords:
- IEnumDebugProcesses2
ms.assetid: 06a1368f-10f0-44eb-af61-e388c2327111
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 75778ea0f02c0e7dcca1f7d2eb0ea8ace82c9b9c
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102224383"
---
# <a name="ienumdebugprocesses2"></a>IEnumDebugProcesses2
このインターフェイスは、デバッグポートで実行されているプロセスを列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugProcesses : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 カスタムポート供給業者は、このインターフェイスを実装して、ポートで実行されているプロセスの一覧を提供します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスを取得するために、Visual Studio は [EnumProcesses](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md) を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IEnumDebugProcesses2` ます。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugprocesses2-next.md)|列挙シーケンス内の指定された数のプロセスを取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugprocesses2-skip.md)|列挙シーケンス内の指定された数のプロセスをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugprocesses2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugprocesses2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugprocesses2-getcount.md)|列挙子内のプロセスの数を取得します。|

## <a name="remarks"></a>解説
 Visual Studio では、このインターフェイスを使用して [ **プロセス** ] ウィンドウを設定します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumProcesses](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md)
