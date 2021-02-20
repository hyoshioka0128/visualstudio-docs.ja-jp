---
title: BeginCapture | Microsoft Docs
description: VsgDbg クラスの BeginCapture メソッドを使用し、EndCapture で終了するキャプチャ区間を開始します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 9edbb52d-ee0b-4cc4-a382-972bcee067d3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a9e002a66ec3ec121a4cdc20ffb9ce59c1ed9dc0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99874575"
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