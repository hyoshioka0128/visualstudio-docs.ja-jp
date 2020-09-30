---
title: 読み込むことができない ActiveX コントロールがブックに含まれています
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: error-reference
f1_keywords:
- VST.SelectDocWizard.ContainsActiveXControls
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 09182fb354ad3ae8937b66952a0acd376d54fe0a
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584452"
---
# <a name="the-workbook-contains-activex-controls-that-cannot-be-loaded"></a>読み込むことができない ActiveX コントロールがブックに含まれています

  プログラムによって Word 文書または Excel ワークシートにコントロールを追加し、ドキュメントまたはブックを保存して、ドキュメントまたはブックに基づいて新しいドキュメントレベルのソリューションを作成すると、"このプロジェクトの作成に使用されるブックには、デザイナーで読み込めない ActiveX コントロールが含まれています" というエラーが表示されます。

 コントロールのマネージド型を記述した情報は、文書またはブックと共に保存されません。 このような文書またはブックに基づいて新しいソリューションを作成すると、コントロールをホスト項目デザイナーに読み込むのに必要な情報が Visual Studio に提供されません。

## <a name="to-correct-this-error"></a>このエラーを解決するには

1. 文書またはブックを開きます。

2. 実行時に追加されたコントロールを削除します。 これを行うには、ドキュメントまたはブックでそれらを選択し、 **del** キーを押します。

3. 文書またはブックに基づいたドキュメント レベルのソリューションを作成します。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
