---
title: Iデバッグポート2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPort2
helpviewer_keywords:
- IDebugPort2 interface
ms.assetid: 8fd87f05-a950-4d14-b925-98be29d4facc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 62912be9fdfecc98a264a58c9713cc12ccaf28f2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725230"
---
# <a name="idebugport2"></a>IDebugPort2
このインターフェイスは、コンピューター上のデバッグ ポートを表します。

## <a name="syntax"></a>構文

```
IDebugPort2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 カスタム ポート サプライヤーは、コンピューター上のデバッグ ポートを表すために、このインターフェイスを実装します。

 ポートがポート イベントの送信をサポートしている場合は<xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer>[、IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)インターフェイスを提供するインターフェイスを<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint>サポートするインターフェイスも実装する必要があります。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [GetPort](../../../extensibility/debugger/reference/idebugportsupplier2-getport.md)または[AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)への呼び出しは、要求されたポートを表すこのインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugPort2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetPortName](../../../extensibility/debugger/reference/idebugport2-getportname.md)|ポート名を返します。|
|[GetPortId](../../../extensibility/debugger/reference/idebugport2-getportid.md)|ポート識別子を返します。|
|[GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)|ポートの作成に使用された要求を返します (使用可能な場合)。|
|[GetPortSupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md)|このポートのポート サプライヤーを返します。|
|[プロセスを取得します。](../../../extensibility/debugger/reference/idebugport2-getprocess.md)|プロセスの識別子を指定して、プロセスへのインターフェイスを返します。|
|[EnumProcesses](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md)|ポートで実行されているすべてのプロセスを列挙します。|

## <a name="remarks"></a>Remarks
 ローカル ポートは、ローカル マシンで実行されているすべてのプロセスとプログラムにアクセスできます。 他のポートは、Windows CE ベースのデバイスへのシリアル ケーブル接続、または DCOM 以外のコンピューターへのネットワーク接続を表している場合があります。 インターフェイス`IDebugPort2`は、ポートの名前と識別子を検索し、ポートで実行されているすべてのプロセスを列挙するために使用されます。 ポート上でプロセスを起動および終了するための機能は、インターフェイスに`IDebugPortEx2`実装されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
