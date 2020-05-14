---
title: プログラム3 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgram3 interface
ms.assetid: 4301ba23-c00c-4ce5-8b1e-3f27da312034
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9da63d54f64a4ef7592fdbc4d36e2b31220f82df
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722642"
---
# <a name="idebugprogram3"></a>IDebugProgram3
このインターフェイスは、プロセス内で実行されているプログラムを表し、スレッド情報を提供することによって[Execute を](../../../extensibility/debugger/reference/idebugprogram2-execute.md)拡張します。

## <a name="syntax"></a>構文

```
IDebugProgram3 : IDebugProgram3
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) とカスタム ポート サプライヤーは、プロセス内のプログラムを表すために、このインターフェイスを実装します。 セッション デバッグ マネージャー (SDM) も、このインターフェイスを実装して[、Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md)に情報を提供します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 イベント[は](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)、新しいプログラムのこのインターフェイスを返します。 このインターフェイスは、複数のインターフェイスで多くのメソッドのパラメーターとしても使用されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugProgram3`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[ExecuteOnThread](../../../extensibility/debugger/reference/idebugprogram3-executeonthread.md)|プログラムを実行します。 スレッドが返され、実行中にユーザーが表示しているスレッドに関する情報をデバッガーに提供します。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="remarks"></a>Remarks
 プログラムは、特定のランタイム アーキテクチャで実行されるスレッド コンテナーであり、プロセスは 1 つ以上のプログラムで構成されます。

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)
- [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
