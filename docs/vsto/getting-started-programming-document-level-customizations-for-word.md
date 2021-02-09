---
title: Word のドキュメントレベルのカスタマイズのプログラミングの概要
description: Visual Studio を使用して Microsoft Office Word のドキュメントレベルのカスタマイズの作成を開始するために知っておく必要があることについて説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ff19fd84b66b9d31ed806589044775e006ef7096
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860660"
---
# <a name="get-started-programming-document-level-customizations-for-word"></a>Word のドキュメントレベルのカスタマイズのプログラミングの概要
  Visual Studio を使用して Microsoft Office Word のドキュメントレベルのカスタマイズの作成を開始するだけの場合は、次のことを理解しておく必要があります。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

## <a name="understand-how-document-level-customizations-for-word-work"></a>Word の作業に関するドキュメントレベルのカスタマイズについて理解する
 作成する各単語のカスタマイズは、1つのドキュメントに基づいています。 カスタマイズの使用を開始するには、エンドユーザーがドキュメントを開くか、Word テンプレートからドキュメントを作成します。 ドキュメント内のイベント。たとえば、カーソルを特定の領域に移動したり、ボタンやメニュー項目をクリックしたりすると、アセンブリ内のイベント処理メソッドを呼び出すことができます。 ドキュメントを閉じると、カスタマイズによって提供される機能が Word で使用できなくなります。

 詳細については、「 [ドキュメントレベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)」を参照してください。

## <a name="create-document-level-projects-for-word"></a>Word のドキュメントレベルのプロジェクトを作成する
 Word のドキュメントレベルのカスタマイズを作成するには、[ **新しいプロジェクト** ] ダイアログボックスで、word 文書または word テンプレートのプロジェクトテンプレートを使用します。 これらのテンプレートには必要なアセンブリ参照とプロジェクト ファイルが含まれています。

 Word のドキュメントレベルのプロジェクトを作成する方法の詳細については、「 [方法: Visual Studio で Office プロジェクトを作成](../vsto/how-to-create-office-projects-in-visual-studio.md)する」を参照してください。 プロジェクトテンプレートの詳細については、「 [Office プロジェクトテンプレートの概要](../vsto/office-project-templates-overview.md)」を参照してください。

## <a name="program-word-documents-by-using-host-items-host-controls"></a>ホスト項目のホストコントロールを使用して Word 文書をプログラミングする
 *ホスト項目* と *ホストコントロール* は、ドキュメントレベルのカスタマイズのプログラミングモデルを提供するクラスです。

 ホスト項目はコードのエントリポイントを提供し、ホストコントロールおよび Windows フォームコントロールのコンテナーとしても機能します。 Word のドキュメントレベルのプロジェクトでは、ホスト項目はクラスによって表され `ThisDocument` ます。

 ホストコントロールは、コンテンツコントロール、ブックマーク、XML ノードなどのネイティブな Word オブジェクトに基づいています。 ホストコントロールは、ネイティブ Word オブジェクトと同様の機能を提供しますが、新しいイベント、デザイナーサポート、およびデータバインディング機能も備えています。 これらのオブジェクトは、プロジェクトコードと IntelliSense ではファーストクラスのオブジェクトとして表示されるので、Word オブジェクトモデルを操作することなく、コード内で直接特定のオブジェクトを参照することが簡単になります。

 詳細については、次のトピックを参照してください。

- [プログラムドキュメントレベルのカスタマイズ](../vsto/programming-document-level-customizations.md)

- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)

- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)

## <a name="customize-the-user-interface-of-word"></a>Word のユーザーインターフェイスをカスタマイズする
 ほとんどの Microsoft Office ソリューションでは、ユーザーがソリューションと対話する手段を提供するために、Office アプリケーションのユーザーインターフェイス (UI) を変更します。 ドキュメントレベルのカスタマイズを使用して Word の UI を変更するには、さまざまな方法があります。 たとえば、リボンにコントロールを追加して、操作ウィンドウを表示することができます。 詳細については、「 [OFFICE UI のカスタマイズ](../vsto/office-ui-customization.md)」を参照してください。

 また、プロジェクトに関連付けられているドキュメントを Visual Studio で直接開くこともできます。 ドキュメントが Visual Studio で開かれている場合は、Word のユーザーインターフェイスを使用してドキュメントを変更できます。 ドキュメントをデザイン画面として使用することもできます。これにより、コントロールをコントロールにドラッグできるようになります。 詳細については、「 [Visual Studio 環境における Office プロジェクト](../vsto/office-projects-in-the-visual-studio-environment.md)」を参照してください。

## <a name="bind-controls-to-data"></a>コントロールをデータにバインドする
 コンテンツコントロールとコントロールは、 <xref:Microsoft.Office.Tools.Word.Bookmark> [ **データソース** ] ウィンドウからドラッグできるコントロールのリストに含まれています。 この方法でコンテンツコントロールとブックマークを追加すると、ウィンドウを使用して設定したデータソースに自動的にバインドされます。 コードを記述しなくても、データベース、サービス、およびビジネスオブジェクトのデータを表示できます。 詳細については、「 [データを Office ソリューションのコントロールにバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)」を参照してください。

## <a name="next-steps"></a>次の手順
 Word のドキュメントレベルのカスタマイズを作成する方法については、「 [チュートリアル: word の最初のドキュメントレベルのカスタマイズを作成](../vsto/walkthrough-creating-your-first-document-level-customization-for-word.md)する」を参照してください。 このチュートリアルでは、Visual Studio の Office 開発ツールと Word ドキュメントレベルのカスタマイズのプログラミングモデルについて説明します。

 Word プロジェクトの一般的なタスクについて説明するトピックの一覧については、「 [Office プログラミングにおける一般的なタスク](../vsto/common-tasks-in-office-programming.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [プログラムドキュメントレベルのカスタマイズ](../vsto/programming-document-level-customizations.md)
- [Word ソリューション](../vsto/word-solutions.md)
- [チュートリアル: 初めての Word 用ドキュメントレベルのカスタマイズの作成](../vsto/walkthrough-creating-your-first-document-level-customization-for-word.md)
- [Word を使用したチュートリアル](../vsto/walkthroughs-using-word.md)
- [Word オブジェクトモデルの概要](../vsto/word-object-model-overview.md)
- [Office ソリューションでコードを記述する](../vsto/writing-code-in-office-solutions.md)
