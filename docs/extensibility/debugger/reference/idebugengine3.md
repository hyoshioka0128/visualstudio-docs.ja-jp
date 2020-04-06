---
title: Iデバッグエンジン3 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3
helpviewer_keywords:
- IDebugEngine3 interface
ms.assetid: 8bdf4bb7-3b5d-4991-8981-772d4f6bb656
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7026156eac7f60e7435e32244c3cc03ae5f08e1e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730655"
---
# <a name="idebugengine3"></a>IDebugEngine3
1 つ以上のモジュールのデバッグを制御する単一のデバッグ エンジン (DE) を表します。

## <a name="syntax"></a>構文

```
IDebugEngine3 : IDebugEngine2
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 このインターフェイスは、カスタム DE によって実装されます (シンボルをサポートしている場合) は、JustMyCode 状態を有効にします。 このインターフェイスは、シンボルと JustMyCode をサポートする場合、DE によって実装する必要があります。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスは、シンボルを読み込む場所のユーザー オプションを渡すために、セッション デバッグ マネージャー (SDM) によって呼び出されます。 また、エンジンがインスタンス化されるときに、エンジンの GUID を設定するために呼び出されます (この GUID は、エンジン登録時のメトリックに基づいています)。 SDM は、このインターフェイスを呼び出して、JustMyCode 状態を設定し、デバッガーによって認識されるすべての例外を指定した状態に設定します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)から継承されたメソッドに加えて、`IDebugEngine3`インターフェイスは、次のメソッドを公開します。

|Method|説明|
|------------|-----------------|
|[SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)|デがデバッグ シンボルを検索するために使用するパスを設定します。|
|[LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)|シンボルがまだロードされていないすべてのモジュールのシンボルをロードします。|
|[SetJustMyCodeState](../../../extensibility/debugger/reference/idebugengine3-setjustmycodestate.md)|JustMyCode 情報について DE に通知します。|
|[SetEngineGuid](../../../extensibility/debugger/reference/idebugengine3-setengineguid.md)|メトリックから DE GUID を設定します。|
|[SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)|現在未処理のすべての例外を指定の状態に設定します。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
