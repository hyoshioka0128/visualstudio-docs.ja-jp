---
title: 'ワークフロー デザイナー - 方法: 変数デザイナーの使用'
ms.date: 11/04/2016
ms.topic: conceptual
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Presentation.View.DesignTimeVariable.UI
ms.assetid: 0318dfb0-bf8f-4f92-9b86-ae4c1b2161ad
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: dc180df4a9be83c0f0b755bffd7ed40009b41497
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
ms.locfileid: "31970100"
---
# <a name="how-to-use-the-variable-designer"></a>変数デザイナーを使用する方法

変数デザイナーは、データ バインディングや条件ステートメントで使用する変数を作成するために使用します。 デザイナーにアクセスする をクリックして、**変数**デザイン キャンバスの左下隅にあるボタンをクリックします。 デザイナーには以外の各列見出しで並べ替えることができます、表形式で表示されている変数の一覧が含まれています、**既定**列です。 それぞれの変数には、名前、変数の型、スコープ、および既定値 (存在する場合) があります。 名前および既定値は編集可能なテキスト フィールドで、型およびスコープはドロップダウン リストです。 スコープは、変数デザイナーの呼び出し時に選択されたアクティビティです。 選択したスコープ内に変数を作成できない場合は、対応するスコープに変数を作成できる直近の先祖アクティビティが既定のスコープとなります。 詳細については、次を参照してください。[変数と引数 (.NET)](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)です。

 いずれかの並べ替えコントロールをユーザーが明示的に使用するか、変数デザイナーを閉じてから開き直すか、または、別の変数を作成するまで、並べ替え順序は適用されません。

## <a name="to-create-a-new-variable"></a>新しい変数を作成するには

1.  Visual Studio でワークフローまたはアクティビティ ソリューションを開きます。

2.  デザイン キャンバスで、ワークフローのアクティビティを選択します。

3.  変数デザイナーを開く をクリックして、**変数**デザイン キャンバスの左下隅にあるボタンをクリックします。 変数デザイナーが表示されます。

4.  ラベルの付いた空の行をクリックして**変数の作成**です。 新しい行には、次の既定値を使用して新しい変数追加されます: の variablex、**名前**x は一意の変数名を作成して自動的にインクリメントされる 1 の初期値を持つ整数**文字列**の**変数型**、および**シーケンス**の**スコープ**です。 値は追加されません**既定**です。 これらの値は、ワークフローのデザイン プロセス中にいつでも変更できます。

    > [!NOTE]
    > 削除する変数をクリックして、変数を選択し、キーを押します、**削除**キー。

## <a name="see-also"></a>関連項目

- [ワークフロー デザイナーの使用](../workflow-designer/using-the-workflow-designer.md)
- [変数と引数](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)
- [方法: 引数デザイナーを使用する](../workflow-designer/how-to-use-the-argument-designer.md)