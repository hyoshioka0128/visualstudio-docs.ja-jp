---
title: '方法: プログラムによって新しい Visio 図面を作成する'
description: プログラムを使用して新しい Microsoft Visio 図面ドキュメントを作成し、開いている Visio 図面のドキュメントコレクションに追加する方法について説明します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4b12b7e94109391928ad7c83387917e5934ae1c7
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825317"
---
# <a name="how-to-programmatically-create-new-visio-documents"></a>方法: プログラムによって新しい Visio 図面を作成する
  Microsoft Office Visio 描画図面を新規に作成する場合、開いている Visio 図面の `Microsoft.Office.Interop.Visio.Documents` コレクションにその図面を追加します。 これにより、`Microsoft.Office.Interop.Visio.Documents.Add` メソッドで新しい Visio 描画図面が作成されます。 詳細については、 [Microsoft.Office.Interop.Visio.Documents.Add](/office/vba/api/Visio.Documents.Add) メソッドの VBA リファレンス ドキュメントを参照してください。

## <a name="create-new-blank-documents"></a>新しい空のドキュメントを作成する

### <a name="to-create-a-new-document"></a>新しい図面を作成するには

- `Microsoft.Office.Interop.Visio.Documents.Add` メソッドを使用して、テンプレートに基づかない新しい空白の図面を作成します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet1":::

## <a name="create-documents-copied-from-existing-documents"></a>既存のドキュメントからコピーされたドキュメントを作成する
 `Microsoft.Office.Interop.Visio.Documents.Add` メソッドは、既存の Visio 図面をコピーして新しい図面を作成できます。 図のファイル名と完全修飾パスを指定する必要があります。

### <a name="to-create-a-new-document-that-is-copied-from-an-existing-document"></a>既存の図面をコピーして新しい図面を作成するには

- `Microsoft.Office.Interop.Visio.Documents.Add` メソッドを呼び出して、Visio 図面のパスを指定します。

:::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet2":::
:::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet2":::

## <a name="create-stencils-copied-from-existing-stencils"></a>既存のステンシルからコピーされたステンシルを作成する
 [Microsoft.Office.Interop.Visio.Documents.Add](/office/vba/api/Visio.Documents.Add) メソッドは、既存の Visio ステンシルをコピーして新しいステンシルを作成できます。 ステンシルのファイル名と完全修飾パスを指定する必要があります。

### <a name="to-create-a-new-stencil-that-is-copied-from-an-existing-stencil"></a>既存のステンシルをコピーして新しいステンシルを作成するには

- `Microsoft.Office.Interop.Visio.Documents.Add` メソッドを呼び出して、ステンシルのパスを指定します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet3":::

## <a name="create-documents-based-on-existing-templates"></a>既存のテンプレートに基づいてドキュメントを作成する
 メソッドは、 `Microsoft.Office.Interop.Visio.Documents.Add` 既存の Visio テンプレート ( *.vst* ファイル) に基づく新しいドキュメント ( *.vsd* ファイル) を作成できます。 このメソッドは、テンプレート ワークスペースの一部である、ステンシル、スタイル、および設定をコピーします。 テンプレートのファイル名と完全修飾パスを指定する必要があります。

### <a name="to-create-a-new-document-that-is-based-on-an-existing-template"></a>既存のテンプレートに基づいて新しい図面を作成するには

- `Microsoft.Office.Interop.Visio.Documents.Add` メソッドを呼び出して、テンプレートのパスを指定します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet4":::

## <a name="compile-the-code"></a>コードのコンパイル
 このコード例で必要な要素は次のとおりです。

- という名前の Visio 図面は、 `myDrawing.vsd` `Test` *[マイドキュメント* ] フォルダー (windows XP 以前の場合) または [ *ドキュメント* ] フォルダー (windows Vista の場合) のという名前のディレクトリに配置する必要があります。

- という名前の Visio 図面は、 `myStencil.vss` `Test` *[マイドキュメント* ] フォルダー (windows XP 以前の場合) または [ *ドキュメント* ] フォルダー (windows Vista の場合) のという名前のディレクトリに配置する必要があります。

- という名前の Visio 図面は、 `myTemplate.vst` `Test` *[マイドキュメント* ] フォルダー (windows XP 以前の場合) または [ *ドキュメント* ] フォルダー (windows Vista の場合) のという名前のディレクトリに配置する必要があります。

## <a name="see-also"></a>関連項目
- [Visio ソリューション](../vsto/visio-solutions.md)
- [Visio オブジェクトモデルの概要](../vsto/visio-object-model-overview.md)
- [方法: プログラムによって Visio 図面を開く](../vsto/how-to-programmatically-open-visio-documents.md)
- [方法: プログラムによって Visio 図面を閉じる](../vsto/how-to-programmatically-close-visio-documents.md)
- [方法: プログラムによって Visio 図面を保存する](../vsto/how-to-programmatically-save-visio-documents.md)
- [方法: プログラムによって Visio 図面を印刷する](../vsto/how-to-programmatically-print-visio-documents.md)
