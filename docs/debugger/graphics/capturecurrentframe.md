---
title: CaptureCurrentFrame |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 4509311d-6fe2-4b65-9b4a-ff0522585d6a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b9967d776845088e707035c7b1c56855ac80af82
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72736132"
---
# <a name="capturecurrentframe"></a>CaptureCurrentFrame
現在のフレームの残りの部分を、グラフィックス ログ ファイルにキャプチャします。

## <a name="syntax"></a>構文

```C++
void CaptureCurrentFrame();
```

## <a name="remarks"></a>Remarks
 `BeginCapture` 関数によって開始されたキャプチャなど、別のキャプチャ操作が進行中の場合、そのキャプチャ操作は完了し、別個のフレームとしてグラフィックス ログに記録されます。 その直後、グラフィックス診断によって現在のフレームの残りの部分のキャプチャが開始され、それも個別のフレームとして記録されます。 present への呼び出しによって、現在のフレームの末尾がマークされます。

 フレームをキャプチャするには、グラフィックス情報をキャプチャして記録するようにアプリを準備する必要があります。つまり、`CaptureCurrentFrame` を呼び出す前に、`VsgDbg` クラスのインスタンスを使用して[Init](init.md)を呼び出す必要があります。

## <a name="see-also"></a>関連項目
- [Init](init.md)
- [BeginCapture](begincapture.md)
