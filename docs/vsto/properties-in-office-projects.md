---
title: Office プロジェクトのプロパティ
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Trust Assemblies Location property
- Cache in Document property
- properties [Office development in Visual Studio]
- Namespace for Host Item property
- Office projects [Office development in Visual Studio], properties
- projects [Office development in Visual Studio], properties
- Value2 property
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9fc2a0774206eac0c9295a425d81555ffdd3cac8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62561367"
---
# <a name="properties-in-office-projects"></a>Office プロジェクトのプロパティ
  Visual Studio で Office プロジェクトに使用できる重要なプロパティがいくつかあります。 これらのプロパティには [ **プロパティ** ] ウィンドウでアクセスできます。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="namespace-for-host-item"></a>ホスト項目の名前空間
 ホスト項目 **の名前空間** プロパティを使用して、Visual C# プロジェクトのホスト項目クラス ( `ThisAddIn` 、、 `ThisWorkbook` またはクラスなど) の名前空間を変更し `ThisDocument` ます。 このプロパティは、ドキュメントレベルのプロジェクト ( *ExcelWorkbook1.xlsx*や*WordDocument1.docx*など) でドキュメントノードを選択したとき、または**ソリューションエクスプローラー**で VSTO アドインプロジェクト (Excel や Word など) のアプリケーションノードを選択したときに、[**プロパティ**] ウィンドウに表示されます。

 Visual C# Office プロジェクトを作成すると、プロジェクトの名前に基づいてホスト項目に名前空間が与えられます。 コード ファイルを直接編集するのではなく、[ **ホスト項目の名前空間** ] プロパティを使用して名前空間を変更することをお勧めします。 このプロパティを使用すると、名前空間は、生成されるコード ファイル (非表示) だけでなく、表示されるコード ファイル内でも変更されます。

## <a name="cacheindocument"></a>CacheInDocument
 **CacheInDocument** プロパティは、Visual Studio デザイナーで **のインスタンスを選択すると、ドキュメント レベルのプロジェクトの [** プロパティ <xref:System.Data.DataSet> ] ウィンドウに表示されます。 パブリック メンバーだけがキャッシュされます。 **をキャッシュする場合は、[** Modifiers **] プロパティを [** Public <xref:System.Data.DataSet>] に設定してください。

 このプロパティはブール値を受け取ります。

- ドキュメント内のデータセットをキャッシュする場合は、 **true** を選択します。

- ドキュメントのデータセットをキャッシュしない場合は、 **false** を選択します。

  データのキャッシュの詳細については、「 [ドキュメントレベルのカスタマイズでのキャッシュデータ](../vsto/cached-data-in-document-level-customizations.md)」を参照してください。

## <a name="value2"></a>Value2
 **Value2** プロパティは、Excel ブック プロジェクトまたはテンプレート プロジェクトにのみ使用できます。 ワークシート デザイナーで **コントロールを選択すると、[** プロパティ **] ウィンドウの** Databindings <xref:Microsoft.Office.Tools.Excel.NamedRange> プロパティの下に表示されます。

 **の** プロパティをデータ ソースのフィールドにバインドするには、[ **プロパティ** ] ウィンドウの <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> Value2 <xref:Microsoft.Office.Tools.Excel.NamedRange> プロパティを使用します。

## <a name="see-also"></a>こちらもご覧ください
- [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)
- [Office プロジェクトテンプレートの概要](../vsto/office-project-templates-overview.md)
- [Office プロジェクトのイベント](../vsto/events-in-office-projects.md)
