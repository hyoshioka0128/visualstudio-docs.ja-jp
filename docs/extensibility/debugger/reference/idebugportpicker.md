---
title: IDebugPortPicker |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortPicker interface
ms.assetid: 8b7f6685-a3c5-4355-b706-c1b574f6ff84
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 554ac24d7148f0d5de07779f35376b28b7ff7b07
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80724837"
---
# <a name="idebugportpicker"></a>IDebugPortPicker
ポートを選択するためのカスタマイズされた UI を表します。

## <a name="syntax"></a>構文

```
IDebugPortPicker : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、ポートサプライヤーによって実装されます。 ポートサプライヤーは、ポートピッカーを CLSID として公開し、公開された CLSID でメトリックをポイントすることによって、そのポートの選択を定義し `metricPortPickerCLSID` ます。

## <a name="methods"></a>メソッド
 次の表に、のメソッドを示し `IDebugPortPicker` ます。

|Method|説明|
|------------|-----------------|
|[DisplayPortPicker](../../../extensibility/debugger/reference/idebugportpicker-displayportpicker.md)|指定されたダイアログボックスを表示し、ユーザーがポートを選択できるようにします。|
|[SetSite](../../../extensibility/debugger/reference/idebugportpicker-setsite.md)|サービスプロバイダーを設定します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
