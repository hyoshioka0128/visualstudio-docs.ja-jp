---
description: デバッガーの出力ウィンドウにメッセージを表示する式エバリュエーター (EE) を有効にします。
title: IDebugIDECallback |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugIDECallback interface
ms.assetid: 8d31adc0-1c44-4658-8d4f-f4b73e35f4a6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d0ef2072967aad5f2cd012283b0c6f4ac7b9b3be
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102172559"
---
# <a name="idebugidecallback"></a>IDebugIDECallback
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 デバッガーの出力ウィンドウにメッセージを表示する式エバリュエーター (EE) を有効にします。

## <a name="syntax"></a>構文

```
IDebugIDECallback : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このコールバックはマネージデバッグエンジンによって実装されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 デバッガーの出力ウィンドウに出力を送信するために、式エバリュエーターによって使用される場合があります。

## <a name="methods"></a>メソッド
 このインターフェイスは、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[DisplayMessage](../../../extensibility/debugger/reference/idebugidecallback-displaymessage.md)|指定したメッセージ文字列をデバッガーの出力ウィンドウに送信します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Ee

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
