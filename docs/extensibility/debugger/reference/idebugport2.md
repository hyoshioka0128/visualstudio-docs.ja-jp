---
description: このインターフェイスは、コンピューター上のデバッグポートを表します。
title: IDebugPort2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPort2
helpviewer_keywords:
- IDebugPort2 interface
ms.assetid: 8fd87f05-a950-4d14-b925-98be29d4facc
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f78db8ba9a29b40d111dc5a82827395b100302b5
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169484"
---
# <a name="idebugport2"></a>IDebugPort2
このインターフェイスは、コンピューター上のデバッグポートを表します。

## <a name="syntax"></a>構文

```
IDebugPort2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 カスタムポート供給業者は、このインターフェイスを実装してコンピューター上のデバッグポートを表します。

 ポートで送信ポートイベントがサポートされている場合は、インターフェイスをサポートするインターフェイスも実装する必要があります。インターフェイスは、 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) インターフェイスを提供します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [Getport](../../../extensibility/debugger/reference/idebugportsupplier2-getport.md)または[addport](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)を呼び出すと、要求されたポートを表すこのインターフェイスが返されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugPort2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetPortName](../../../extensibility/debugger/reference/idebugport2-getportname.md)|ポート名を返します。|
|[GetPortId](../../../extensibility/debugger/reference/idebugport2-getportid.md)|ポート識別子を返します。|
|[GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)|ポートを作成するために使用された要求を返します (使用可能な場合)。|
|[GetPortSupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md)|このポートのポート供給元を返します。|
|[GetProcess](../../../extensibility/debugger/reference/idebugport2-getprocess.md)|プロセスの識別子を指定して、プロセスへのインターフェイスを返します。|
|[EnumProcesses](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md)|ポートで実行されているすべてのプロセスを列挙します。|

## <a name="remarks"></a>解説
 ローカルポートは、ローカルコンピューター上で実行されているすべてのプロセスとプログラムへのアクセスを提供します。 その他のポートは、Windows CE ベースのデバイスへのシリアルケーブル接続、または非 DCOM コンピューターへのネットワーク接続を表す場合があります。 インターフェイスは、ポート `IDebugPort2` の名前と識別子を検索し、ポートで実行されているすべてのプロセスを列挙するために使用されます。 ポートでプロセスを起動して終了するための機能は、インターフェイスに実装されてい `IDebugPortEx2` ます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
