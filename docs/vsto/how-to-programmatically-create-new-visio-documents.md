---
title: '方法: プログラムによって新しい Visio 図面を作成する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visio [Office development in Visual Studio], creating Visio documents
- documents [Office development in Visual Studio], creating Visio documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 171ad93caf6b5c13d000073a0d7f7e82282b9b4a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541532"
---
# <a name="how-to-programmatically-create-new-visio-documents"></a>方法: プログラムによって新しい Visio 図面を作成する
  Microsoft Office Visio 描画図面を新規に作成する場合、開いている Visio 図面の `Microsoft.Office.Interop.Visio.Documents` コレクションにその図面を追加します。 これにより、`Microsoft.Office.Interop.Visio.Documents.Add` メソッドで新しい Visio 描画図面が作成されます。 詳細については、 [Microsoft.Office.Interop.Visio.Documents.Add](/office/vba/api/Visio.Documents.Add) メソッドの VBA リファレンス ドキュメントを参照してください。

## <a name="create-new-blank-documents"></a>新しい空のドキュメントを作成する

### <a name="to-create-a-new-document"></a>新しい図面を作成するには

- `Microsoft.Office.Interop.Visio.Documents.Add` メソッドを使用して、テンプレートに基づかない新しい空白の図面を作成します。

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#1](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#1)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#1](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#1)]

## <a name="create-documents-copied-from-existing-documents"></a>既存のドキュメントからコピーされたドキュメントを作成する
 `Microsoft.Office.Interop.Visio.Documents.Add` メソッドは、既存の Visio 図面をコピーして新しい図面を作成できます。 図のファイル名と完全修飾パスを指定する必要があります。

### <a name="to-create-a-new-document-that-is-copied-from-an-existing-document"></a>既存の図面をコピーして新しい図面を作成するには

- `Microsoft.Office.Interop.Visio.Documents.Add` メソッドを呼び出して、Visio 図面のパスを指定します。

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#2](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#2)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#2](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#2)]

## <a name="create-stencils-copied-from-existing-stencils"></a>既存のステンシルからコピーされたステンシルを作成する
 [Microsoft.Office.Interop.Visio.Documents.Add](/office/vba/api/Visio.Documents.Add) メソッドは、既存の Visio ステンシルをコピーして新しいステンシルを作成できます。 ステンシルのファイル名と完全修飾パスを指定する必要があります。

### <a name="to-create-a-new-stencil-that-is-copied-from-an-existing-stencil"></a>既存のステンシルをコピーして新しいステンシルを作成するには

- `Microsoft.Office.Interop.Visio.Documents.Add` メソッドを呼び出して、ステンシルのパスを指定します。

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#3](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#3)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#3](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#3)]

## <a name="create-documents-based-on-existing-templates"></a>既存のテンプレートに基づいてドキュメントを作成する
 メソッドは、 `Microsoft.Office.Interop.Visio.Documents.Add` 既存の Visio テンプレート ( *.vst*ファイル) に基づく新しいドキュメント ( *.vsd*ファイル) を作成できます。 このメソッドは、テンプレート ワークスペースの一部である、ステンシル、スタイル、および設定をコピーします。 テンプレートのファイル名と完全修飾パスを指定する必要があります。

### <a name="to-create-a-new-document-that-is-based-on-an-existing-template"></a>既存のテンプレートに基づいて新しい図面を作成するには

- `Microsoft.Office.Interop.Visio.Documents.Add` メソッドを呼び出して、テンプレートのパスを指定します。

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#4](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#4)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#4](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#4)]

## <a name="compile-the-code"></a>コードのコンパイル
 このコード例で必要な要素は次のとおりです。

- という名前の Visio 図面は、 `myDrawing.vsd` `Test` *[マイドキュメント*] フォルダー (windows XP 以前の場合) または [*ドキュメント*] フォルダー (windows Vista の場合) のという名前のディレクトリに配置する必要があります。

- という名前の Visio 図面は、 `myStencil.vss` `Test` *[マイドキュメント*] フォルダー (windows XP 以前の場合) または [*ドキュメント*] フォルダー (windows Vista の場合) のという名前のディレクトリに配置する必要があります。

- という名前の Visio 図面は、 `myTemplate.vst` `Test` *[マイドキュメント*] フォルダー (windows XP 以前の場合) または [*ドキュメント*] フォルダー (windows Vista の場合) のという名前のディレクトリに配置する必要があります。

## <a name="see-also"></a>関連項目
- [Visio ソリューション](../vsto/visio-solutions.md)
- [Visio オブジェクトモデルの概要](../vsto/visio-object-model-overview.md)
- [方法: プログラムによって Visio 図面を開く](../vsto/how-to-programmatically-open-visio-documents.md)
- [方法: プログラムによって Visio 図面を閉じる](../vsto/how-to-programmatically-close-visio-documents.md)
- [方法: プログラムによって Visio 図面を保存する](../vsto/how-to-programmatically-save-visio-documents.md)
- [方法: プログラムによって Visio 図面を印刷する](../vsto/how-to-programmatically-print-visio-documents.md)
