---
title: Outlook フォーム領域の作成
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- MICROSOFT.OFFICE.TOOLS.OUTLOOK.FORMREGION
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio]
- form regions [Office development in Visual Studio], creating
- Outlook [Office development in Visual Studio], form regions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8a999ca11427533690628fb92f28e93d22cf0971
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "71255916"
---
# <a name="create-outlook-form-regions"></a>Outlook フォーム領域の作成
  フォーム領域を使用して、Microsoft Office Outlook フォームをカスタマイズできます。 Visual Studio には、フォーム領域のデザイン、開発、およびデバッグを簡単に行うことができる高度なツールが用意されています。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 このトピックでは次の情報について説明します。

- [フォーム領域を使用する利点](#Enhance)

- [プロジェクトに Outlook フォーム領域を追加する](#Adding)

- [フォーム領域デザイナーを使用する](#UsingFormRegionDesigner)

- [Outlook でデザインされたフォーム領域を使用する](#UsingFormRegionDesignedOutlook)

- [フォーム領域へのカスタムコードの追加](#AddingCustomCode)

- [プロジェクトのビルド](#Building)

- [フォーム領域のデバッグ](#Debugging)

- [フォーム領域を配置する](#Deploying)

## <a name="advantages-of-using-form-regions"></a><a name="Enhance"></a> フォーム領域を使用する利点
 フォーム領域は、従来の Outlook フォーム開発に多くの機能強化をもたらします。

- 標準フォームの既定のページをカスタマイズする。

- 標準フォームに最大 12 ページ追加する。

- 標準フォームを置換または拡張する。

- 閲覧ペインとインスペクターにカスタム UI を表示する。

  詳細については、「 [フォームページとフォーム領域をカスタマイズ](/office/vba/outlook/Concepts/Forms/customizing-form-pages-and-form-regions)する」を参照してください。

## <a name="add-an-outlook-form-region-to-your-project"></a><a name="Adding"></a> プロジェクトに Outlook フォーム領域を追加する
 **新しい Outlook フォーム領域**ウィザードを使用して、新しいフォーム領域をデザインしたり、outlook でデザインされたフォーム領域をインポートしたりできます。 また、別の Outlook VSTO アドイン プロジェクトで使用したフォーム領域がある場合は、既存のフォーム領域を再利用できます。

### <a name="create-a-new-form-region-by-using-the-wizard"></a><a name="CreatingFormRegion"></a> ウィザードを使用して新しいフォーム領域を作成する
 フォーム領域を作成するには、outlook VSTO アドインプロジェクトに **Outlook フォーム領域** アイテムを追加します。 **新しい Outlook フォーム領域**ウィザードが起動します。

 このウィザードでは、新しいフォーム領域をデザインするか、Outlook でデザインしたフォーム領域をインポートするかを指定します。 新しいフォーム領域のデザインの詳細については、「 [フォーム領域デザイナーの使用](#UsingFormRegionDesigner)」を参照してください。 Outlook でデザインされたフォーム領域の使用方法の詳細については、「 [outlook でデザインされたフォーム領域をインポートする](#UsingFormRegionDesignedOutlook)」を参照してください。

 このウィザードでは、作成するフォーム領域の種類を指定します。 フォーム領域の種類について、次の表で説明します。

|リージョンの種類|説明|
|-----------------|-----------------|
|分離|フォーム領域を Outlook フォームの新しいページとして追加します。|
|隣接|フォーム領域を Outlook フォームの既定のページの下部に追加します。|
|代替|フォーム領域を Outlook フォームの既定のページに代わる新しいページとして追加します。|
|すべて置換|Outlook フォーム全体をフォーム領域に置き換えます。|

 このウィザードでは、表示条件を指定し、拡張するフォームの種類を選択することもできます。 詳細については、「 [方法: フォーム領域を Outlook アドインプロジェクトに追加](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)する」を参照してください。

 このウィザードで行った選択は、他のウィザード ページで使用できるオプションに影響します。 たとえば、[**新しい Outlook フォーム領域を作成**する] ページで [**隣接**] または [**個別**] を選択した場合、[**説明用のテキストを入力し、表示設定を選択**します] ページで [**タイトル**] フィールドと [**説明**] フィールドを使用できません。 これは、隣接または分離フォーム領域を表示するときに、Outlook ではこれらのフィールドを使用しないためです。

#### <a name="form-region-files"></a>フォーム領域ファイル
 **新しい Outlook フォーム領域**ウィザードを完了すると、Visual Studio によって次のファイルがプロジェクトに自動的に追加されます。

- フォーム領域コード ファイル。 このファイルには、[**新しい項目の追加**] ダイアログボックスで**Outlook フォーム領域**の項目に指定した名前が付いています。 このファイルには、フォーム領域イベントを処理するコードを追加します。

- フォーム領域デザイナー コード ファイル。 このファイルは、フォーム領域デザイナーによって生成されたコードを含んでおり、直接編集すべきではありません。

- Outlook Form Storage (*.ofs*) ファイル。

    > [!NOTE]
    > このファイルがプロジェクトに追加されるのは、Outlook でデザインしたフォーム領域をインポートした場合だけです。

#### <a name="form-region-factory-class"></a>フォーム領域ファクトリクラス
 フォーム領域コード ファイルには、<xref:Microsoft.Office.Tools.Outlook.IFormRegionFactory> インターフェイスを実装する部分クラスが含まれています。 これがフォーム領域ファクトリ クラスです。 フォーム領域ファクトリ クラスは、フォーム領域の新しいインスタンスを作成するために使用します。

 このクラスは、 **フォーム領域ファクトリ** 領域を展開することで見つけることができます。

 **新しい Outlook フォーム領域**ウィザードは、フォーム領域の内部名とフォーム領域を表示するメッセージクラスを指定する属性をこのクラスに追加します。 これらの属性は、ファイルがプロジェクトに追加された後、手動で変更できます。

 フォーム領域ファクトリ クラスの大部分は、フォーム領域デザイナー ファイルに実装されます。 ただし、`FormRegionInitializing` イベント ハンドラーはフォーム領域コード ファイルに公開されます。 このイベント ハンドラーを使用して、Outlook がフォーム領域を表示するかどうかを指定できます。 詳細については、「 [フォーム領域イベントの処理](#HandlingFormRegionEvents)」を参照してください。

### <a name="add-an-existing-form-region-to-your-project"></a><a name="AddingExistingFormRegion"></a> 既存のフォーム領域をプロジェクトに追加する
 別の Outlook プロジェクトで使用した Outlook フォーム領域がある場合は、 **[既存項目の追加]** ダイアログ ボックスを使用して、そのフォーム領域を現在の Outlook VSTO アドイン プロジェクトで再利用できます。

 既存のフォーム領域には、コードファイル (*.vb*または *.cs*) が必要です。[**既存項目の追加**] ダイアログボックスを使用して Outlook Form Storage (*.ofs*) ファイルを追加することはできません。 ただし、Outlook Form Storage ファイルをインポートすることによって新しいフォーム領域を作成できます。 詳細については、「 [方法: フォーム領域を Outlook アドインプロジェクトに追加](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)する」を参照してください。

## <a name="use-the-form-region-designer"></a><a name="UsingFormRegionDesigner"></a> フォーム領域デザイナーを使用する
 フォーム領域デザイナーでは、フォーム領域のレイアウトと外観をデザインできます。 マネージコントロールをデザイナーの画面にドラッグし、[コントロール] をダブルクリックしてイベントハンドラーを開き、[ **プロパティ** ] ウィンドウでプロパティを設定することができます。

> [!NOTE]
> フォーム領域が Outlook の [**プロパティ**] ウィンドウの [**マニフェスト**] ノードの下に表示される方法に影響を与えるプロパティを見つけることができます。

 フォーム領域デザイナーは、**新しい Outlook フォーム領域**ウィザードの [**フォーム領域を作成する方法を選択**してください] ページで [**新しいフォーム領域をデザイン**する] を選択した場合にのみ使用できます。

 フォーム領域デザイナーを開くには、次の 3 つの方法があります。

- **ソリューションエクスプローラー**で、フォーム領域コードファイルをダブルクリックします。

- **ソリューションエクスプローラー**で、フォーム領域コードファイルを右クリックし、[デザイナーの**表示**] をクリックします。

- **ソリューションエクスプローラー**で、フォーム領域コードファイルを選択し、[**表示**] メニューの [**デザイナー**] をクリックします。

  フォーム領域デザイナーは、マネージド コントロールのみをサポートしています。 ネイティブな Outlook コントロールを追加することはできません。

## <a name="import-a-form-region-designed-in-outlook"></a><a name="UsingFormRegionDesignedOutlook"></a> Outlook でデザインされたフォーム領域をインポートする
 Outlook でデザインする際に、ネイティブな Outlook コントロールをフォーム領域に追加できます。 ネイティブな Outlook コントロールは、デザイン時に Outlook データにバインドできます。 ただし、その場合はフォーム領域デザイナーを使用してマネージド コントロールを追加したりフォーム領域のデザインを変更したりすることはできません。

 **新しい Outlook フォーム領域**ウィザードを使用して、フォーム領域を Outlook VSTO アドインプロジェクトにインポートできます。 [ **フォーム領域を作成する方法を選択し** ます] ページで、[ **Outlook フォームストレージ (.ofs) ファイルのインポート**] を選択します。 その後、Outlook Form Storage ファイル (*.ofs*) ファイルの場所を参照できます。 (フォーム領域は *.ofs* ファイルとして保存されます)。

 **新しい Outlook フォーム領域**ウィザードでは、 *.ofs*ファイルがプロジェクトディレクトリにコピーされ、コントロール参照がフォーム領域デザイナーファイルに追加されます。 これで、フォーム領域コード ファイルでコントロールのイベントを処理できます。

 Visual Basic プロジェクトでイベントを処理するには、コード エディターの上部にあるメソッド名リストからイベントを選択します。

 C# プロジェクトでイベントを処理するには、<xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing> メソッドでコントロール イベントにサブスクライブします。 詳細については、「 [方法: イベントをサブスクライブまたは登録解除する &#40;C&#35; プログラミングガイド&#41;](/dotnet/csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events)」を参照してください。

 フォーム領域のプロパティは、フォーム領域ファクトリ クラスの `InitializeManifest` メソッドで変更できます。

> [!NOTE]
> フォーム領域をインポートするには、開発用コンピューターにインストールされている Outlook と同じバージョンの Outlook を対象とするプロジェクトで作業している必要があります。 たとえば、Outlook 2010 がインストールされている場合、フォーム領域のインポートは、 **outlook 2010 アドイン** プロジェクトテンプレートを使用して作成されたプロジェクトでのみ機能します。

### <a name="update-an-imported-form-regions-design"></a>インポートされたフォーム領域のデザインを更新する
 フォーム領域に対して、コントロールの追加、削除、または変更を行うことができます。 これを行う前に、フォーム領域コード ファイルに追加したコードをバックアップします。 次に、Outlook で *.ofs* ファイルを開き、フォーム領域を変更して、変更を保存します。 **新しい Outlook フォーム領域**ウィザードを使用して、変更*した .ofs*ファイルをインポートします。 その後、新しいフォーム領域コード ファイルにコードを貼り付けることができます。

## <a name="add-custom-code-to-a-form-region"></a><a name="AddingCustomCode"></a> フォーム領域へのカスタムコードの追加
 <xref:Microsoft.Office.Tools.Outlook> 名前空間では、フォーム領域、フォーム領域を表示する Outlook アイテム、およびその他の役に立つアイテムを表すクラスにアクセスできます。 **Outlook フォーム領域**の項目は、自動的にこのアセンブリへの参照をプロジェクトに追加し、適切な**Using**または**Imports**ステートメントをフォーム領域コードファイルの先頭に挿入します。

 `Microsoft.Office.Interop.Outlook` 名前空間のクラス、メソッド、およびプロパティを使用して、ほとんどの Outlook プログラミング タスクを実行できます。 Outlook オブジェクトモデルの詳細については、「 [outlook オブジェクトモデルの概要](../vsto/outlook-object-model-overview.md)」を参照してください。 Outlook オブジェクトモデルを使用する一般的なタスクの例については、「 [outlook solutions (outlook ソリューション](../vsto/outlook-solutions.md))」を参照してください。

### <a name="handle-form-region-events"></a><a name="HandlingFormRegionEvents"></a> フォーム領域イベントの処理
 **Outlook フォーム領域**の項目は、次の3つのイベントハンドラーをフォーム領域コードファイルに自動的に追加します。

|Event|説明|
|-----------|-----------------|
|FormRegionInitializing|フォーム領域が初期化される前に発生します。 このイベント ハンドラーの状態をチェックして、Outlook がフォーム領域を表示する必要があるかどうかを判定できます。 詳細については、「 [方法: Outlook にフォーム領域が表示されないよう](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)にする」を参照してください。|
|FormRegionShowing|フォーム領域のインスタンスが作成されてから、フォーム領域が表示される前までの間に発生します。|
|FormRegionClosed|フォーム領域が閉じられる前に発生します。|

## <a name="build-the-project"></a><a name="Building"></a> プロジェクトをビルドする
 フォーム領域を含む Outlook VSTO アドイン プロジェクトをビルドすると、Visual Studio によってレジストリに次の情報が追加されます。

- 1 つ以上のフォーム領域に関連付けられている各メッセージ クラスのキー。

- 各フォーム領域のエントリと、Outlook VSTO アドインの名前を表す関連値。

  この情報は、Outlook がフォーム領域を読み込むときに使用されます。

## <a name="debug-a-form-region"></a><a name="Debugging"></a> フォーム領域のデバッグ
 フォーム領域を含む Outlook VSTO アドインは、他の [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] プロジェクトと同じようにデバッグできます。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デバッガーを起動すると、Visual Studio によって自動的に Outlook が起動されます。

 フォーム領域を表示するには、対応する Outlook アイテムを開く必要があります。 たとえば、隣接フォーム領域をメール アイテムの下部に追加する場合は、メール アイテムを開きます。

## <a name="deploy-a-form-region"></a><a name="Deploying"></a> フォーム領域を配置する
 フォーム領域は、関連付けられた Outlook VSTO アドインと共に自動的に配置されます。 したがって、フォーム領域を配置するための特別なタスクを実行する必要はありません。 VSTO アドインの配置の詳細については、「 [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[Outlook フォーム領域を作成するためのガイドライン](../vsto/guidelines-for-creating-outlook-form-regions.md)|フォーム領域を最適化し、発生する可能性のある問題を回避するのに役立つ情報を提供します。|
|[方法: フォーム領域を Outlook アドインプロジェクトに追加する](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)|**新しい Outlook フォーム領域**ウィザードを使用して、標準またはカスタムの Microsoft Office outlook フォームを拡張するフォーム領域を作成する方法について説明します。|
|[フォーム領域を Outlook メッセージクラスに関連付ける](../vsto/associating-a-form-region-with-an-outlook-message-class.md)|フォーム領域を各アイテムのメッセージ クラスに関連付けることにより、そのフォーム領域を表示する Microsoft Office Outlook アイテムを指定する方法について説明します。|
|[チュートリアル: Outlook フォーム領域のデザイン](../vsto/walkthrough-designing-an-outlook-form-region.md)|連絡先アイテムのインスペクター ウィンドウに新しいページとして表示するカスタム フォーム領域をデザインする方法について説明します。|
|[チュートリアル: Outlook でデザインされたフォーム領域をインポートする](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)|Outlook Microsoft Office でフォーム領域をデザインし、 **新しい Outlook フォーム領域** ウィザードを使用して Outlook VSTO アドインプロジェクトにフォーム領域をインポートする方法について説明します。|
|[実行時のフォーム領域へのアクセス](../vsto/accessing-a-form-region-at-run-time.md)|コードを記述して、フォーム領域でコントロールの表示、非表示、変更を行う方法と、`Globals` クラスを使用して、記述したコードをユーザーがプロジェクト内の他の領域から実行できるようにする方法について説明します。|
|[方法: Outlook でフォーム領域が表示されないようにする](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)|Microsoft Office Outlook で特定のアイテムのフォーム領域が表示されないようにする方法について説明します。|
|フォーム領域が表示される Outlook アイテムにアクセスする方法について説明します。|
|[Outlook フォーム領域のカスタムアクション](../vsto/custom-actions-in-outlook-form-regions.md)|ユーザーが Outlook アイテムに応答できるようにする方法について説明します。|
