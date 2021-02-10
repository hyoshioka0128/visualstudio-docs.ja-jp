---
title: VsgDbg::~VsgDbg (デストラクター) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7a3b97fb-d344-4df7-b195-9347d1edfcf7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 53d969e6be772b446598c9c3644582684be488a8
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99861349"
---
# <a name="vsgdbgvsgdbg-destructor"></a>VsgDbg::~VsgDbg (デストラクター)
`VsgDbg` クラスのインスタンスを破棄します。 グラフィックス情報がアクティブに記録されている場合、グラフィック ログ ファイルは終了して閉じられ、グラフィックス情報がアクティブにキャプチャされているときに使用されたリソースが解放されます。

## <a name="syntax"></a>構文

```C++
~VsgDbg();
```

## <a name="see-also"></a>関連項目
- [VsgDbg::VsgDbg (コンストラクター)](vsgdbg-vsgdbg-constructor.md)