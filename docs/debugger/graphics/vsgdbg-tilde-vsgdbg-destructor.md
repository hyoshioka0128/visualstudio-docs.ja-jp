---
description: VsgDbg クラスのインスタンスを破棄します。
title: VsgDbg::~VsgDbg (デストラクター) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7a3b97fb-d344-4df7-b195-9347d1edfcf7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d90664723695756ebd8acdc7c56bec1fcbd08a31
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102155227"
---
# <a name="vsgdbgvsgdbg-destructor"></a>VsgDbg::~VsgDbg (デストラクター)
`VsgDbg` クラスのインスタンスを破棄します。 グラフィックス情報がアクティブに記録されている場合、グラフィック ログ ファイルは終了して閉じられ、グラフィックス情報がアクティブにキャプチャされているときに使用されたリソースが解放されます。

## <a name="syntax"></a>構文

```C++
~VsgDbg();
```

## <a name="see-also"></a>関連項目
- [VsgDbg::VsgDbg (コンストラクター)](vsgdbg-vsgdbg-constructor.md)
