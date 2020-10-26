---
title: '方法: 引数デザイナーを使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Presentation.View.ArgumentDesigner.UI
- System.Activities.Presentation.View.DesignTimeArgument.UI
ms.assetid: 64813fd5-1ea1-499a-98b4-ab2a44b7ee5e
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a436d33bbb7c791f3f192357fded779fa77d148d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72659113"
---
# <a name="how-to-use-the-argument-designer"></a>引数デザイナーを使用する方法
[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] の以前のバージョンと比べ、引数デザイナーを使用した場合は、アクティビティとの間のデータの受け渡しを簡単に実行できます。 デザイナーにアクセスするには、デザインキャンバスの左下隅にある [ **引数** ] ボタンをクリックします。 デザイナーには、表形式で表示される引数の一覧が含まれており、 **既定値** の列を除き、各列ヘッダーで並べ替えることができます。 各引数には、名前、方向 (入力、出力、入力/出力、またはプロパティ)、型、および既定の式の値 (存在する場合) が含まれます。 名前および既定の式の値は編集可能なテキスト フィールドで、型および方向はドロップダウンです。 [!INCLUDE[crabout](../includes/crabout-md.md)] 引数、「 [変数と引数](https://msdn.microsoft.com/library/d03dbe34-5b2e-4f21-8b57-693ee49611b8)」を参照してください。

### <a name="to-create-a-new-argument"></a>新しい引数を作成するには

1. [!INCLUDE[vs2010](../includes/vs2010-md.md)] でワークフロー ソリューションまたはアクティビティ ソリューションを開きます。

2. デザインキャンバスの左下隅にある [ **引数** ] ボタンをクリックして、引数デザイナーを開きます。 引数デザイナーが表示されます。

3. [ **引数の作成**] というラベルの付いた空の行をクリックします。 これにより、新しい引数を含む新しい行が追加されます。**名前**には argumentx を使用します。ここで、x は、一意の引数名を作成するために自動的にインクリメントされ、**方向**が、**引数の型**が**String** **で**ある整数です。 **既定値**の値は追加されません。 これらの値は、ワークフローのデザイン プロセス中にいつでも変更できます。

    > [!NOTE]
    > 引数を削除するには、引数をクリックして選択し、 **del** キーを押します。

## <a name="see-also"></a>参照
 [ワークフローデザイナーの](../workflow-designer/using-the-workflow-designer.md)[変数と引数](https://msdn.microsoft.com/library/d03dbe34-5b2e-4f21-8b57-693ee49611b8)の使用