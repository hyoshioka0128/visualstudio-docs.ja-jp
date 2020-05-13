---
title: グラフィックスフレームの検証 |Microsoft Docs
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
ms.openlocfilehash: 49248c6209f9e56e51551f6cd3d4af66ecac8b56
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72735497"
---
# <a name="graphics-frame-validation"></a>グラフィックスフレームの検証
<!-- VERSIONLESS -->
Visual Studio 2017 以降では、**フレーム検証**ツールがサポートされています。  [フレームの検証] ウィンドウには、イベント一覧に関連付けられたエラーと警告が表示されます。  このウィンドウを表示するには、 **[> フレームの検証]** メニューを選択します。

![フレームの検証](media/gfx_diag_frame_validation.png)

左上隅にある **[検証の実行]** ボタンをクリックして、分析を開始します。  フレームの複雑さによっては、完了までに数分かかる場合があります。  ここに表示されるデータは、 [SDK レイヤー](/windows/desktop/direct3d11/overviews-direct3d-11-devices-layers)が有効になったときに D3D 自体が生成するメッセージと、ツール自体の内部状態追跡から収集されたデータという2つのソースからの組み合わせです。 完了すると、データの列がいくつか表示されます。

| **列** | **説明** |
|------------| - |
| イベント ID | [[イベント一覧](graphics-event-list.md)] ウィンドウのエントリにマップされる ID。 |
| 重要度 | 破損、エラー、警告、情報、またはメッセージ。 |
| カテゴリ | アプリケーション定義、その他、初期化、クリーンアップ、コンパイル、状態の作成、状態の設定、状態の取得、実行、リソースの操作、シェーダー、冗長、未使用。 |
| [メッセージ] | イベントに関連付けられているメッセージ。 |
| event | エラーまたは警告に関連付けられたイベント。 |

## <a name="see-also"></a>関連項目
[グラフィックス診断 (DirectX グラフィックスのデバッグ)](visual-studio-graphics-diagnostics.md)
<!-- /VERSIONLESS -->
