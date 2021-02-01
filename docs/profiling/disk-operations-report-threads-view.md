---
title: ディスク操作レポート (スレッド ビュー) | Microsoft Docs
description: ディスク操作レポートには、ディスク チャネルにおけるディスク I/O 操作が表示されます。 各ディスク アクセスについて報告される情報を確認します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.report.diskoperations
helpviewer_keywords:
- Concurrency Visualizer, File Operations Report (Threads View)
ms.assetid: e352f4f3-f654-45eb-96ed-417863487ddc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 44975999c71b1c331d90aa10f709071cef466cb1
ms.sourcegitcommit: d13f7050c873b6284911d1f4acf07cfd29360183
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2021
ms.locfileid: "98686533"
---
# <a name="disk-operations-report-threads-view"></a>ディスク操作レポート (スレッド ビュー)
ディスク操作レポートには、ディスク チャネルにおけるディスク I/O 操作が表示されます。

 現在表示されている時間帯でプロファイリングされているプロセスの代わりに発生する各ディスク アクセスについて、この情報が報告されます。

- ディスク アクセスを実行したプロセスの名前と PID

- ディスクにアクセスしたスレッドの ID

- アクセスされたファイルの名前

- 各ファイルの読み取りの数

- 読み取られたバイト数

- 読み取り待機時間 (ミリ秒)

- 書き込み数

- 書き込まれたバイト数

- 書き込み待機時間 (ミリ秒)

## <a name="see-also"></a>関連項目
- [スレッド ビュー](../profiling/threads-view-parallel-performance.md)