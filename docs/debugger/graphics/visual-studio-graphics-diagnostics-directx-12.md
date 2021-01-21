---
title: Visual Studio での DirectX 12 のサポート | Microsoft Docs
description: DirectX 12 でフル グラフィックのデバッグ エクスペリエンスを実現するには、Windows の PIX を使用することをお勧めします
ms.date: 09/29/2020
ms.topic: conceptual
author: davidcongruili
ms.author: davidli1
manager: mluparu
ms.workload:
- multiple
ms.openlocfilehash: 9dbc52a0233abe467da4d41af0134663bc7cd9df
ms.sourcegitcommit: a1cb4e2025045c2ad79167645c4c0f33b94b1152
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2020
ms.locfileid: "91671416"
---
# <a name="directx-12-support-in-visual-studio"></a>Visual Studio での DirectX 12 のサポート

## <a name="directx-12-support"></a>DirectX 12 のサポート

Visual Studio グラフィックス診断では、DirectX 12 のゲームはサポートされていません。 Visual Studio で DirectX 12 を完全にサポートするグラフィカル デバッグを行うには、"*Windows の PIX*" を使用することをお勧めします。 

Windows の PIX は、リモート機能を備えたパフォーマンス チューニングおよびデバッグ ツールです。 Windows の PIX には、グラフィカル デバッグのニーズに合わせた主要な機能が 7 つ用意されています。 GPU キャプチャによって Direct3D 12 グラフィックス レンダリングのパフォーマンスをデバッグおよび分析します。 ゲームによって実行されるすべての CPU および GPU 作業のパフォーマンスとスレッド処理をタイミングのキャプチャによって把握します。 ファイル IO キャプチャを使用して、タイトルのディスク IO パターンとパッケージ レイアウトの非効率性を特定します。

グラフィカル デバッグの作業を [**Windows の PIX**](https://aka.ms/PIXonWindows) を使用して進めましょう。

[**Windows の PIX をダウンロードする**](https://aka.ms/downloadPIX)か、[**ドキュメントを参照**してください。](https://devblogs.microsoft.com/pix/documentation/)

## <a name="pix-on-windows"></a>Windows の PIX

Windows の PIX には、次の 7 つの操作モードがあります。
1. **GPU キャプチャ** - Direct3D 12 グラフィックス レンダリングのパフォーマンスをデバッグおよび分析します。
2. **タイミングのキャプチャ** - ゲームによって実行されるすべての CPU および GPU 作業のパフォーマンスとスレッド処理を把握し、GPU メモリ使用率を追跡します。
3. **関数の概要のキャプチャ** - 各関数の実行時間と各関数が呼び出される頻度についての情報を蓄積します。
4. **コールグラフのキャプチャ** - 1 つの関数の実行をトレースします。
5. **メモリ割り当てのキャプチャ** - ゲームによって行われたメモリ割り当てに関する分析情報を提供します。
6. **ファイル IO キャプチャ** - タイトルのディスク IO パターンとパッケージ レイアウトの非効率性を特定できます。
7. **システム モニター** - ゲームの実行中にリアルタイムのカウンター データを表示します。

Windows の PIX の詳細なビデオは、[**こちら**](https://www.youtube.com/playlist?list=PLeHvwXyqearWuPPxh6T03iwX-McPG5LkB)をご覧ください
