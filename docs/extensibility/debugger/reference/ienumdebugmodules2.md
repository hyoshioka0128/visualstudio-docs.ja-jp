---
description: このインターフェイスは、モジュールの一覧を列挙します。
title: IEnumDebugModules2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugModules2
helpviewer_keywords:
- IEnumDebugModules2
ms.assetid: 4fe28074-a960-41ad-b74d-b57f04c0c0ad
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 33853804078d5f32aba6fda6dac409cf2a24de0a
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102224760"
---
# <a name="ienumdebugmodules2"></a>IEnumDebugModules2
このインターフェイスは、モジュールの一覧を列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugModules2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、プログラム用に読み込まれたモジュールの一覧を表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 Visual Studio は、このインターフェイスを取得するために [Enummodules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md) を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IEnumDebugModules2` ます。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugmodules2-next.md)|列挙シーケンス内の指定された数のモジュールを取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugmodules2-skip.md)|列挙シーケンス内の指定された数のモジュールをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugmodules2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugmodules2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugmodules2-getcount.md)|モジュールの数を取得します。|

## <a name="remarks"></a>解説
 Visual Studio では、主にこのインターフェイスを使用して [ **モジュール** ] ウィンドウを更新します。

 Visual Studio でのデバッグのために、プログラムはモジュールの境界を越えることができるコード命令の論理的なシーケンスです。そのため、単一の [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスのモジュールの一覧が必要になります。 リスト内の最初のモジュールには、通常、関連付けられているプログラムの最初のエントリポイントが含まれています。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)
