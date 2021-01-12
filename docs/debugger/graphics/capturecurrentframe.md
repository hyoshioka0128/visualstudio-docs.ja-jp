---
title: CaptureCurrentFrame | Microsoft Docs
description: VsgDbg クラスの CaptureCurrentFrame メソッドを使用し、現在のフレームの残りの部分をグラフィックス ログ ファイルにキャプチャします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 4509311d-6fe2-4b65-9b4a-ff0522585d6a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 793d86ac7d23fa209560222415dce50f4e5ac508
ms.sourcegitcommit: fcfd0fc7702a47c81832ea97cf721cca5173e930
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2020
ms.locfileid: "97727945"
---
# <a name="capturecurrentframe"></a>CaptureCurrentFrame
現在のフレームの残りの部分を、グラフィックス ログ ファイルにキャプチャします。

## <a name="syntax"></a>構文

```C++
void CaptureCurrentFrame();
```

## <a name="remarks"></a>Remarks
 `BeginCapture` 関数によって開始されたキャプチャなど、別のキャプチャ操作が進行中の場合、そのキャプチャ操作は完了し、別個のフレームとしてグラフィックス ログに記録されます。 その直後、グラフィックス診断によって現在のフレームの残りの部分のキャプチャが開始され、それも個別のフレームとして記録されます。 present への呼び出しによって、現在のフレームの末尾がマークされます。

 フレームをキャプチャするには、グラフィックス情報をキャプチャして記録するようにアプリケーションを準備する必要があります。つまり、`CaptureCurrentFrame` を呼び出す前に、`VsgDbg` クラスのインスタンスを通じて [Init](init.md) を呼び出してしておく必要があります。

## <a name="see-also"></a>関連項目
- [Init](init.md)
- [BeginCapture](begincapture.md)