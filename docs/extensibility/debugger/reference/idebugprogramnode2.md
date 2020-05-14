---
title: プログラムノード2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2
helpviewer_keywords:
- IDebugProgramNode2 interface
ms.assetid: 80e511d8-9b40-4a85-aa5d-952fa5ee6ae7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2e6eac7c97b9d375f32e36a372d6f31175c79098
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721915"
---
# <a name="idebugprogramnode2"></a>IDebugProgramNode2
このインターフェイスは、デバッグできるプログラムを表します。

## <a name="syntax"></a>構文

```
IDebugProgramNode2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) またはカスタム ポート サプライヤーは、デバッグできるプログラムを表すために、このインターフェイスを実装します。 このインターフェイスは、通常[、IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)インターフェイスを実装する同じオブジェクトに実装されます。 このインターフェイスは、呼[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]び出すことによって登録[されます](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスを返すために[呼](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)び出します。 カスタム ポート サプライヤーは[、AddProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)への呼び出しを通じてこのインターフェイスを受け取ります。 DE は[、Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)への呼び出しを通じてこのインターフェイスを受け取ります。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugProgramNode2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetProgramName](../../../extensibility/debugger/reference/idebugprogramnode2-getprogramname.md)|プログラムの名前を取得します。|
|[GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)|プログラムをホストしているプロセスの名前を取得します。|
|[GetHostPid](../../../extensibility/debugger/reference/idebugprogramnode2-gethostpid.md)|プログラムをホストしているプロセスのシステム プロセス識別子を取得します。|
|[GetHostMachineName_V7](../../../extensibility/debugger/reference/idebugprogramnode2-gethostmachinename-v7.md)|廃止。 使用しないでください。|
|[Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)|廃止。 使用しないでください。 別の方法については[、IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)インターフェイスを参照してください。|
|[GetEngineInfo](../../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)|このプログラムを実行している DE の名前と識別子を取得します。|
|[DetachDebugger_V7](../../../extensibility/debugger/reference/idebugprogramnode2-detachdebugger-v7.md)|廃止。 使用しないでください。|

## <a name="remarks"></a>Remarks
 セッション デバッグ マネージャー (SDM) は、通常、このインターフェイスを取得するために[GetProvider プログラム ノード](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)を呼び出します。

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [AddProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
- [RemoveProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)
- [PublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)
