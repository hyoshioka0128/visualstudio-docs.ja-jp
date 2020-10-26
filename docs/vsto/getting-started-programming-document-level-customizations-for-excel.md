---
title: 'Excel: ドキュメントレベルのカスタマイズのプログラミングを開始する'
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "66402159"
---
# <a name="get-started-programming-document-level-customizations-for-excel"></a>Excel のドキュメントレベルのカスタマイズのプログラミングの概要
  Visual Studio を使用して Microsoft Office Excel のドキュメントレベルのカスタマイズの作成を開始するだけの場合は、次のことを理解しておく必要があります。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

## <a name="understand-how-document-level-customizations-for-excel-work"></a>Excel の作業におけるドキュメントレベルのカスタマイズについて理解する
 Excel のドキュメントレベルのカスタマイズは、1つのブックに基づいています。 カスタマイズの使用を開始するには、エンドユーザーがブックを開くか、Excel テンプレートからブックを作成します。 たとえば、セルへの入力や、ボタンやメニュー項目のクリックなど、ブック内のイベントでは、アセンブリ内のイベント処理メソッドを呼び出すことができます。 ブックを閉じると、カスタマイズによって提供される機能が Excel で使用できなくなります。これらの機能は、それを含むドキュメント内でのみ使用できます。

 詳細については、「 [ドキュメントレベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)」を参照してください。

## <a name="create-document-level-projects-for-excel"></a>Excel のドキュメントレベルのプロジェクトを作成する
 Excel のドキュメントレベルのカスタマイズを作成するには、[ **新しいプロジェクト** ] ダイアログボックスで excel ブックまたは excel テンプレートのプロジェクトテンプレートを使用します。 これらのテンプレートには必要なアセンブリ参照とプロジェクト ファイルが含まれています。

 Excel のドキュメントレベルのプロジェクトを作成する方法の詳細については、「 [方法: Visual Studio で Office プロジェクトを作成](../vsto/how-to-create-office-projects-in-visual-studio.md)する」を参照してください。 プロジェクトテンプレートの詳細については、「 [Office プロジェクトテンプレートの概要](../vsto/office-project-templates-overview.md)」を参照してください。

## <a name="program-excel-workbooks-by-using-host-items-and-host-controls"></a>ホスト項目とホストコントロールを使用して Excel ブックをプログラミングする
 *ホスト項目* と *ホストコントロール* は、Visual Studio を使用して作成されたドキュメントレベルのカスタマイズのプログラミングモデルを提供するクラスです。

 ホスト項目はコードのエントリポイントを提供し、ホストコントロールおよび Windows フォームコントロールのコンテナーとしても機能します。 Excel のドキュメントレベルのプロジェクトでは、これらのホスト項目は、、、、およびの各クラスによって表され `ThisWorkbook` `Sheet1` `Sheet2` `Sheet3` ます。

 ホストコントロールは、リストオブジェクトや範囲など、ネイティブの Excel オブジェクトに基づいています。 ホストコントロールは、ネイティブの Excel オブジェクトと同様の機能を提供しますが、新しいイベント、デザイナーサポート、およびデータバインディング機能も備えています。 これらのオブジェクトは、プロジェクトコードと IntelliSense ではファーストクラスのオブジェクトとして表示されるので、Excel オブジェクトモデルに移動しなくても、コード内で直接特定のオブジェクトを参照することが簡単になります。

 詳細については、次のトピックを参照してください。

- [プログラムドキュメントレベルのカスタマイズ](../vsto/programming-document-level-customizations.md)

- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)

- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)

## <a name="customize-the-user-interface-of-excel"></a>Excel のユーザーインターフェイスをカスタマイズする
 ほとんどの Microsoft Office ソリューションでは、ユーザーがソリューションと対話する手段を提供するために、Office アプリケーションのユーザーインターフェイス (UI) を変更します。 ドキュメントレベルのカスタマイズを使用して Excel の UI を変更するには、さまざまな方法があります。 たとえば、リボンにコントロールを追加したり、操作ウィンドウを表示したりすることができます。 詳細については、「 [OFFICE UI のカスタマイズ](../vsto/office-ui-customization.md)」を参照してください。

 また、プロジェクトに関連付けられているブックを Visual Studio で直接開くこともできます。 ブックが Visual Studio で開かれている場合は、Excel ユーザーインターフェイスを使用してブックを変更できます。 ブックをデザイン画面として使用することもできます。これにより、コントロールをワークシートにドラッグできるようになります。 詳細については、「 [Visual Studio 環境における Office プロジェクト](../vsto/office-projects-in-the-visual-studio-environment.md)」を参照してください。

## <a name="use-data-binding"></a>データバインディングを使用する
 ホストコントロールは、[ **データソース** ] ウィンドウからドラッグできるコントロールの一覧にもあります。 この方法でホストコントロールを追加すると、ウィンドウを使用して設定したデータソースに自動的にバインドされます。 コードを記述しなくても、データベース、web サービス、およびビジネスオブジェクトのデータを表示できます。 詳細については、「 [データを Office ソリューションのコントロールにバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)」を参照してください。

## <a name="next-steps"></a>次のステップ
 Excel 用のドキュメントレベルのカスタマイズを作成する方法については、「 [チュートリアル: 初めての excel 用ドキュメントレベルのカスタマイズを作成](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md)する」を参照してください。 このチュートリアルでは、Visual Studio の Office 開発ツールと Excel ドキュメントレベルのカスタマイズのプログラミングモデルについて説明します。

 Excel プロジェクトの一般的なタスクについて説明するトピックの一覧については、「 [Office プログラミングにおける一般的なタスク](../vsto/common-tasks-in-office-programming.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [プログラムドキュメントレベルのカスタマイズ](../vsto/programming-document-level-customizations.md)
- [Excel ソリューション](../vsto/excel-solutions.md)
- [チュートリアル: 初めての Excel 用ドキュメントレベルのカスタマイズの作成](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md)
- [Excel を使用したチュートリアル](../vsto/walkthroughs-using-excel.md)
- [Excel オブジェクトモデルの概要](../vsto/excel-object-model-overview.md)
- [Office ソリューションでコードを記述する](../vsto/writing-code-in-office-solutions.md)
