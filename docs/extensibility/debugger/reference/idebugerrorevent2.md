---
description: このインターフェイスは、ユーザーに報告されるエラーメッセージを指定します。
title: IDebugErrorEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugErrorEvent2
helpviewer_keywords:
- IDebugErrorEvent2 interface
ms.assetid: 275b6f38-b3d4-4cae-8491-491177f524fb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bf249e8568c3ae70bc8d881d72b491cf7fa3576b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102153041"
---
# <a name="idebugerrorevent2"></a>IDebugErrorEvent2
このインターフェイスは、ユーザーに報告されるエラーメッセージを指定します。

## <a name="syntax"></a>構文

```
IDebugErrorEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、このインターフェイスを実装して、エラーを人間が判読できるメッセージとして報告します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は、 [QueryInterface](/cpp/atl/queryinterface) を使用してインターフェイスにアクセスし `IDebugEvent2` ます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE は、このイベントオブジェクトを作成して送信し、エラーを報告します。 イベントは、デバッグ対象のプログラムにアタッチされたときに SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド
 このインターフェイスは、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|`GetErrorMessage`|人間が判読できる文字列としてエラーを返します。|

## <a name="remarks"></a>解説
 デバッグエンジンがエラーを検出した場合、このインターフェイスを使用して、Visual Studio を通じてユーザーにメッセージを報告できます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
