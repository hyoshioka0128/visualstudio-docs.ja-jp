---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugModules2
helpviewer_keywords:
- IEnumDebugModules2
ms.assetid: 4fe28074-a960-41ad-b74d-b57f04c0c0ad
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 612285aa4d5a249c0f922ccae88d98a7df83187b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716446"
---
# <a name="ienumdebugmodules2"></a>IEnumDebugModules2
このインターフェイスは、モジュールの一覧を列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugModules2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、プログラムに読み込まれたモジュールの一覧を表すこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスを取得するために[列挙モジュール](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IEnumDebugModules2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugmodules2-next.md)|列挙体シーケンス内の指定した数のモジュールを取得します。|
|[スキップ](../../../extensibility/debugger/reference/ienumdebugmodules2-skip.md)|列挙シーケンス内の指定した数のモジュールをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugmodules2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugmodules2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugmodules2-getcount.md)|モジュールの数を取得します。|

## <a name="remarks"></a>Remarks
 Visual Studio では、主に**モジュール**ウィンドウを更新するために、このインターフェイスを使用します。

 Visual Studio でデバッグを行う目的で、プログラムはモジュールの境界を越えるコード命令の論理的なシーケンスであるため、単一の[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)インターフェイスのモジュールの一覧が必要になります。 一覧の最初のモジュールには、通常、関連付けられたプログラムの初期エントリ ポイントが含まれています。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)
