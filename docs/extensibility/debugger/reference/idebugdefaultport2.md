---
description: このインターフェイスには、ポートのサーバーと通知機能にアクセスするためのメソッドがいくつか用意されています。
title: IDebugDefaultPort2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2
helpviewer_keywords:
- IDebugDefaultPort2 interface
ms.assetid: 7b3452af-9a96-4c4c-9946-4339b72d3d7b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 03eb9f8c1bae74f15d295a72b27821d41b8282a1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067115"
---
# <a name="idebugdefaultport2"></a>IDebugDefaultPort2
このインターフェイスには、ポートのサーバーと通知機能にアクセスするためのメソッドがいくつか用意されています。

## <a name="syntax"></a>Syntax

```
IDebugDefaultPort2 : IDebugPort2
```

## <a name="notes-for-implementers"></a>実装側の注意
 Visual Studio は、プログラムにアクセスするためのデバッグポートを表すために、このインターフェイスを実装します。 カスタムポート供給業者は、リモートデバッグを処理する場合にこのインターフェイスを実装することもできます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)インターフェイスのメソッドの引数によって、このインターフェイスが提供されます。 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)インターフェイスで[QueryInterface](/cpp/atl/queryinterface)を呼び出すと、このインターフェイスを取得することもできます。

## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド
 このインターフェイスは、 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)で定義されているメソッドに加えて、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[GetPortNotify](../../../extensibility/debugger/reference/idebugdefaultport2-getportnotify.md)|このポートからポート通知インターフェイスを取得します。|
|[GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)|このポートをホストしているサーバーへのインターフェイスを取得します。|
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugdefaultport2-queryislocal.md)|このポートがローカルコンピューター上で実行されているかどうかを判断します。|

## <a name="remarks"></a>注釈
 名前 " `IDebugDefaultPort2` " は、既定のポートを表すものではないため、名称の1つです。 "IDebugPort3" という名前を指定することもできます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
