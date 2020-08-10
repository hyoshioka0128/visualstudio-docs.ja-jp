---
title: Office プロジェクト内のオブジェクトへのグローバルアクセス
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ThisDocument_Shutdown
- ThisDocument_Startup
- Globals class, object global access
- worksheets [Office development in Visual Studio], global access
- documents [Office development in Visual Studio], global access
- event handlers [Office development in Visual Studio]
- ThisWorkbook_Startup
- application-level addins [Office development in Visual Studio]
- addins [Office development in Visual Studio], events
- workbooks [Office development in Visual Studio], global access
- ThisWorkbook_Shutdown
- document-level customizations [Office development in Visual Studio]
- Startup event
- Shutdown event
- projects [Office development in Visual Studio], global access
- Office documents [Office development in Visual Studio, global access
- ThisAddin_Startup
- events [Office development in Visual Studio]
- ThisAddIn_Shutdown
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f76a2e74315980764a2cdffe67af4403552de7fe
ms.sourcegitcommit: d293c0e3e9cc71bd4117b6dfd22990d52964addc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/10/2020
ms.locfileid: "88041052"
---
# <a name="global-access-to-objects-in-office-projects"></a>Office プロジェクト内のオブジェクトへのグローバルアクセス
  Office プロジェクトを作成すると、Visual Studio は自動的に `Globals` という名前のクラスをプロジェクトに生成します。 `Globals` クラスを使用して、プロジェクト内の任意のコードから実行時に異なる複数のプロジェクト項目にアクセスすることができます。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="how-to-use-the-globals-class"></a>Globals クラスの使用方法
 `Globals` はプロジェクト内の特定の項目への参照を保持する静的クラスです。 `Globals` クラスを使用することで、実行時にプロジェクト内の任意のコードから次の項目へとアクセスすることができます。

- Excel ブックまたはテンプレート プロジェクトの `ThisWorkbook` および `Sheet`*n* クラス。 これらのオブジェクトは、 `Globals.ThisWorkbook` および `Sheet`*n* プロパティを使用してアクセスすることができます。

- Word 文書またはテンプレート プロジェクトの `ThisDocument` クラス。 このオブジェクトには、 `Globals.ThisDocument` プロパティを使用してアクセスすることができます。

- `ThisAddIn`VSTO アドインプロジェクトのクラス。 このオブジェクトには、 `Globals.ThisAddIn` プロパティを使用してアクセスすることができます。

- リボン デザイナーを使用してカスタマイズした、プロジェクト内のすべてのリボン。 リボンには、 `Globals.Ribbons` プロパティを使用してアクセスすることができます。 詳細については、「[実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)」を参照してください。

- Outlook VSTO アドイン プロジェクトのすべての Outlook フォーム領域。 フォーム領域には、 `Globals.FormRegions` プロパティを使用してアクセスすることができます。 詳細については、「実行時の[フォーム領域へのアクセス](../vsto/accessing-a-form-region-at-run-time.md)」を参照してください。

- [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] または [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]をターゲットとするプロジェクトで実行時にリボン コントロールおよびホスト項目を作成できるようにするファクトリ オブジェクト。 このオブジェクトには、 `Globals.Factory` プロパティを使用してアクセスすることができます。 このオブジェクトは、次のいずれかのインターフェイスを実装するクラスのインスタンスです。

  - [Microsoft. Office. ツールファクトリ](xref:Microsoft.Office.Tools.Factory)

  - [Microsoft. Office. Excel. Factory](xref:Microsoft.Office.Tools.Excel.Factory)

  - [Microsoft. Office. Outlook. Factory](xref:Microsoft.Office.Tools.Outlook.Factory)

  - [Microsoft. Office. Word. Factory](xref:Microsoft.Office.Tools.Word.Factory)

  たとえば、 `Globals.Sheet1` プロパティを使用すると、Excel のドキュメントレベルのプロジェクトの操作ウィンドウでユーザーがボタンをクリックした場合に <xref:Microsoft.Office.Tools.Excel.NamedRange> の `Sheet1` コントロールにテキストを挿入することができます。

  [!code-vb[Trin_VstcoreProgramming#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/Sheet1.vb#1)]
  [!code-csharp[Trin_VstcoreProgramming#1](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/Sheet1.cs#1)]

 `Globals`ドキュメントまたは VSTO アドインが初期化される前にクラスを使用しようとするコードは、実行時の例外をスローする可能性があります。 たとえば、クラス レベルの変数の宣言が `Globals` を使用することで失敗する場合があります。これは、宣言されたオブジェクトがインスタンス化される前に、 `Globals` クラスがすべてのホスト項目への参照を使用して初期化されない可能性があるためです。

> [!NOTE]
> `Globals` クラスは設計時に初期化されることはありませんが、コントロールのインスタンスがデザイナーによって作成されます。 これは、ユーザーコントロールクラス内からクラスのプロパティを使用するユーザーコントロールを作成する場合 `Globals` 、返されたオブジェクトを使用する前に、プロパティが**null**を返すかどうかを確認する必要があることを意味します。

## <a name="see-also"></a>関連項目
- [実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)
- [実行時のフォーム領域へのアクセス](../vsto/accessing-a-form-region-at-run-time.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ドキュメントホスト項目](../vsto/document-host-item.md)
- [ブックホスト項目](../vsto/workbook-host-item.md)
- [ワークシートホスト項目](../vsto/worksheet-host-item.md)
- [Office ソリューションでコードを記述する](../vsto/writing-code-in-office-solutions.md)
