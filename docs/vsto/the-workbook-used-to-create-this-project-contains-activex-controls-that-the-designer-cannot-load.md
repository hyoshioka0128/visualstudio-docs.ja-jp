---
title: 読み込むことができない ActiveX コントロールがブックに含まれています
description: 読み込むことができない ActiveX コントロールがブックに含まれている場合に発生するエラーを解決する方法について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 7257e3940af72f344906642adc51a1dd98cb3f25
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97524180"
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
