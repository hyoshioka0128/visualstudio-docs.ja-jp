---
title: I列挙プログラム2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPrograms2
helpviewer_keywords:
- IEnumDebugPrograms2
ms.assetid: 7fbb8fb7-db64-4546-a364-dc668430c8af
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1717397d9ff073642c7b6bc25ad85babe76d684c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715566"
---
# <a name="ienumdebugprograms2"></a>IEnumDebugPrograms2
このインターフェイスは、現在のデバッグ セッションで実行されているプログラムを列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugPrograms2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、DE によってデバッグされているプログラムの一覧を提供するには、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスを取得するために[列挙プログラム](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)を呼び出します。 [列挙プログラム](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md)は、Visual Studio では使用されません。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IEnumDebugPrograms2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)|列挙体シーケンス内の指定した数のプログラムを取得します。|
|[スキップ](../../../extensibility/debugger/reference/ienumdebugprograms2-skip.md)|列挙体シーケンス内の指定した数のプログラムをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugprograms2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugprograms2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugprograms2-getcount.md)|列挙子のプログラムの数を取得します。|

## <a name="remarks"></a>Remarks
 Visual Studio では、このインターフェイスを使用して次の用途に使用します。

- **[モジュール**] ウィンドウに値を設定します[(EnumPrograms を](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)呼び出し、各プログラムで[EnumModule を](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)呼び出します)。

- プロセス**へのアタッチ**リストを設定します`IDebugProcess2::EnumPrograms`(呼び出し、IDebugProgram2 インターフェイスを取得する[IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)各[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)インターフェイスで[クエリ インターフェイス](/cpp/atl/queryinterface)を呼び出すことによって)。

- プロセス内の各プログラムをデバッグできる DEs のリストを生成します[(GetEngineInfo](../../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md)を使用)。

- エディット コンティニュ (ENC) の更新を各プログラムに適用します (IDebugProcess2::EnumPrograms を呼び出し[、GetENCUpdate](../../../extensibility/debugger/reference/idebugprogram2-getencupdate.md)を呼び出します)。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPrograms](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md)
- [EnumPrograms](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)
