---
title: グラフィックス フレームの検証 | Microsoft Docs
description: Visual Studio のグラフィックス用フレーム検証ツールについて説明します。 このツールには、イベントの一覧に関連付けられたエラーと警告が表示されます。
ms.custom: SEO-VS-2020
ms.date: 03/02/2017
ms.topic: conceptual
f1_keywords:
- vs.graphics.FrameValidation
ms.assetid: 1e639182-1301-4e28-9c1e-b5df732f3f1b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0fe9b1ed3acbe588b342ba6550bc45558a2070d2
ms.sourcegitcommit: fcfd0fc7702a47c81832ea97cf721cca5173e930
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2020
ms.locfileid: "97727646"
---
# <a name="graphics-frame-validation"></a>グラフィックス フレームの検証
<!-- VERSIONLESS -->
Visual Studio 2017 以降では、**フレームの検証** ツールがサポートされています。  [フレームの検証] ウィンドウには、イベントの一覧に関連付けられたエラーと警告が表示されます。  このウィンドウを表示するには、 **[表示] > [フレームの検証]** メニューを選択します。

![フレームの検証](media/gfx_diag_frame_validation.png)

左上隅にある **[検証の実行]** ボタンをクリックして、分析を開始します。  フレームの複雑さによっては、完了するまでに数分かかることがあります。  ここに表示されるデータは、次の 2 つのソースのデータの組み合わせです: [SDK レイヤー](/windows/desktop/direct3d11/overviews-direct3d-11-devices-layers)が有効なときに D3D 自体によって生成されるメッセージと、ツールの独自の内部状態追跡から収集されたデータ。 完了すると、さまざまなデータ列が表示されます。

| **列** | **説明** |
|------------| - |
| イベント ID | [[イベントの一覧]](graphics-event-list.md) ウィンドウ内のエントリにマップされる ID。 |
| 重要度 | 破損、エラー、警告、情報、またはメッセージ。 |
| カテゴリ | アプリケーション定義、その他、初期化、クリーンアップ、コンパイル、状態の作成、状態の設定、状態の取得、実行、リソースの操作、シェーダー、冗長、未使用。 |
| メッセージ | イベントに関連付けられたメッセージ。 |
| event | エラーまたは警告に関連付けられたイベント。 |

## <a name="see-also"></a>関連項目
[グラフィックス診断 (DirectX グラフィックスのデバッグ)](visual-studio-graphics-diagnostics.md)
<!-- /VERSIONLESS -->