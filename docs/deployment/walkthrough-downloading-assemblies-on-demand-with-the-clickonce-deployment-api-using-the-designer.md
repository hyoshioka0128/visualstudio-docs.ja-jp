---
title: デザイナーを使用して必要に応じてアセンブリをダウンロードする (ClickOnce API)
description: デザイナーを使用して ClickOnce アプリケーションの特定のアセンブリをオプションとしてマークし、共通言語ランタイムで必要になったときにそれらをダウンロードする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- assemblies, downloading [ClickOnce]
- Windows applications, ClickOnce deployments
- ClickOnce deployment, on-demand download
- on-demand assemblies, ClickOnce
ms.assetid: 59a0dd5f-1cab-4f2f-b780-0ab7399905d5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0c2ced89c73d39fecb6b6cee80a8fddb0a8c2391
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99917329"
---
# <a name="walkthrough-download-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer"></a>チュートリアル: デザイナーを使用して ClickOnce 配置 API で必要に応じてアセンブリをダウンロードする
既定では、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに含まれるすべてのアセンブリが、アプリケーションを初めて実行したときにダウンロードされます。 ただし、アプリケーションには少数のユーザーにしか使われない部分が含まれることがあります。 その場合は、そのような型を作成するときにだけアセンブリをダウンロードすることができます。 以下のチュートリアルでは、アプリケーション内の特定のアセンブリに "オプション" マークを付ける方法、および共通言語ランタイムでそのアセンブリが必要なときに <xref:System.Deployment.Application> 名前空間にあるクラスを使用してアセンブリをダウンロードする方法について説明します。

> [!NOTE]
> これを行うには、アプリケーションが完全な信頼で実行する必要があります。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[リセット設定](../ide/environment-settings.md#reset-settings)」を参照してください。

## <a name="create-the-projects"></a>プロジェクトを作成する

### <a name="to-create-a-project-that-uses-an-on-demand-assembly-with-visual-studio"></a>Visual Studio でオンデマンド アセンブリを使用するプロジェクトを作成するには

1. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]で新しい Windows フォーム プロジェクトを作成します。 **[ファイル]** メニューの **[追加]** をポイントし、**[新しいプロジェクト]** をクリックします。 ダイアログ ボックスで **[クラス ライブラリ]** プロジェクトを選択し、名前を `ClickOnceLibrary`に設定します。

   > [!NOTE]
   > Visual Basic でプロジェクトのプロパティを変更し、このプロジェクトのルート名前空間を `Microsoft.Samples.ClickOnceOnDemand` または他の適切な名前空間にすることをお勧めします。 わかりやすくするため、このチュートリアルでは 2 つのプロジェクトを同じ名前空間にします。

2. `DynamicClass` という名前のプロパティを 1 つ持つ `Message`という名前のクラスを定義します。

    [!code-vb[ClickOnceLibrary#1](../deployment/codesnippet/VisualBasic/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer_1.vb)]
    [!code-csharp[ClickOnceLibrary#1](../deployment/codesnippet/CSharp/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer_1.cs)]

3. **ソリューション エクスプローラー** で Windows フォーム プロジェクトを選択します。 <xref:System.Deployment.Application> アセンブリに対する参照および `ClickOnceLibrary` プロジェクトに対するプロジェクト参照を追加します。

   > [!NOTE]
   > Visual Basic でプロジェクトのプロパティを変更し、このプロジェクトのルート名前空間を `Microsoft.Samples.ClickOnceOnDemand` または他の適切な名前空間にすることをお勧めします。 わかりやすくするため、このチュートリアルでは 2 つのプロジェクトを同じ名前空間にします。

4. フォームを右クリックし、メニューの **[コードの表示]** をクリックして、次の参照をフォームに追加します。

    [!code-csharp[ClickOnceOnDemand#1](../deployment/codesnippet/CSharp/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer_2.cs)]
    [!code-vb[ClickOnceOnDemand#1](../deployment/codesnippet/VisualBasic/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer_2.vb)]

5. このアセンブリをオンデマンドでダウンロードする次のコードを追加します。 このコードでは、 <xref:System.Collections.DictionaryBase.Dictionary%2A> ジェネリック クラスを使用してアセンブリのセットをグループ名にマップする方法を示します。 このチュートリアルではダウンロードするアセンブリが 1 つだけなので、グループに含まれるアセンブリは 1 つのみです。 実際のアプリケーションでは、アプリケーションの 1 つの機能に関連するすべてのアセンブリを同時にダウンロードすることがあります。 マッピング テーブルを使用すると、機能に属しているすべての DLL をダウンロード グループ名に関連付けることにより、これを簡単に実行できます。

    [!code-csharp[ClickOnceOnDemand#2](../deployment/codesnippet/CSharp/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer_3.cs)]
    [!code-vb[ClickOnceOnDemand#2](../deployment/codesnippet/VisualBasic/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer_3.vb)]

6. **[表示]** メニューの **[ツールボックス]** をクリックします。 <xref:System.Windows.Forms.Button> ツールボックス **からフォームに** をドラッグします。 ボタンをダブルクリックして、 <xref:System.Windows.Forms.Control.Click> イベント ハンドラーに次のコードを追加します。

    [!code-csharp[ClickOnceOnDemand#3](../deployment/codesnippet/CSharp/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer_4.cs)]
    [!code-vb[ClickOnceOnDemand#3](../deployment/codesnippet/VisualBasic/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer_4.vb)]

## <a name="mark-assemblies-as-optional"></a>アセンブリをオプションとしてマークする

### <a name="to-mark-assemblies-as-optional-in-your-clickonce-application-by-using-visual-studio"></a>Visual Studio を使用して ClickOnce アプリケーションでアセンブリをオプションとしてマークするには

1. **ソリューション エクスプローラー** で Windows フォーム プロジェクトを右クリックし、 **[プロパティ]** をクリックします。 **[発行]** タブを選択します。

2. **[アプリケーション ファイル]** ボタンをクリックします。

3. *ClickOnceLibrary.dll* のリストを探します。 **[発行の状況]** ドロップダウン ボックスを **[含む]** に設定します。

4. **[グループ]** ドロップダウン ボックスを展開し、 **[新規]** を選択します。 新しいグループ名として「 `ClickOnceLibrary` 」と入力します。

5. 「 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)する」の説明に従って、アプリケーションの発行を続行します。

### <a name="to-mark-assemblies-as-optional-in-your-clickonce-application-by-using-manifest-generation-and-editing-tool--graphical-client-mageuiexe"></a>マニフェストの生成および編集ツールを使用して ClickOnce アプリケーションでアセンブリをオプションとしてマークするには — グラフィカル クライアント (MageUI.exe)

1. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]「[チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」の説明に従って、マニフェストを作成します。

2. MageUI.exe を終了する前に、配置のアプリケーション マニフェストを含むタブを選択し、そのタブで **[ファイル]** タブを選択します。

3. アプリケーション ファイルの一覧で ClickOnceLibrary.dll を探し、 **[ファイルの種類]** 列を **[なし]** に設定します。 **[グループ]** 列に「 `ClickOnceLibrary.dll`」と入力します。

## <a name="test-the-new-assembly"></a>新しいアセンブリをテストする

オンデマンド アセンブリをテストするには

1. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]で配置されたアプリケーションを起動します。

2. メイン フォームが表示されたら、 <xref:System.Windows.Forms.Button>をクリックします。 メッセージ ボックスに "Hello, World!" と表示されます。

## <a name="see-also"></a>関連項目

- <xref:System.Deployment.Application.ApplicationDeployment>
