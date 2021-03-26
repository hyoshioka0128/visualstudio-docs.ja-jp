---
description: 関連付けられているプログラムにアタッチしようとしたことをプログラムノードに通知します。
title: IDebugProgramNodeAttach2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNodeAttach2
helpviewer_keywords:
- IDebugProgramNodeAttach2 interface
ms.assetid: 46b37ac9-a026-4ad3-997b-f19e2f8deb73
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1a1de6c7480e1ce4dcc0723614741a05dcc961a6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071468"
---
# <a name="idebugprogramnodeattach2"></a>IDebugProgramNodeAttach2
関連付けられているプログラムにアタッチしようとしたことをプログラムノードに通知します。

## <a name="syntax"></a>Syntax

```
IDebugProgramNodeAttach2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、アタッチ操作の通知を受信し、アタッチ操作をキャンセルする機会を提供するために、 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) インターフェイスを実装する同じクラスに実装されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスを取得するには、 `QueryInterface` [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクトのメソッドを呼び出します。 アタッチプロセスを停止する機会をプログラムノードに付与するには、 [attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)メソッドの前に[onattach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)メソッドを呼び出す必要があります。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスは、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)|関連付けられているプログラムにアタッチするか、アタッチプロセスを [attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドに従います。|

## <a name="remarks"></a>注釈
 このインターフェイスは、非推奨の [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md) 方法の代わりに使用することをお勧めします。 すべてのデバッグエンジンは、常に関数と共に読み込まれ `CoCreateInstance` ます。つまり、デバッグ対象のプログラムのアドレス空間の外部でインスタンス化されます。

 メソッドの以前の実装が、単にデバッグ対象のプログラムのを設定している場合は、 `IDebugProgramNode2::Attach_V7` `GUID` [onattach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) メソッドのみを実装する必要があります。

 メソッドの以前の実装で `IDebugProgramNode2::Attach_V7` 、指定されたコールバックインターフェイスが使用されていた場合、その機能を [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドの実装に移動し、インターフェイスを実装する必要はあり `IDebugProgramNodeAttach2` ません。

## <a name="requirements"></a>要件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
