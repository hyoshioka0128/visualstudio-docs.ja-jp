---
title: をクリックします。マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724837"
---
# <a name="idebugportpicker"></a>IDebugPortPicker
ポートを選択するためのカスタマイズされた UI を表します。

## <a name="syntax"></a>構文

```
IDebugPortPicker : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 このインターフェイスは、ポートサプライヤーによって実装されます。 ポート サプライヤーは、ポート ピッカーを CLSID として公開し、`metricPortPickerCLSID`メトリックを公開 CLSID に向けることによって、ポート ピッカーを定義します。

## <a name="methods"></a>メソッド
 次の表に`IDebugPortPicker`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[DisplayPortPicker](../../../extensibility/debugger/reference/idebugportpicker-displayportpicker.md)|指定されたダイアログ ボックスを表示して、ユーザーがポートを選択できるようにします。|
|[SetSite](../../../extensibility/debugger/reference/idebugportpicker-setsite.md)|サービス プロバイダーを設定します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: を使用します。

 アセンブリ:
