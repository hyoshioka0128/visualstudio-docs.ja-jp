---
title: をクリックして既定のポート 2 を実行します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2
helpviewer_keywords:
- IDebugDefaultPort2 interface
ms.assetid: 7b3452af-9a96-4c4c-9946-4339b72d3d7b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f560a3dabefb0a8dede6520dcd8fd47f609a7780
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732314"
---
# <a name="idebugdefaultport2"></a>IDebugDefaultPort2
このインターフェイスは、ポートのサーバーおよび通知機能にアクセスするためのいくつかのメソッドを提供します。

## <a name="syntax"></a>構文

```
IDebugDefaultPort2 : IDebugPort2
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 Visual Studio では、プログラムにアクセスするためのデバッグ ポートを表すために、このインターフェイスを実装します。 カスタム ポート サプライヤーは、リモート デバッグを処理する場合にもこのインターフェイスを実装できます。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [インターフェイス](../../../extensibility/debugger/reference/idebugprogramprovider2.md)上のメソッドへの引数は、このインターフェイスを提供します。 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)インターフェイスで[クエリ インターフェイス](/cpp/atl/queryinterface)を呼び出す場合も、このインターフェイスを取得できます。

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)で定義されているメソッドに加えて、このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetPortNotify](../../../extensibility/debugger/reference/idebugdefaultport2-getportnotify.md)|このポートからポート通知インターフェイスを取得します。|
|[GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)|このポートをホストしているサーバーへのインターフェイスを取得します。|
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugdefaultport2-queryislocal.md)|このポートがローカル マシンで実行されているかどうかを判断します。|

## <a name="remarks"></a>Remarks
 名前 "`IDebugDefaultPort2`" は、既定のポートを表さないため、少し誤解を与えます。 それは「IDebugPort3」と呼ばれる可能性があります。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
