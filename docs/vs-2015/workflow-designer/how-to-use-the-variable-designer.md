---
title: '方法: 変数デザイナーを使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Presentation.View.DesignTimeVariable.UI
ms.assetid: 0318dfb0-bf8f-4f92-9b86-ae4c1b2161ad
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4744864824da5efb238e9af1a5a12fcef79ea4ff
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72659074"
---
# <a name="how-to-use-the-variable-designer"></a>変数デザイナーを使用する方法
変数デザイナーは、データ バインディングや条件ステートメントで使用する変数を作成するために使用します。 デザイナーにアクセスするには、デザインキャンバスの左下隅にある [ **変数** ] ボタンをクリックします。 デザイナーには、表形式で表示される変数の一覧が含まれており、 **既定** の列を除き、各列ヘッダーで並べ替えることができます。 それぞれの変数には、名前、変数の型、スコープ、および既定値 (存在する場合) があります。 名前および既定値は編集可能なテキスト フィールドで、型およびスコープはドロップダウン リストです。 スコープは、変数デザイナーの呼び出し時に選択されたアクティビティです。 選択したスコープ内に変数を作成できない場合は、対応するスコープに変数を作成できる直近の先祖アクティビティが既定のスコープとなります。 [!INCLUDE[crabout](../includes/crabout-md.md)] 変数、「 [変数と引数](https://msdn.microsoft.com/library/d03dbe34-5b2e-4f21-8b57-693ee49611b8)」を参照してください。

 いずれかの並べ替えコントロールをユーザーが明示的に使用するか、変数デザイナーを閉じてから開き直すか、または、別の変数を作成するまで、並べ替え順序は適用されません。

### <a name="to-create-a-new-variable"></a>新しい変数を作成するには

1. [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] でワークフロー ソリューションまたはアクティビティ ソリューションを開きます。

2. デザイン キャンバスで、ワークフローのアクティビティを選択します。

3. デザインキャンバスの左下隅にある [ **変数** ] ボタンをクリックして、変数デザイナーを開きます。 変数デザイナーが表示されます。

4. [ **変数の作成**] という名前の空の行をクリックします。 次の既定値を使用して新しい変数を含む新しい行が追加されます **。ここで**、x は整数です。ここで、x は、一意の変数名を作成するために自動的にインクリメントされる整数、**変数型**の場合は**String** 、**スコープ**の場合は**シーケンス**です。 **既定**では、値は追加されません。 これらの値は、ワークフローのデザイン プロセス中にいつでも変更できます。

    > [!NOTE]
    > 変数を削除するには、変数をクリックして選択し、 **del** キーを押します。

## <a name="see-also"></a>参照
 [ワークフローデザイナーの](../workflow-designer/using-the-workflow-designer.md)[変数と引数](https://msdn.microsoft.com/library/d03dbe34-5b2e-4f21-8b57-693ee49611b8)の使用[方法: 引数デザイナーを使用する](../workflow-designer/how-to-use-the-argument-designer.md)