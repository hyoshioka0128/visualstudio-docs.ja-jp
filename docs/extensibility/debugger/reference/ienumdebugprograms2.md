---
description: このインターフェイスは、現在のデバッグセッションで実行されているプログラムを列挙します。
title: IEnumDebugPrograms2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPrograms2
helpviewer_keywords:
- IEnumDebugPrograms2
ms.assetid: 7fbb8fb7-db64-4546-a364-dc668430c8af
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d7f9a981146d5e024333f17557f4fdbc3d35bc05
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082934"
---
# <a name="ienumdebugprograms2"></a>IEnumDebugPrograms2
このインターフェイスは、現在のデバッグセッションで実行されているプログラムを列挙します。

## <a name="syntax"></a>Syntax

```
IEnumDebugPrograms2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、このインターフェイスを実装して、DE によってデバッグされているプログラムの一覧を提供します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 Visual Studio は、このインターフェイスを取得するために [Enumprograms](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md) を呼び出します。 [Enumprograms](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md) は Visual Studio では使用されません。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IEnumDebugPrograms2` ます。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)|列挙シーケンス内の指定された数のプログラムを取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugprograms2-skip.md)|列挙シーケンス内の指定された数のプログラムをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugprograms2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugprograms2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugprograms2-getcount.md)|列挙子内のプログラムの数を取得します。|

## <a name="remarks"></a>注釈
 Visual Studio では、このインターフェイスを使用して次のことを行います。

- [ **モジュール** ] ウィンドウを設定します ( [enumprograms](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md) を呼び出して、各プログラムで [enumprograms](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md) を呼び出します)。

- [**プロセスにアタッチ**] の一覧を作成し `IDebugProcess2::EnumPrograms` ます (を呼び出し、各 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)インターフェイスで [QueryInterface](/cpp/atl/queryinterface)を呼び出して [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)インターフェイスを取得します)。

- プロセス内の各プログラムをデバッグできる DEs の一覧を生成します ( [GetEngineInfo](../../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md)を使用)。

- エディットコンティニュ (ENC) の更新プログラムを各プログラムに適用します (IDebugProcess2:: EnumPrograms を呼び出し、次に [Getencupdate](../../../extensibility/debugger/reference/idebugprogram2-getencupdate.md)を呼び出します)。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPrograms](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md)
- [EnumPrograms](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)
