---
title: Iデバッグプロセス3 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3
helpviewer_keywords:
- IDebugProcess3 interface
ms.assetid: 7bd6b952-cf34-4e66-b8f6-d472dac3748f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b423ee2cb95ad55296c452cfdc4b891ee4cd26a0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723544"
---
# <a name="idebugprocess3"></a>IDebugProcess3
このインターフェイスは、実行中のプロセスとそのプログラムを表します。 このインターフェイスは[、IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)インターフェイスのいくつかのメソッドの代わりとして存在します。 プロセス内のすべてのプログラムを制御できます。

> [!NOTE]
> [続行](../../../extensibility/debugger/reference/idebugprogram2-continue.md)、[実行](../../../extensibility/debugger/reference/idebugprogram2-execute.md)、および[ステップ](../../../extensibility/debugger/reference/idebugprogram2-step.md)の各メソッドは非推奨となり、使用しないでください。 代わりに、インターフェイスで対応`IDebugProcess3`するメソッドを使用します。

## <a name="syntax"></a>構文

```
IDebugProcess3 : IDebugProcess2
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 このインターフェイスは、グループとしてプログラムを管理するカスタム ポート サプライヤーによって実装されます。 プログラムがグループとして管理されている場合、その実行を制御し、式エバリュエーターの言語を確立できます。 このインターフェイスは、ポート サプライヤーによって実装されている必要があります。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスは、このプロセスで識別されたプログラムのグループと対話するために、主にセッション デバッグ マネージャー (SDM) によって呼び出されます。

 この[インターフェイス](/cpp/atl/queryinterface)を取得するには[、IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)インターフェイスでクエリ インターフェイスを呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)から継承されたメソッドに加えて`IDebugProcess3`、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[続行](../../../extensibility/debugger/reference/idebugprocess3-continue.md)|プロセスの実行を継続するか、プロセスをステップ実行します。|
|[実行](../../../extensibility/debugger/reference/idebugprocess3-execute.md)|プロセスの実行を開始します。|
|[Step](../../../extensibility/debugger/reference/idebugprocess3-step.md)|プロセス内の 1 つの命令またはステートメントを進めます。|
|[GetDebugReason](../../../extensibility/debugger/reference/idebugprocess3-getdebugreason.md)|デバッグ用にプロセスが起動された理由を取得します。|
|[SetHostingProcessLanguage](../../../extensibility/debugger/reference/idebugprocess3-sethostingprocesslanguage.md)|デバッグ エンジンが適切な式エバリュエーターを読み込むことができるように、ホスティング言語を設定します。|
|[GetHostingProcessLanguage](../../../extensibility/debugger/reference/idebugprocess3-gethostingprocesslanguage.md)|このプロセスに現在設定されている言語を取得します。|
|[DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)|このプロセスのエディット コンティニュ (ENC) を無効にします。<br /><br /> カスタム ポート サプライヤーはこのメソッドを実装しません (常に`E_NOTIMPL`返す必要があります)。|
|[GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md)|このプロセスの ENC 状態を取得します。<br /><br /> カスタム ポート サプライヤーはこのメソッドを実装しません (常に`E_NOTIMPL`返す必要があります)。|
|[GetEngineFilter](../../../extensibility/debugger/reference/idebugprocess3-getenginefilter.md)|使用可能なデバッグ エンジンの一意の識別子の配列を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
