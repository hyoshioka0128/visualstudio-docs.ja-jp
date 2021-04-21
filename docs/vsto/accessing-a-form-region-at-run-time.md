---
title: 実行時のフォーム領域へのアクセス
description: 実行時に Microsoft Office のさまざまなプロジェクトの種類とバージョンでフォーム領域にアクセスする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Inspectors [Office development in Visual Studio]
- Explorers [Office development in Visual Studio]
- form regions [Office development in Visual Studio], accessing at run time
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: dbd60f5773392af2066e4693751dd6fff99128b9
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827969"
---
# <a name="access-a-form-region-at-run-time"></a>実行時のフォーム領域へのアクセス

|適用対象|
|----------------|
|このトピックの情報は、次の種類のプロジェクトおよび Microsoft Office のバージョンにのみ適用されます。 詳細については、「 [Office アプリケーションおよびプロジェクトの種類別の使用可能な機能](../vsto/features-available-by-office-application-and-project-type.md)」を参照してください。<br /><br /> **プロジェクトの種類**<br /><br /> -VSTO アドインプロジェクト<br /><br /> **Microsoft Office のバージョン**<br /><br /> -   [!INCLUDE[Outlook_14_short](../vsto/includes/outlook-14-short-md.md)]|

 `Globals` クラスを使用すると、Outlook プロジェクトの任意の場所からフォーム領域にアクセスできます。 クラスの詳細につい `Globals` ては、「 [Office プロジェクト内のオブジェクトへのグローバルアクセス](../vsto/global-access-to-objects-in-office-projects.md)」を参照してください。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="access-form-regions-that-appear-in-a-specific-outlook-inspector-window"></a>特定の Outlook インスペクターウィンドウに表示されるフォーム領域へのアクセス
 特定の Outlook インスペクターに表示されるすべてのフォーム領域にアクセスするには、 `FormRegions` クラスの `Globals` プロパティを呼び出し、インスペクターを表す <xref:Microsoft.Office.Interop.Outlook.Inspector> オブジェクトを渡します。

 次の例では、現在フォーカスが設定されているインスペクターに表示されるフォーム領域のコレクションを取得します。 この例では、次に、 `formRegion1` というコレクション内のフォーム領域にアクセスし、テキスト ボックス内のテキストを `Hello World`に設定します。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Access_O12/ThisAddIn.vb" id="Snippet2":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Access_O12/ThisAddIn.cs" id="Snippet2":::

## <a name="access-form-regions-that-appear-in-a-specific-outlook-explorer-window"></a>特定の Outlook エクスプローラーウィンドウに表示されるフォーム領域へのアクセス
 特定の Outlook エクスプローラーに表示されるすべてのフォーム領域にアクセスするには、 `FormRegions` クラスの `Globals` プロパティを呼び出し、エクスプローラーを表す <xref:Microsoft.Office.Interop.Outlook.Explorer> オブジェクトを渡します。

 次の例では、現在フォーカスが設定されているエクスプローラーに表示されるフォーム領域のコレクションを取得します。 この例では、次に、 `formRegion1` というコレクション内のフォーム領域にアクセスし、テキスト ボックス内のテキストを `Hello World`に設定します。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Access_O12/ThisAddIn.vb" id="Snippet3":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Access_O12/ThisAddIn.cs" id="Snippet3":::

## <a name="access-all-form-regions"></a>すべてのフォーム領域にアクセスする
 すべてのエクスプローラーおよびすべてのインスペクターに表示されるすべてのフォーム領域にアクセスするには、 `FormRegions` クラスの `Globals` プロパティを呼び出します。

 次の例では、すべてのエクスプローラーおよびすべてのインスペクターに表示されるフォーム領域のコレクションを取得します。 この例では、次に、 `formRegion1` というフォーム領域にアクセスし、テキスト ボックス内のテキストを `Hello World`に設定します。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Access_O12/ThisAddIn.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Access_O12/ThisAddIn.cs" id="Snippet1":::

## <a name="access-controls-on-a-form-region"></a>フォーム領域上のコントロールへのアクセス
 `Globals` クラスを使用してフォーム領域のコントロールにアクセスするには、それらのコントロールを、フォーム領域コード ファイルの外部にあるコードからアクセスできるようにする必要があります。

### <a name="form-regions-designed-in-the-form-region-designer"></a>フォーム領域デザイナーでデザインされたフォーム領域
 C# の場合は、アクセス対象にする各コントロールの修飾子を変更します。 この操作を行うには、フォーム領域デザイナーで各コントロールを選択し、 **[プロパティ]** ウィンドウで **Modifiers** プロパティを **Internal** または **public** に変更します。 たとえば、 **の** Modifier `textBox1` プロパティを **Internal** に変更すると、 `textBox1` と入力して `Globals.FormRegions.FormRegion1.textBox1`にアクセスできます。

 Visual Basic の場合は、修飾子を変更する必要はありません。

### <a name="imported-form-regions"></a>インポートされたフォーム領域
 Outlook でデザインされたフォーム領域をインポートすると、フォーム領域上の各コントロールのアクセス修飾子はプライベートになります。 インポートされたフォーム領域をフォーム領域デザイナーで変更することはできないため、 **[プロパティ]** ウィンドウでコントロールの修飾子を変更する方法はありません。

 フォーム領域コード ファイルの外部からコードにアクセスできるようにするには、フォーム領域コード ファイルに、そのコントロールを返すプロパティを作成します。

 C# でプロパティを作成する方法の詳細については、「 [方法: 読み取り/書き込みプロパティを宣言して使用する」 &#40;C&#35; プログラミングガイド&#41;](/dotnet/csharp/programming-guide/classes-and-structs/how-to-declare-and-use-read-write-properties)を参照してください。

 Visual Basic でプロパティを作成する方法の詳細については、「 [方法: プロパティを作成する (Visual Basic)](/dotnet/visual-basic/programming-guide/language-features/procedures/how-to-create-a-property)」を参照してください。

## <a name="see-also"></a>関連項目
- [Outlook フォーム領域を作成するためのガイドライン](../vsto/guidelines-for-creating-outlook-form-regions.md)
- [チュートリアル: Outlook フォーム領域のデザイン](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [方法: フォーム領域を Outlook アドインプロジェクトに追加する](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
- [Outlook フォーム領域のカスタムアクション](../vsto/custom-actions-in-outlook-form-regions.md)
- [フォーム領域を Outlook メッセージクラスに関連付ける](../vsto/associating-a-form-region-with-an-outlook-message-class.md)
- [チュートリアル: Outlook でデザインされたフォーム領域をインポートする](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
- [方法: Outlook でフォーム領域が表示されないようにする](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)
- [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)
- [実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)
