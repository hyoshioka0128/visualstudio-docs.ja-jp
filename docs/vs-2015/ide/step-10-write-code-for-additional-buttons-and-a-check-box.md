---
title: '手順 10: その他のボタンおよびチェック ボックスに対するコードの記述 | Microsoft ドキュメント'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 185cf370-ab39-4ac0-b6bc-601d5b95a4a2
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e24152bf2e6acfcb1ed20b75a5c817e0336cdd4c
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75851597"
---
# <a name="step-10-write-code-for-additional-buttons-and-a-check-box"></a>手順 10: その他のボタンおよびチェック ボックスに対するコードの記述
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ここまでで、他の 4 つのメソッドを実行する準備が整いました。 このコードをコピーして貼り付けることもできますが、コードを入力し、IntelliSense を使用すると、このチュートリアルの学習の効果を最大限に高めることができます。

 このコードは、以前に追加したボタンに機能を追加します。 このコードがないと、ボタンは何も実行しません。 コントロールをアクティブにすると、ボタンは `Click` イベントのコードを使用して (およびチェック ボックスは `CheckChanged` イベントを使用して)、異なる内容を実行します。 たとえば、 **[Clear the picture]** ボタンをクリックしたときにアクティブになる `clearButton_Click` イベントは `Image` プロパティを `null` (または `nothing`) に設定して、現在のイメージを消去します。 コードの各イベントには、コードが実行する内容を説明するコメントが含まれています。

 ![ビデオへのリンク](../data-tools/media/playvideo.gif "PlayVideo")このトピックのビデオ版については、「[チュートリアル 1: Visual Basic でのピクチャビューアーの作成-](https://msdn.microsoft.com/vbasic/gg315356.aspx)ビデオ5」または「[チュートリアル 1 C# : ピクチャビューアーの作成-ビデオ 5](https://msdn.microsoft.com/vcsharp/gg278413.aspx)」を参照してください。 これらのビデオでは、旧バージョンの Visual Studio を使用しているため、一部のメニュー コマンドやその他のユーザー インターフェイス要素が若干異なります。 ただし、概念および手順は、現在のバージョンの Visual Studio でも同様です。

> [!NOTE]
> ベスト プラクティスとして、コードには常にコメントを付けることをお勧めします。 コメントは人が読むための情報であり、時間をかけてでも記述しておけばコードがわかりやすくなります。 コメント行の内容は、プログラムではすべて無視されます。 行をコメント行にするには、Visual C# の場合は先頭に 2 つのスラッシュ (//) を入力し、Visual Basic の場合は先頭に単一引用符 (') を入力します。

### <a name="to-write-code-for-additional-buttons-and-a-check-box"></a>その他のボタンとチェック ボックスのコードを記述するには

- 次のコードを Form1 コード ファイル (Form1.cs または Form1.vb) に追加します。 Visual Basic コードを表示するには **[VB]** タブをクリックします。

     [!code-csharp[VbExpressTutorial1Step9_10#2](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial1step9_10/cs/form1.cs#2)]
     [!code-vb[VbExpressTutorial1Step9_10#2](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial1step9_10/vb/form1.vb#2)]

### <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進むには、「[手順 11: プログラムの実行とその他の機能の使用](../ide/step-11-run-your-program-and-try-other-features.md)」を参照してください。

- チュートリアルの前の手順に戻るには、「[手順 9: 確認、コメントの追加、およびコードのテスト](../ide/step-9-review-comment-and-test-your-code.md)」を参照してください。
