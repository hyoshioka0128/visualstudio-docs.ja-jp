---
title: Excel:ドキュメント レベルのカスタマイズのプログラミングを開始します。
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel solutions in Visual Studio
- Excel projects [Office development in Visual Studio], getting started
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2c1ff264eb1a4ca7afdc424cef7edf15bae06554
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2019
ms.locfileid: "66402159"
---
# <a name="get-started-programming-document-level-customizations-for-excel"></a>Excel 用ドキュメント レベル カスタマイズのプログラミングのスタート ガイド
  Visual Studio を使用して Microsoft Office Excel のドキュメント レベルのカスタマイズを作成することを始めるには、次を知る必要があります。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

## <a name="understand-how-document-level-customizations-for-excel-work"></a>Excel のドキュメント レベルのカスタマイズがどのように働くかの理解
 Excel 用ドキュメント レベルのカスタマイズは、1 つのブックに基づいています。 カスタマイズの使用を開始するには、エンド ユーザーはブックを開くか、Excel テンプレートからブックを作成します。 たとえば、セルに入力する、ボタンおよびメニュー項目をクリックするといった、ブック内のイベントは、アセンブリ内のイベント処理メソッドを呼び出すことができます。 ブックが閉じられると、カスタマイズによって提供される機能は Excel では使用できず、それらが含まれているドキュメント内でのみ使用できます。

 詳細については、「[ドキュメント レベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)」を参照してください。

## <a name="create-document-level-projects-for-excel"></a>Excel 用ドキュメント レベルのプロジェクトの作成
 Excel 用ドキュメント レベルのカスタマイズを作成するには、 **[新しいプロジェクト]** ダイアログ ボックスで、Excel ブックまたは Excel テンプレート プロジェクト テンプレートを使用します。 これらのテンプレートには必要なアセンブリ参照とプロジェクト ファイルが含まれています。

 Excel 用ドキュメント レベルのプロジェクトを作成する方法の詳細については、「[Visual Studio で Office プロジェクトを作成する方法](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。 プロジェクト テンプレートの詳細については、「[Office プロジェクト テンプレートの概要](../vsto/office-project-templates-overview.md)」を参照してください。

## <a name="program-excel-workbooks-by-using-host-items-and-host-controls"></a>ホスト項目とホスト コントロールを使用した Excel ブックのプログラミング
 *ホスト項目*と*ホスト コントロール*は Visual Studio を使用して作成されたドキュメント レベル カスタマイズのプログラミング モデルを提供するクラスです。

 ホスト項目は、コードのエントリ ポイントを提供し、ホスト コントロールや Windows フォーム コントロールのコンテナーとしても機能できます。 Excel 用ドキュメント レベルのプロジェクトにおいて、これらのホスト項目は、`ThisWorkbook`、`Sheet1`、`Sheet2`、および `Sheet3` クラスとして表されます。

 ホスト コントロールは、リスト オブジェクトや範囲といったネイティブな Excel オブジェクトに基づいています。 ホスト コントロールは、ネイティブな Excel オブジェクトと同様の機能を提供し、新しいイベント、デザイナー サポート、およびデータ バインディング機能も備えています。 これにより、Excel オブジェクト モデルを操作することなくコード内で直接特定のオブジェクトを参照しやすく、プロジェクト コードおよび IntelliSense で最上位のオブジェクトとして表示されます。

 詳細については、次のトピックを参照してください。

- [ドキュメント レベルのカスタマイズのプログラミング](../vsto/programming-document-level-customizations.md)

- [拡張オブジェクトを使用した Excel の自動化](../vsto/automating-excel-by-using-extended-objects.md)

- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)

## <a name="customize-the-user-interface-of-excel"></a>Excel のユーザー インターフェイスのカスタマイズ
 ほとんどの Microsoft Office ソリューションは、Office アプリケーションのユーザー インターフェイス (UI) を変更して、ユーザーがソリューションと対話するためのなんらかの方法を提供します。 ドキュメント レベルのカスタマイズを使用して Excel の UI を変更する方法はたくさんあります。 たとえば、リボンにコントロールを追加したり、操作ウィンドウを表示したりすることが可能です。 詳細については、「[Office UI のカスタマイズ](../vsto/office-ui-customization.md)」を参照してください。

 Visual Studio で直接、プロジェクトに関連付けられているブックを開くこともできます。 ブックが Visual Studio で開かれていれば、Excel のユーザー インターフェイスを使用して、ブックを変更できます。 ブックをデザイン サーフェイスとして使用して、コントロールをワークシートにドラッグすることもできます。 詳細については、「[Visual Studio 環境における Office プロジェクト](../vsto/office-projects-in-the-visual-studio-environment.md)」を参照してください。

## <a name="use-data-binding"></a>データ バインディングの使用
 ホスト コントロールは、 **[データソース]** ウィンドウからドラッグできるコントロールのリストの中にもあります。 この方法でホスト コントロール追加すると、ウィンドウを使用して設定したデータ ソースに自動的にバインドされます。 コードを記述せずに、データベース、Web サービス、およびビジネス オブジェクトからデータを表示できます。 詳細については、「[Office ソリューションでのコントロールにデータをバインド](../vsto/binding-data-to-controls-in-office-solutions.md)」を参照してください。

## <a name="next-steps"></a>次の手順
 Excel 用ドキュメント レベルのカスタマイズを作成する方法については、「[チュートリアル:最初の Excel 用ドキュメント レベルのカスタマイズを作成する](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md)」を参照してください。 このチュートリアルでは、Visual Studio による Office 開発ツールと Excel のドキュメント レベルのカスタマイズのプログラミング モデルについて説明します。

 Excel プロジェクトで、一般的なタスクを解説しているトピックの一覧は、「[Office プログラミングにおける一般的なタスク](../vsto/common-tasks-in-office-programming.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio での Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [ドキュメント レベルのカスタマイズのプログラミング](../vsto/programming-document-level-customizations.md)
- [Excel ソリューション](../vsto/excel-solutions.md)
- [チュートリアル: 最初の Excel 用ドキュメント レベルのカスタマイズを作成します。](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md)
- [Excel を使用したチュートリアル](../vsto/walkthroughs-using-excel.md)
- [Excel オブジェクト モデルの概要](../vsto/excel-object-model-overview.md)
- [Office ソリューションにおけるコードの記述](../vsto/writing-code-in-office-solutions.md)
