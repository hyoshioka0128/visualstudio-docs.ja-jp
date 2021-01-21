---
title: BeginCapture | Microsoft Docs
description: VsgDbg クラスの BeginCapture メソッドを使用し、EndCapture で終了するキャプチャ区間を開始します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 9edbb52d-ee0b-4cc4-a382-972bcee067d3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 931e7ab05442a429c0b9e6468d42aadca942c1ee
ms.sourcegitcommit: fcfd0fc7702a47c81832ea97cf721cca5173e930
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2020
ms.locfileid: "97727966"
---
# <a name="begincapture"></a>BeginCapture
`EndCapture` で終了するキャプチャ区間を開始します。

## <a name="syntax"></a>構文

```C++
void BeginCapture();
```

## <a name="remarks"></a>Remarks
 特定種類の描画呼び出しに関するグラフィック情報だけをキャプチャするときなど、キャプチャ区間は通常 1 つのフレームのサブセットに及びます。 キャプチャ区間が present への呼び出しに及ぶ場合は、2 つのフレームのグラフィックス情報がキャプチャされます。 最初のフレームは、`BeginCapture` への呼び出しと present への呼び出しの間の区間に及びます。2 つ目のフレームは、present への呼び出しの後の最初の Direct3D イベントと `EndCapture` への呼び出しの間の区間に及びます。

 区間をキャプチャするには、グラフィックス情報をキャプチャして記録するようにアプリケーションを準備する必要があります。つまり、`BeginCapture` または `EndCapture` を呼び出す前に、`VsgDbg` クラスのインスタンスを通じて [Init](init.md) を呼び出してしておく必要があります。

## <a name="see-also"></a>関連項目
- [EndCapture](endcapture.md)
- [CaptureCurrentFrame](capturecurrentframe.md)