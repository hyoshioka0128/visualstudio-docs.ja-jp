---
title: イベント 2 を実行する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugErrorEvent2
helpviewer_keywords:
- IDebugErrorEvent2 interface
ms.assetid: 275b6f38-b3d4-4cae-8491-491177f524fb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 00fd8b4b42f11d18958f8a969bc4ccd58754ab93
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730002"
---
# <a name="idebugerrorevent2"></a>IDebugErrorEvent2
このインターフェイスは、ユーザーに報告されるエラー メッセージを指定します。

## <a name="syntax"></a>構文

```
IDebugErrorEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、人間が読み取り可能なメッセージとしてエラーを報告するには、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は[、インターフェイス](/cpp/atl/queryinterface)にアクセスするのに`IDebugEvent2`クエリ インターフェイスを使用します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 DE は、エラーを報告するために、このイベント オブジェクトを作成して送信します。 イベントは、デバッグ中のプログラムにアタッチされたときに SDM によって提供される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド
 このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|`GetErrorMessage`|人間が判読できる文字列としてエラーを返します。|

## <a name="remarks"></a>Remarks
 デバッグ エンジンでエラーが発生した場合、このインターフェイスを使用して、Visual Studio を通じてメッセージをユーザーに報告できます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
