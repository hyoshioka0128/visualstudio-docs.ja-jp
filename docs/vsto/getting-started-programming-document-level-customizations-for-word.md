---
title: Word 用ドキュメント レベル カスタマイズのプログラミングのスタート ガイド
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word solutions in Visual Studio
- Word projects [Office development in Visual Studio], getting started
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2b2872ca6496444cbb3878dc39800a8661400a76
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62971798"
---
# <a name="get-started-programming-document-level-customizations-for-word"></a>Word 用ドキュメント レベル カスタマイズのプログラミングのスタート ガイド
  ここでは、Visual Studio を使用して Microsoft Office Word 向けのドキュメント レベルのカスタマイズを作成し始めるために必要な事柄を説明します。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

## <a name="understand-how-document-level-customizations-for-word-work"></a>Word のドキュメント レベルのカスタマイズの作用についての理解
 作成する各 Word のカスタマイズは、単一の文書に基づいたものになります。 カスタマイズの使用を開始するには、エンドユーザーがドキュメントを開くかまたは Word テンプレートからドキュメントを作成します。 たとえば特定の領域にカーソルを移動したり、ボタンやメニュー項目をクリックしたりするなどのドキュメントでのイベントにより、アセンブリ内でイベント処理メソッドを呼び出すことができます。 ドキュメントが閉じられると、カスタマイズにより提供された機能は Word で使用できなくなります。
 
 詳細については、「[ドキュメント レベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)」を参照してください。

## <a name="create-document-level-projects-for-word"></a>Word 用のドキュメント レベル プロジェクトの作成
 Word 用のドキュメント レベルのカスタマイズを作成するには、**新しいプロジェクト** ダイアログ ボックスの中の Word 文書または Word テンプレート プロジェクト テンプレートを使用します。 これらのテンプレートには必要なアセンブリ参照とプロジェクト ファイルが含まれています。

 Word 用のドキュメント レベルのプロジェクトを作成する方法の詳細については、「[Visual Studio で Office プロジェクトを作成する方法](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。 プロジェクト テンプレートの詳細については、「[Office プロジェクト テンプレートの概要](../vsto/office-project-templates-overview.md)」を参照してください。

## <a name="program-word-documents-by-using-host-items-host-controls"></a>ホスト項目とホスト コントロールを使用した Word 文書のプログラミング
 *ホスト項目*と*ホスト コントロール*はドキュメント レベルのカスタマイズのプログラミング モデルを提供するクラスです。

 ホスト項目は、コードのエントリ ポイントを提供し、ホスト コントロールや Windows フォーム コントロールのコンテナーの役割を果たすこともできます。 Word 用のドキュメント レベルのプロジェクトでは、ホスト項目は `ThisDocument`クラスで表されます。

 ホスト コントロールは、コンテンツ コントロール、ブックマーク、および XML ノードなど、ネイティブな Word オブジェクトに基づいています。 ホスト コントロールは、ネイティブな Word オブジェクトと同様の機能を提供し、新しいイベント、デザイナー サポート、およびデータ バインディング機能も備えています。 プロジェクト コードでは、Word オブジェクト モデル内を移動することがなくコード内で直接特定のオブジェクトを参照しやすく、IntelliSense で最上位のオブジェクトとして表示されます。

 詳細については、次のトピックを参照してください。

- [ドキュメント レベルのカスタマイズのプログラミング](../vsto/programming-document-level-customizations.md)

- [拡張オブジェクトを使用した Word の自動化](../vsto/automating-word-by-using-extended-objects.md)

- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)

## <a name="customize-the-user-interface-of-word"></a>Word のユーザー インターフェイスのカスタマイズ
 ほとんどの Microsoft Office ソリューションは、Office アプリケーションのユーザー インターフェイス (UI) を変更して、ユーザーがソリューションと対話するためのなんらかの方法を提供します。 ドキュメント レベルのカスタマイズを使用して Word の UI を変更する方法はたくさんあります。 たとえば、コントロールは、リボンを追加することができ、操作ウィンドウを表示することができます。 詳細については、「[Office UI のカスタマイズ](../vsto/office-ui-customization.md)」を参照してください。

 Visual Studio で直接プロジェクトに関連付けられているドキュメントを開くこともできます。 文書を Visual Studio で開いているときは、Word のユーザー インターフェイスを使用して、ドキュメントを変更できます。 デザイン サーフェイスとしてそのドキュメントを使用し、それにコントロールをドラッグすることもできます。 詳細については、「[Visual Studio 環境における Office プロジェクト](../vsto/office-projects-in-the-visual-studio-environment.md)」を参照してください。

## <a name="bind-controls-to-data"></a>データ コントロールのバインド
 コンテンツ コントロールと<xref:Microsoft.Office.Tools.Word.Bookmark> コントロールは、**データソース** ウィンドウからドラッグできるコントロールのリストにあります。 この方法でコンテンツ コントロールやブックマークを追加すると、それらはウィンドウを使用して設定したデータ ソースに自動的にバインドされます。 コードを記述しなくても、データベース、サービス、およびビジネス オブジェクトからデータを表示できます。 詳細については、「[Office ソリューションでのコントロールへのデータのバインド](../vsto/binding-data-to-controls-in-office-solutions.md)」を参照してください。

## <a name="next-steps"></a>次の手順
 Word 用のドキュメント レベルのカスタマイズを作成する方法については、「[チュートリアル:最初の Word 用ドキュメント レベルのカスタマイズの作成](../vsto/walkthrough-creating-your-first-document-level-customization-for-word.md)」を参照してください。 このチュートリアルでは、Visual Studio と Word ドキュメント レベルのカスタマイズのプログラミング モデルでの Office 開発ツールについて説明します。

 Word プロジェクトでの一般的なタスクを解説しているトピックの一覧については、「[Office プログラミングでの一般的なタスク](../vsto/common-tasks-in-office-programming.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio での Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [ドキュメント レベルのカスタマイズのプログラミング](../vsto/programming-document-level-customizations.md)
- [Word ソリューション](../vsto/word-solutions.md)
- [チュートリアル: 最初の Word 用ドキュメント レベルのカスタマイズの作成](../vsto/walkthrough-creating-your-first-document-level-customization-for-word.md)
- [Word を使用したチュートリアル](../vsto/walkthroughs-using-word.md)
- [Word オブジェクト モデルの概要](../vsto/word-object-model-overview.md)
- [Office ソリューションにおけるコードの記述](../vsto/writing-code-in-office-solutions.md)
