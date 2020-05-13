---
title: イベント 2 をアクティブにする |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugActivateDocumentEvent2
helpviewer_keywords:
- IDebugActivateDocumentEvent2 interface
ms.assetid: 6f37edd7-a48c-4b41-b160-dff9be63a284
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f601027ce9e71dff6687bcd6aa1b08f13f5ce0cf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736619"
---
# <a name="idebugactivatedocumentevent2"></a>IDebugActivateDocumentEvent2
デバッグ エンジン (DE) は、読み込まれるドキュメントを要求するのにこのインターフェイスを使用します。

## <a name="syntax"></a>構文

```
IDebugActivateDocumentEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 DE は、ソース ファイルを開く必要があるときに、このインターフェイスを実装します。 このインターフェイスは、スクリプト インタープリタの一部または一部であるデバッグ エンジンによってのみ実装されます。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM は、インターフェイス`IDebugEvent2`にアクセスするのに[QueryInterface](/cpp/atl/queryinterface)を使用します)。

## <a name="notes-for-callers"></a>発信者向けのメモ
 デは、ソース ファイルを開く必要があるときに、このイベント オブジェクトを作成して送信します。 イベントは、デバッグ中のプログラムにアタッチされたときに、SDM によって提供される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugActivateDocumentEvent2`、 のメソッドを示します。

|メソッド|説明|
|-------------|-----------------|
|[GetDocument](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocument.md)|アクティブ化するドキュメントを取得します。|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocumentcontext.md)|ドキュメント内の位置を記述するドキュメント コンテキストを取得します。|

## <a name="remarks"></a>Remarks
 このインターフェイスを使用する一般的なシナリオは、HTML ページのスクリプト コードで解析エラーが発生した場合、スクリプト DE は、解析エラーを持つドキュメントを表示できるように、SDM にこのインターフェイスを送信します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
