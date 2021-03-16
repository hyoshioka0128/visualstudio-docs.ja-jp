---
description: 指定されたブール値パラメーターに基づいて、既定でグラフィックス情報をアクティブにキャプチャして記録するようにグラフィックス診断のアプリ内コンポーネントを準備するか、または準備をせずに、VsgDbg クラスのインスタンスを構築します。
title: VsgDbg::VsgDbg (コンストラクター) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 670651e6-5e79-4845-b0c2-671beb7055a8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ae4259b1af1bcb51b05431131db596d2a26da895
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102160447"
---
# <a name="vsgdbgvsgdbg-constructor"></a>VsgDbg::VsgDbg (コンストラクター)
指定されたブール値パラメーターに基づいて、既定でグラフィックス情報をアクティブにキャプチャして記録するようにグラフィックス診断のアプリ内コンポーネントを準備をするか、または準備しないで、`VsgDbg` クラスのインスタンスを構築します。

## <a name="syntax"></a>構文

```C++
VsgDbg(
  bDefaultInit
);
```

#### <a name="parameters"></a>パラメーター
 `bDefaultInit`: グラフィックス情報をアクティブにキャプチャして記録するようにグラフィックス診断のアプリ内コンポーネントを準備することを指定する場合は `true`、この時点ではグラフィックス情報をアクティブにキャプチャして記録するようにアプリケーションを準備しないことを指定する場合は `false`。

## <a name="remarks"></a>Remarks
 `bDefaultInit` に `true` が設定された状態でコンストラクターが呼び出された場合、グラフィックス ログ ファイルの名前は、`vsgcapture.h` がアプリケーションに含まれる前にプリプロセッサ シンボル `DONT_SAVE_VSGLOG_TO_TEMP` および `VSG_DEFAULT_RUN_FILENAME` がどのように定義されているかによって決まります。

 `bDefaultInit` が `false` に設定された状態でコンストラクターが呼び出された場合、後で `Init` 関数を呼び出して、グラフィックス情報をアクティブにキャプチャして記録するようにグラフィックス診断のアプリ内コンポーネントを準備できます。

## <a name="see-also"></a>関連項目
- [VsgDbg::~VsgDbg (デストラクター)](vsgdbg-tilde-vsgdbg-destructor.md)
- [Init](init.md)
- [DONT_SAVE_VSGLOG_TO_TEMP](dont-save-vsglog-to-temp.md)
- [VSG_DEFAULT_RUN_FILENAME](vsg-default-run-filename.md)
