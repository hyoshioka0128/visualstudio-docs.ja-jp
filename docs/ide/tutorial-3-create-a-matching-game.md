---
title: 'チュートリアル 3: 絵合わせゲームの作成'
description: プレーヤーが隠されたアイコンのペアを見つける絵合わせゲームの作成方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 10/16/2019
ms.assetid: 525815c8-2845-45e8-be96-100d1f144725
ms.topic: tutorial
ms.technology: vs-ide-general
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cfb5a8af72d7c41cdee913ee94c382c57e8cf5dc
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99971415"
---
# <a name="tutorial-3-create-a-matching-game"></a>チュートリアル 3: 絵合わせゲームの作成

このチュートリアルでは、プレーヤーが隠されたアイコンのペアを見つける絵合わせゲームを作成します。

> [!NOTE]
> このチュートリアルでは、C# と Visual Basic の両方が取り上げられているため、使用しているプログラミング言語固有の情報に注意してください。

このチュートリアルでは、次のタスクについて説明します。

- アイコンなどのオブジェクトを <xref:System.Collections.Generic.List%601> オブジェクトに格納する。

- `foreach` ループ (C# の場合) または `For Each` ループ (Visual Basic の場合) を使用して、リスト内の項目を反復処理する。

- 参照変数を使用してフォームの状態を追跡する。

- 複数のオブジェクトでイベントへの応答に使用できるイベント ハンドラーを作成する。

- 開始されるとカウント ダウンを行い一度だけイベントを発生させるタイマーを作成する。

完了すると、アプリは次の図のようになります。

![このチュートリアルで作成するゲーム](../ide/media/express_finishedgame.png)

## <a name="tutorial-links"></a>チュートリアルのリンク

|Title|[説明]|
|-----------|-----------------|
|[手順 1: プロジェクトの作成とフォームへのテーブルの追加](../ide/step-1-create-a-project-and-add-a-table-to-your-form.md)|プロジェクトを作成し、`TableLayoutPanel` コントロールを追加してコントロールの位置を正しく保つことから始めます。|
|[手順 2: Random オブジェクトおよびアイコンのリストの追加](../ide/step-2-add-a-random-object-and-a-list-of-icons.md)|`Random` オブジェクトおよび `List` オブジェクトを追加し、アイコンのリストを作成します。|
|[手順 3: 各ラベルへのランダムなアイコンの割り当て](../ide/step-3-assign-a-random-icon-to-each-label.md)|`Label` コントロールにアイコンをランダムに割り当てて、各ゲームでそれらの配置が同じにならないようにします。|
|[手順 4: 各ラベルに Click イベント ハンドラーを追加する](../ide/step-4-add-a-click-event-handler-to-each-label.md)|クリックされたラベルの色を変更させる `Click` イベント ハンドラーを追加します。|
|[手順 5: ラベルの参照の追加](../ide/step-5-add-label-references.md)|参照変数を追加して、どのラベルがクリックされたかを追跡します。|
|[手順 6: タイマーの追加](../ide/step-6-add-a-timer.md)|ゲームの実行中に経過した時間を追跡するためのタイマーをフォームに追加します。|
|[手順 7: ペアの表示の維持](../ide/step-7-keep-pairs-visible.md)|一致するペアが選択された場合に、アイコンのペアが表示されたままになるようにします。|
|[手順 8: プレーヤーが勝利したかどうかを確認するメソッドの追加](../ide/step-8-add-a-method-to-verify-whether-the-player-won.md)|プレーヤーが勝利したかどうかを確認する `CheckForWinner()` メソッドを追加します。|
|[手順 9: その他の機能を試す](../ide/step-9-try-other-features.md)|アイコンおよび色の変更、グリッドの追加、サウンドの追加などの、その他の機能を試します。 また、ボードの拡大およびタイマーの調整を試します。|

無料で利用できる便利なビデオ学習リソースもあります。 C# でのプログラミングの詳細については、「[C# の基礎: 入門者向けの開発](https://channel9.msdn.com/Series/C-Sharp-Fundamentals-Development-for-Absolute-Beginners)」を参照してください。 Visual Basic でのプログラミングの詳細については、「[Visual Basic の基礎: 入門者向けの開発](https://channel9.msdn.com/Series/Visual-Basic-Development-for-Absolute-Beginners)」を参照してください。

## <a name="next-steps"></a>次のステップ

チュートリアルを開始するには、「 **[手順 1:プロジェクトの作成とフォームへのテーブルの追加](../ide/step-1-create-a-project-and-add-a-table-to-your-form.md)** 」をご覧ください。

## <a name="see-also"></a>関連項目

* [その他の C# のチュートリアル](../get-started/csharp/index.yml)
* [Visual Basic のチュートリアル](../get-started/visual-basic/index.yml)
* [C++ のチュートリアル](/cpp/get-started/tutorial-console-cpp)