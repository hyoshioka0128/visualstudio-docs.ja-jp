---
title: その他のボタンおよびチェック ボックスに対するコードの記述
description: 画像ビューアーの作成チュートリアル内のその他のボタンとチェック ボックスのコードを記述する方法を説明します。
ms.date: 08/30/2019
ms.custom: SEO-VS-2020
ms.assetid: 185cf370-ab39-4ac0-b6bc-601d5b95a4a2
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 29d4dc70195d4c98653bc8503a079f462a502809
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106214370"
---
# <a name="step-10-write-code-for-additional-buttons-and-a-check-box"></a>手順 10: その他のボタンおよびチェック ボックスに対するコードの記述

ここまでで、他の 4 つのメソッドを実行する準備が整いました。 このコードをコピーして貼り付けることもできますが、コードを入力し、IntelliSense を使用すると、このチュートリアルの学習の効果を最大限に高めることができます。

このコードは、以前に追加したボタンに機能を追加します。 このコードがないと、ボタンは何も実行しません。 コントロールをアクティブにすると、ボタンは <xref:System.Windows.Forms.Control.Click> イベントのコードを使用して (およびチェック ボックスは <xref:System.Windows.Forms.CheckBox.CheckedChanged> イベントを使用して)、異なる内容を実行します。 たとえば、**[Clear the picture]** ボタンをクリックするとアクティブになる `clearButton_Click` (または `ClearButton_Click`) イベントでは、**Image** プロパティが **null** (または **nothing**) に設定されることによって、現在のイメージが消去されます。 コードの各イベントには、コードが実行する内容を説明するコメントが含まれています。

> [!TIP]
> ベスト プラクティスとして、コードには常にコメントを付けることをお勧めします。 コメントは人が読むための情報であり、時間をかけてでも記述しておけばコードがわかりやすくなります。 コメント行の内容は、アプリではすべて無視されます。 行をコメント行にするには、C# の場合は先頭に 2 つのスラッシュ (//) を入力し、Visual Basic の場合は先頭に単一引用符 (') を入力します。

## <a name="how-to-write-code-for-additional-buttons-and-a-check-box"></a>その他のボタンとチェック ボックスのコードを記述する方法

次のコードを **Form1** コード ファイル (*Form1.cs* または *Form1.vb*) に追加します。

  [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

  :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial1step9_10/cs/form1.cs" id="Snippet2":::

  :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial1step9_10/vb/form1.vb" id="Snippet2":::

> [!NOTE]
> ご利用のコードでは、"camelCase" という文字が表示されない場合があります。

## <a name="next-steps"></a>次のステップ

* チュートリアルの次の手順に進むには、 **[手順 11: アプリの実行とその他の機能の使用](../ide/step-11-run-your-program-and-try-other-features.md)** に関するページを参照してください。

* チュートリアルの前の手順に戻るには、「[手順 9: 確認、コメントの追加、およびコードのテスト](../ide/step-9-review-comment-and-test-your-code.md)」を参照してください。

## <a name="see-also"></a>関連項目

* [チュートリアル 2: 制限時間ありの計算クイズの作成](tutorial-2-create-a-timed-math-quiz.md)
* [チュートリアル 3: 絵合わせゲームの作成](tutorial-3-create-a-matching-game.md)
