---
title: リボンの概要
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- customizing the Ribbon, multiple Ribbons
- Ribbon [Office development in Visual Studio], about Ribbon
- toolbars [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio]
- Ribbon [Office development in Visual Studio], multiple Ribbons
- toolbars [Office development in Visual Studio]
- custom Ribbon, multiple Ribbons
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 668517705caa7ba6baef0b85305bf4470bc3b26b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72985613"
---
# <a name="ribbon-overview"></a>リボンの概要
  リボンは、関連するコマンドを簡単に見つけられるように整理する方法です。 コマンドは、リボン上のコントロールとして表示されます。 コントロールは、アプリケーションウィンドウの上端にある水平ストリップに沿って *グループ化* されます。 関連するグループは、タブに整理されます。

 以前のバージョンの Microsoft Office システムのメニューとツールバーを使用してアクセスされた機能のほとんどは、リボンを使用してアクセスできるようになりました。 詳細については、技術記事「 [2007 Microsoft Office システム用のユーザーインターフェイスの開発者向け概要](/previous-versions/office/developer/office-2007/aa338198(v=office.12))」を参照してください。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

## <a name="customize-the-microsoft-office-ribbon"></a>Microsoft Office リボンをカスタマイズする
 リボンをカスタマイズするには、次のいずれかのリボン項目を Office プロジェクトに追加します。

- **リボン (ビジュアルなデザイナー)**

- **リボン (XML)**

  たとえば、Excel のリボンをカスタマイズするには、Excel VSTO アドイン プロジェクトにリボン項目を追加します。

### <a name="ribbon-visual-designer-item"></a>リボン (ビジュアルデザイナー) 項目
 **リボン (ビジュアルデザイナー)** 項目には、カスタムリボンのデザインと開発を容易にする高度なツールが用意されています。 リボン **(ビジュアルデザイナー)** 項目を使用して、次の方法でリボンをカスタマイズします。

- カスタムタブまたは組み込みタブをリボンに追加します。

- カスタム タブまたは組み込みタブにカスタム グループを追加します。

  > [!NOTE]
  > 組み込みのタブまたはグループは、Microsoft Office アプリケーションのリボンに既に存在しています。 たとえば、[ **データ** ] タブは Excel の組み込みタブです。 **接続**グループは、[**データ**] タブの組み込みグループです。

- カスタム コントロールをカスタム グループに追加します。

- Backstage ビューにカスタム コントロールを追加します。

  リボン **(ビジュアルデザイナー)** 項目を使用してリボンをカスタマイズする方法の詳細については、「 [リボンデザイナー](../vsto/ribbon-designer.md)」を参照してください。

### <a name="ribbon-xml-item"></a>リボン (XML) 項目
 リボン **(ビジュアルデザイナー)** 項目でサポートされていない方法でリボンをカスタマイズする場合は、**リボン (XML)** 項目を使用します。 リボン **(XML)** 項目を使用して、次の方法でリボンをカスタマイズします。

- *組み込み*のグループをカスタムタブまたは組み込みタブに追加します。

- 組み込みコントロールをカスタム グループに追加します。

- カスタム コードを追加して、組み込みコントロールのイベント ハンドラーをオーバーライドします。

- クイック アクセス ツールバーをカスタマイズします。

- 修飾 ID を使用して、VSTO アドイン間でリボンのカスタマイズを共有します。

  リボン **(xml)** 項目を使用してリボンをカスタマイズする方法の詳細については、「 [リボン xml](../vsto/ribbon-xml.md)」を参照してください。

## <a name="export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml"></a>リボンデザイナーからリボン XML にリボンをエクスポートする
 リボンデザイナーを使用してリボンを作成し、リボン **(ビジュアルデザイナー)** 項目でサポートされていない方法でリボンをカスタマイズする場合は、リボンを XML にエクスポートします。

 Visual Studio では、リボン **(xml)** 項目が自動的に作成され、リボン XML ファイルに、リボン上の各コントロールの要素と属性が設定されます。

 リボンデザイナーの [ **プロパティ** ] ウィンドウに表示されるプロパティのすべてが、リボン XML ファイルに転送されるわけではありません。  たとえば、Visual Studio では、 **Image** または **Text** プロパティの値はエクスポートされません。 これは、コントロールのイメージを割り当てたり、コントロールのテキストを設定したりするには、エクスポートしたプロジェクトのリボン コード ファイルにコールバック メソッドを作成する必要があるためです。 Visual Studio で、エクスポート プロセスの一部としてコールバック メソッドが自動的に生成されることはありません。

 また、既定値から変更されていないプロパティ値は、結果として得られるリボン XML ファイルには含められません。

 リボンを XML にエクスポートする方法の詳細については、「方法: リボンをリボン [デザイナーからリボン xml にエクスポート](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)する」を参照してください。

### <a name="update-the-code"></a>コードを更新する
 新しいリボンコードファイルが **ソリューションエクスプローラー**に追加されます。 このファイルにはリボン XML クラスが含まれています。 ボタンのクリックなどのユーザー操作を処理するには、このクラスの `Ribbon Callbacks` 領域にコールバック メソッドを作成する必要があります。 イベント ハンドラーからこれらのコールバック メソッドにコードを移動し、リボン機能拡張 (RibbonX) プログラミング モデルで動作するようにコードを変更します。 詳細については、「 [Ribbon XML](../vsto/ribbon-xml.md)」を参照してください。

 さらに、`ThisAddIn`、`ThisWorkbook`、または `ThisDocument` のいずれかのクラスに、`CreateRibbonExtensibilityObject` メソッドをオーバーライドして Office アプリケーションにリボン XML クラスを返すコードを追加する必要もあります。

 詳細については、「 [Ribbon XML](../vsto/ribbon-xml.md)」を参照してください。

