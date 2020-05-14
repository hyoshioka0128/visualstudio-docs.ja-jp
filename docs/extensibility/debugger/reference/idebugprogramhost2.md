---
title: プログラムホスト2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramHost2
helpviewer_keywords:
- IDebugProgramHost2 interface
ms.assetid: 2c37b3aa-97a9-4665-8709-edd917f18cb1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 64db456e0c438f8665f122c3cd1b079c2ad1cea1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722210"
---
# <a name="idebugprogramhost2"></a>IDebugProgramHost2
このインターフェースは、プログラムに関するホスト (プロセス) 情報を提供します。

## <a name="syntax"></a>構文

```
IDebugProgramHost2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジンは、ホスト プロセスに関する情報を提供する[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)インターフェイスと同じオブジェクトにこのインターフェイスを実装します。 これはオプションのインターフェイスです。

## <a name="notes-for-callers"></a>発信者向けのメモ
 この[QueryInterface](/cpp/atl/queryinterface)インターフェイスを取得するには`IDebugProgram2`、インターフェイスでクエリ インターフェイスを呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugProgramHost2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetHostName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostname.md)|このプログラムのホスト プロセスのタイトル、フレンドリ名、またはファイル名を取得します。|
|[GetHostId](../../../extensibility/debugger/reference/idebugprogramhost2-gethostid.md)|このプログラムのホスト プロセスのプロセス識別子を取得します。|
|[GetHostMachineName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostmachinename.md)|このプログラムのホスト プロセスが実行されているコンピューターの名前を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
