---
title: を行う必要があります。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugIDECallback interface
ms.assetid: 8d31adc0-1c44-4658-8d4f-f4b73e35f4a6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 585ff354cef9686097325ea4dea25cd08c4cbb1b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727825"
---
# <a name="idebugidecallback"></a>IDebugIDECallback
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 デバッガーの出力ウィンドウにメッセージを表示する式エバリュエーター (EE) を有効にします。

## <a name="syntax"></a>構文

```
IDebugIDECallback : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 このコールバックは、マネージ デバッグ エンジンによって実装されます。

## <a name="notes-for-callers"></a>発信者向けのメモ
 デバッガーの出力ウィンドウに出力を送信する式エバリュエーターによって使用できます。

## <a name="methods"></a>メソッド
 このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[メッセージを表示する](../../../extensibility/debugger/reference/idebugidecallback-displaymessage.md)|指定したメッセージ文字列をデバッガーの出力ウィンドウに送信します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Ee.h

 名前空間: を使用します。

 アセンブリ:
