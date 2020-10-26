---
title: 'チュートリアル: Outlook フォーム領域のデザイン'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 01cfe55964a1d61c2ad200c9538ced9ff0aa5599
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72985465"
---
# <a name="walkthrough-design-an-outlook-form-region"></a>チュートリアル: Outlook フォーム領域のデザイン
  カスタム フォーム領域は、標準またはカスタムの Microsoft Office Outlook フォームを拡張します。 このチュートリアルでは、連絡先アイテムのインスペクター ウィンドウに新しいページとして表示するカスタム フォーム領域をデザインします。 このフォーム領域では、アドレス情報を Windows Live Local Search の Web サイトに送信することによって、連絡先に設定された個々の住所の地図を表示します。 フォーム領域の詳細については、「 [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)」を参照してください。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 このチュートリアルでは、次の作業について説明します。

- 新しい Outlook VSTO アドイン プロジェクトの作成。

- VSTO アドイン プロジェクトへのフォーム領域の追加。

- フォーム領域のレイアウトのデザイン。

- フォーム領域の動作のカスタマイズ。

- Outlook フォーム領域のテスト。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Outlook_14_short](../vsto/includes/outlook-14-short-md.md)] 以降。

  ![ビデオへのリンク](../vsto/media/playvideo.gif "ビデオへのリンク") このトピックのビデオ版については、「 [方法: Outlook フォーム領域をデザイン](/previous-versions/visualstudio/visual-studio-2008/cc837160(v=vs.90))する」を参照してください。

## <a name="create-a-new-outlook-vsto-add-in-project"></a>新しい Outlook VSTO アドインプロジェクトを作成する
 まず、基本的な VSTO アドイン プロジェクトを作成します。

### <a name="to-create-a-new-outlook-vsto-add-in-project"></a>新しい Outlook VSTO アドイン プロジェクトを作成するには

1. で [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、 **Mapitaddin**という名前の Outlook VSTO アドインプロジェクトを作成します。

2. **[新しいプロジェクト]** ダイアログ ボックスの **[ソリューションのディレクトリを作成]** チェック ボックスをオンにします。

3. プロジェクトを任意のディレクトリに保存します。

     詳細については、「 [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

## <a name="add-a-form-region-to-the-outlook-vsto-add-in-project"></a>Outlook VSTO アドインプロジェクトへのフォーム領域の追加
 Outlook VSTO アドイン ソリューションには、1 つ以上の Outlook フォーム領域アイテムを格納できます。 **新しい Outlook フォーム領域**ウィザードを使用して、プロジェクトにフォーム領域アイテムを追加します。

### <a name="to-add-a-form-region-to-the-outlook-vsto-add-in-project"></a>Outlook VSTO アドイン プロジェクトにフォーム領域を追加するには

1. **ソリューションエクスプローラー**で、 **mapitaddin**プロジェクトを選択します。

2. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

3. [ **新しい項目の追加** ] ダイアログボックスで、[ **Outlook フォーム領域**] を選択し、ファイルに **mapit**という名前を指定して、[ **追加**] をクリックします。

     **Newoutlook フォーム領域**ウィザードが起動します。

4. [ **フォーム領域を作成する方法を選択** します] ページで、[ **新しいフォーム領域をデザイン**する] をクリックし、[ **次へ**] をクリックします。

5. [ **作成するフォーム領域の種類を選択** します] ページで、[ **分離**] をクリックし、[ **次へ**] をクリックします。

     *別*のフォーム領域によって Outlook フォームに新しいページが追加されます。 フォーム領域の種類の詳細については、「 [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)」を参照してください。

6. [**説明用のテキストを指定し、表示設定を選択**します] ページで、[**名前**] ボックスに「 **Map It** 」と入力します。

     この名前は、連絡先アイテムを開いたときにインスペクター ウィンドウのリボンに表示されます。

7. **作成モードのインスペクター**と**読み取りモードのインスペクター**を選択し、[**次へ**] をクリックします。

8. [ **このフォーム領域を表示するメッセージクラスを指定** します] ページで、[ **メールメッセージ**] をクリアし、[ **連絡先**] を選択して、[ **完了**] をクリックします。

     *MapIt.cs*ファイルまたは*mapit .vb*ファイルがプロジェクトに追加されます。

## <a name="design-the-layout-of-the-form-region"></a>フォーム領域のレイアウトをデザインする
 フォーム *領域デザイナー*を使用して、フォーム領域を視覚的に開発します。 フォーム領域デザイナーの画面にマネージド コントロールをドラッグできます。 デザイナーと [ **プロパティ** ] ウィンドウを使用すると、コントロールのレイアウトと外観を調整できます。

### <a name="to-design-the-layout-of-the-form-region"></a>フォーム領域のレイアウトをデザインするには

1. **ソリューションエクスプローラー**で、 **mapitaddin**プロジェクトを展開し、 *MapIt.cs*または*Mapit .Vb*をダブルクリックしてフォーム領域デザイナーを開きます。

2. デザイナーを右クリックし、[ **プロパティ**] をクリックします。

3. [ **プロパティ** ] ウィンドウで、[ **サイズ** ] を **664, 469**に設定します。

     これにより、フォーム領域が地図を表示するのに十分な大きさになります。

4. **[表示]** メニューの **[ツールボックス]** をクリックします。

5. **ツールボックス**の [**コモンコントロール**] タブから、 **WebBrowser**をフォーム領域に追加します。

     **WebBrowser**には、連絡先について一覧表示されている各住所のマップが表示されます。

## <a name="customize-the-behavior-of-the-form-region"></a>フォーム領域の動作をカスタマイズする
 フォーム領域の実行時の動作をカスタマイズするには、フォーム領域のイベント ハンドラーにコードを追加します。 このフォーム領域に対して、コードは Outlook アイテムのプロパティを調べ、Map It フォーム領域を表示するかどうかを決定します。 フォーム領域を表示する場合、コードは Windows Live Local Search に接続し、Outlook 連絡先アイテムに設定された各住所の地図を読み込みます。

### <a name="to-customize-the-behavior-of-the-form-region"></a>フォーム領域の動作をカスタマイズするには

1. **ソリューションエクスプローラー**で、 *MapIt.cs*または*mapit .vb*を右クリックし、[**コードの表示**] をクリックします。

    *MapIt.cs* または *mapit. Vb* がコードエディターで開きます。

2. **フォーム領域ファクトリ**コード領域を展開します。

    `MapItFactory` という名前のフォーム領域ファクトリ クラスが公開されます。

3. `MapItFactory_FormRegionInitializing` イベント ハンドラーに次のコードを追加します。 このイベント ハンドラーは、ユーザーが連絡先アイテムを開いたときに呼び出されます。 次のコードは、連絡先アイテムに住所が含まれているかどうかを判定します。 連絡先アイテムに住所が含まれていない場合、このコードは <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> クラスのプロパティを <xref:Microsoft.Office.Tools.Outlook.FormRegionInitializingEventArgs> **true** に設定し、フォーム領域は表示されません。 それ以外の場合は、VSTO アドインで <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing> イベントが発生し、フォーム領域が表示されます。

    [!code-csharp[Trin_Outlook_FR_Separate#1](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs#1)]
    [!code-vb[Trin_Outlook_FR_Separate#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb#1)]

4. <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing> イベント ハンドラーに次のコードを追加します。 このコードは、以下のタスクを実行します。

   - 連絡先アイテムの各住所を連結し、URL 文字列を作成します。

   - <xref:System.Windows.Forms.WebBrowser> オブジェクトの <xref:System.Windows.Forms.WebBrowser.Navigate%2A> メソッドを呼び出し、パラメーターとして URL 文字列を渡します。

     Map It フォーム領域に Local Search の Web サイトが表示され、スクラッチ パッドに各住所が表示されます。

     [!code-csharp[Trin_Outlook_FR_Separate#2](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs#2)]
     [!code-vb[Trin_Outlook_FR_Separate#2](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb#2)]

## <a name="test-the-outlook-form-region"></a>Outlook フォーム領域のテスト
 プロジェクトを実行すると、Visual Studio によって Outlook が開かれます。 連絡先アイテムを開くと、Map It フォーム領域が表示されます。 Map It フォーム領域は、住所が含まれる連絡先アイテムのフォームのページとして表示されます。

### <a name="to-test-the-map-it-form-region"></a>Map It フォーム領域をテストするには

1. **F5**キーを押してプロジェクトを実行します。

     Outlook が開きます。

2. Outlook の [ **ホーム** ] タブで、[ **新しいアイテム**] をクリックし、[ **連絡先**] をクリックします。

3. 連絡先フォームに、連絡先の名前として「 **彩 Beebe** 」と入力し、次の3つのアドレスを指定します。

    |住所の種類|Address|
    |------------------|-------------|
    |**勤務先**|**4567 Main バッファロー、NY**|
    |**Home**|**1234北部バッファロー、NY**|
    |**その他**|**3456 Main St Seattle, WA**|

4. 連絡先アイテムを保存して閉じます。

5. **彩 Beebe**の連絡先項目を再度開きます。

    Outlook では、 **[検索] グループで** この操作を行うには、連絡先のアドレス帳を開くか、「彩 Beebe」と入力して **検索担当**者に入力します。

6. 項目のリボンの [ **表示** ] グループで、[ **マップ** ] をクリックして、マップ it フォーム領域を開きます。

     Map It フォーム領域が開き、Local Search の Web サイトが表示されます。 **ビジネス**、**自宅**、および**その他の**アドレスは、スクラッチパッドに表示されます。 スクラッチ パッドで、地図を表示する住所を選択します。

## <a name="next-steps"></a>次の手順
 Outlook アプリケーションの UI をカスタマイズする方法の詳細については、次のトピックを参照してください。

- Outlook アイテムのリボンをカスタマイズする方法については、「 [outlook のリボンをカスタマイズ](../vsto/customizing-a-ribbon-for-outlook.md)する」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [実行時のフォーム領域へのアクセス](../vsto/accessing-a-form-region-at-run-time.md)
- [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)
- [Outlook フォーム領域を作成するためのガイドライン](../vsto/guidelines-for-creating-outlook-form-regions.md)
- [チュートリアル: Outlook でデザインされたフォーム領域をインポートする](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
- [方法: フォーム領域を Outlook アドインプロジェクトに追加する](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
- [フォーム領域を Outlook メッセージクラスに関連付ける](../vsto/associating-a-form-region-with-an-outlook-message-class.md)
- [Outlook フォーム領域のカスタムアクション](../vsto/custom-actions-in-outlook-form-regions.md)
- [方法: Outlook でフォーム領域が表示されないようにする](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)
