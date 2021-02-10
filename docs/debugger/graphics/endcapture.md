---
title: EndCapture | Microsoft Docs
description: VsgDbg クラスの EndCapture メソッドを使用し、BeginCapture で開始されたキャプチャ区間を終了します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 06084c3b-e065-49b6-968e-d578762fb871
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3f7733eb9bed86bc450e4438ce34054312b13db5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99880282"
---
# <a name="endcapture"></a>EndCapture
`BeginCapture` で開始されたキャプチャ区間を終了します。

## <a name="syntax"></a>構文

```C++
void EndCapture();
```

## <a name="remarks"></a>Remarks
 特定種類の描画呼び出しに関するグラフィック情報だけをキャプチャするときなど、キャプチャ区間は通常 1 つのフレームのサブセットに及びます。 キャプチャ区間が present への呼び出しに及ぶ場合は、2 つのフレームのグラフィックス情報がキャプチャされます。 最初のフレームは、`BeginCapture` への呼び出しと present への呼び出しの間の区間に及びます。2 つ目のフレームは、present への呼び出しの後の最初の Direct3D イベントと `EndCapture` への呼び出しの間の区間に及びます。

 区間をキャプチャするには、グラフィックス情報をキャプチャして記録するようにアプリケーションを準備する必要があります。つまり、`BeginCapture` または `EndCapture` を呼び出す前に、`VsgDbg` クラスのインスタンスを通じて [Init](init.md) を呼び出してしておく必要があります。

## <a name="see-also"></a>関連項目
- [BeginCapture](begincapture.md)
- [CaptureCurrentFrame](capturecurrentframe.md)