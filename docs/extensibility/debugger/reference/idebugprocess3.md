---
description: このインターフェイスは、実行中のプロセスとそのプログラムを表します。
title: IDebugProcess3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3
helpviewer_keywords:
- IDebugProcess3 interface
ms.assetid: 7bd6b952-cf34-4e66-b8f6-d472dac3748f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a2303dfef18a1abccc728d80def0de25b4e7eadd
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169185"
---
# <a name="idebugprocess3"></a>IDebugProcess3
このインターフェイスは、実行中のプロセスとそのプログラムを表します。 このインターフェイスは、 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスのいくつかのメソッドに代わるものとして存在します。 プロセス内のすべてのプログラムを制御できます。

> [!NOTE]
> [Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md)、 [Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md)、および [Step](../../../extensibility/debugger/reference/idebugprogram2-step.md) メソッドは非推奨とされ、使用できなくなりました。 代わりに、インターフェイスに対応するメソッドを使用 `IDebugProcess3` してください。

## <a name="syntax"></a>構文

```
IDebugProcess3 : IDebugProcess2
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、プログラムをグループとして管理するためにカスタムポート供給業者によって実装されます。 プログラムがグループとして管理されている場合は、実行を制御し、式エバリュエーターの言語を設定できます。 このインターフェイスは、ポートサプライヤーによって実装される必要があります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、このプロセスで識別されるプログラムのグループと対話するために、主にセッションデバッグマネージャー (SDM) によって呼び出されます。

 このインターフェイスを取得するには、 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)インターフェイスで[QueryInterface](/cpp/atl/queryinterface)を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)から継承されたメソッドに加えて、は `IDebugProcess3` 次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md)|プロセスの実行またはステップ実行を続行します。|
|[実行](../../../extensibility/debugger/reference/idebugprocess3-execute.md)|プロセスの実行を開始します。|
|[Step](../../../extensibility/debugger/reference/idebugprocess3-step.md)|手順をステップ実行します。|
|[GetDebugReason](../../../extensibility/debugger/reference/idebugprocess3-getdebugreason.md)|プロセスがデバッグのために起動された理由を取得します。|
|[SetHostingProcessLanguage](../../../extensibility/debugger/reference/idebugprocess3-sethostingprocesslanguage.md)|デバッグエンジンが適切な式エバリュエーターを読み込むことができるように、ホスティング言語を設定します。|
|[GetHostingProcessLanguage](../../../extensibility/debugger/reference/idebugprocess3-gethostingprocesslanguage.md)|このプロセスに対して現在設定されている言語を取得します。|
|[DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)|このプロセスのエディットコンティニュ (ENC) を無効にします。<br /><br /> カスタムポート供給業者がこのメソッドを実装していません (常にを返す必要があり `E_NOTIMPL` ます)。|
|[GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md)|このプロセスの ENC 状態を取得します。<br /><br /> カスタムポート供給業者がこのメソッドを実装していません (常にを返す必要があり `E_NOTIMPL` ます)。|
|[GetEngineFilter](../../../extensibility/debugger/reference/idebugprocess3-getenginefilter.md)|使用可能なデバッグエンジンの一意の識別子の配列を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
