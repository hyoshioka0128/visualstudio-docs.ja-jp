---
title: プログラムノードアタッチ2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNodeAttach2
helpviewer_keywords:
- IDebugProgramNodeAttach2 interface
ms.assetid: 46b37ac9-a026-4ad3-997b-f19e2f8deb73
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d527dfcfcd09e4d70adca86436aa56e1852bee70
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721823"
---
# <a name="idebugprogramnodeattach2"></a>IDebugProgramNodeAttach2
関連付けられたプログラムへの接続試行をプログラム ノードに通知できるようにします。

## <a name="syntax"></a>構文

```
IDebugProgramNodeAttach2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 このインターフェイスは、アタッチ操作の通知を受信し、アタッチ操作をキャンセルする機会を提供するために[、IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)インターフェイスを実装する同じクラスに実装されます。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスを取得するには、`QueryInterface`メソッドを呼び出すことによって[、 IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)オブジェクトです。 プログラム ノードにアタッチ プロセスを停止する機会を与えるために[、OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)メソッドを呼び出す必要があります、 [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)メソッドです。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)|関連付けられたプログラムにアタッチするか[、Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)メソッドへのアタッチ プロセスを延期します。|

## <a name="remarks"></a>Remarks
 このインターフェイスは、非推奨の[Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)メソッドの代わりに推奨されます。 すべてのデバッグ エンジンは常に`CoCreateInstance`関数で読み込まれます。つまり、デバッグ中のプログラムのアドレス空間の外部でインスタンス化されます。

 `IDebugProgramNode2::Attach_V7`メソッドの以前の実装がデバッグ中のプログラムの`GUID`を設定しただけである場合[、OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)メソッドのみを実装する必要があります。

 メソッドの以前の実装が提供されたコールバック インターフェイスを使用していた場合、その機能を Attach メソッドの実装に移動する必要があり、`IDebugProgramNodeAttach2`インターフェイスを実装する必要はありません。 [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) `IDebugProgramNode2::Attach_V7`

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