## <a name="add-multiple-ribbon-items-to-a-project"></a>複数のリボン項目をプロジェクトに追加する
 1 つのプロジェクトに複数のリボン項目を追加することができます。 これは、次の 2 つのタスクのいずれかを実行する場合に便利です。

- Outlook *インスペクター*用のリボンを作成します。 詳細については、「 [Outlook のリボンのカスタマイズ](../vsto/customizing-a-ribbon-for-outlook.md)」を参照してください。

    > [!NOTE]
    > インスペクターは、ユーザーが電子メール メッセージを作成するなど、特定のタスクを実行するときに表示されるウィンドウです。

- 実行時に表示するリボンを選択します。

### <a name="select-which-ribbons-to-display-at-run-time"></a>実行時に表示するリボンを選択する
 1つのプロジェクトに複数のリボンを含めることができるため、実行時に表示するリボンを選択できます。

 実行時に表示するリボンを選択するには、 `CreateRibbonExtensibilityObject` `ThisAddin` `ThisWorkbook` プロジェクトの、、またはクラスのメソッドをオーバーライド `ThisDocument` し、表示するリボンを返します。 次の例では、という名前のフィールドの値をチェック `myCondition` し、適切なリボンを返します。

> [!NOTE]
> この例で使用する構文は、 **リボン (ビジュアルデザイナー)** 項目を使用して作成されたリボンを返します。 **リボン (XML)** 項目を使用して作成されたリボンを返す構文は少し異なります。 **リボン (xml)** 項目を返す方法の詳細については、「[リボン xml](../vsto/ribbon-xml.md)」を参照してください。

 次のコードを追加します。

 [!code-vb[Trin_Ribbon_Choose_Ribbon#1](../vsto/codesnippet/VisualBasic/trin_Ribbon_choose_Ribbon_4/ThisWorkbook.vb#1)]
 [!code-csharp[Trin_Ribbon_Choose_Ribbon#1](../vsto/codesnippet/CSharp/trin_Ribbon_choose_Ribbon_4/ThisWorkbook.cs#1)]

### <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[方法: リボンのカスタマイズを開始する](../vsto/how-to-get-started-customizing-the-ribbon.md)|Microsoft Office アプリケーションのリボンをカスタマイズし、 **リボン (ビジュアルデザイナー)** または **リボン (XML)** 項目を Office プロジェクトに追加する方法について説明します。|
|[リボンデザイナー](../vsto/ribbon-designer.md)|リボンデザイナーを使用して、Microsoft Office アプリケーションのリボンにカスタムタブ、グループ、およびコントロールを追加する方法について説明します。|
|[チュートリアル: リボンデザイナーを使用したカスタムタブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)|リボン デザイナーを使用してカスタム リボン タブを作成する方法について説明します。 リボン デザイナーを使用すると、カスタム タブにコントロールを追加し、位置を設定することができます。|
|[リボンオブジェクトモデルの概要](../vsto/ribbon-object-model-overview.md)|実行時にリボン コントロールのプロパティを取得および設定するために使用できる厳密に型指定されたオブジェクト モデルの概要について説明します。|
|[チュートリアル: 実行時にリボンのコントロールを更新する](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)|Office アプリケーションにリボンを読み込んだ後に、リボン オブジェクト モデルを使用してリボン上のコントロールを更新する方法について説明します。|
|[Outlook のリボンのカスタマイズ](../vsto/customizing-a-ribbon-for-outlook.md)|Outlook Microsoft Office でリボンをカスタマイズするためのガイダンスを示します。|
|[InfoPath のリボンのカスタマイズ](../vsto/customizing-a-ribbon-for-infopath.md)|InfoPath Microsoft Office でリボンをカスタマイズするためのガイダンスを示します。|
|[実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)|リボンを表示、非表示、および変更する方法と、ユーザーがカスタム作業ウィンドウ、操作ウィンドウ、または Outlook フォーム領域のコントロールからコードを実行できるようにする方法について説明します。|
|[方法: リボンのタブの位置を変更する](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)|リボンのタブの順序を変更する方法について説明します。|
|[方法: 組み込みタブをカスタマイズする](../vsto/how-to-customize-a-built-in-tab.md)|組み込みタブにグループやコントロールを追加する方法について説明します。|
|[方法: Backstage ビューにコントロールを追加する](../vsto/how-to-add-controls-to-the-backstage-view.md)|**ファイル**をクリックしたときに開かれるメニューにコントロールを追加する方法について説明します。|
|[方法: リボングループにダイアログボックスランチャーを追加する](../vsto/how-to-add-a-dialog-box-launcher-to-a-ribbon-group.md)|リボン上の任意のグループにダイアログボックスランチャーを追加する方法を示します。|
|[方法: リボンをリボンデザイナーからリボン XML にエクスポートする](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)|リボンをデザイナーからリボン XML にエクスポートすることによって、高度な方法でリボンをカスタマイズする方法について説明します。|
|[Ribbon XML](../vsto/ribbon-xml.md)|リボン XML を使用してリボンをカスタマイズする方法について説明します。|
|[チュートリアル: リボンデザイナーを使用したカスタムタブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)|**リボン (XML)** 項目を使用してカスタムリボンタブを作成する方法を示します。|
