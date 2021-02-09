---
title: SharePoint のパッケージ化と配置のトラブルシューティング |Microsoft Docs
description: SharePoint ソリューションをパッケージ化して配置するときに発生する可能性のあるさまざまな問題について理解し、修正します。
ms.custom: SEO-VS-2020
ms.date: 02/22/2017
ms.topic: conceptual
f1_keywords:
- VSTO.WorkflowDeployment.Troubleshooting
- VS.SharePointTools.Project.PackageRetraction
- VS.SharePointTools.Deployment.Troubleshooting
- VS.SharePointTools.Deploying.Troubleshooting
- VS.SharePointTools.Project.DeploymentTroubleshooting
- VS.SharePointTools.Project.SharePointNotInstalled
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packaging
- SharePoint development in Visual Studio, troubleshooting
- SharePoint development in Visual Studio, deployment conflict resolution
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f3ef56ba868700699eaaeb8ec88291fd6f8d8d32
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99892308"
---
# <a name="troubleshoot-sharepoint-packaging-and-deployment"></a>SharePoint のパッケージ化と配置のトラブルシューティング
  このトピックでは、SharePoint ソリューションをパッケージ化および配置するときに発生する可能性があるさまざまな問題について説明します。

## <a name="enable-enhanced-debugging"></a>強化されたデバッグを有効にする
 Visual Studio、SharePoint、およびその他のレイヤーの間で問題を診断する場合は、EnableDiagnostics レジストリ キーを使用してスタック トレースを表示することができます。 詳細については、「 [SharePoint ソリューションのデバッグ](../sharepoint/debugging-sharepoint-solutions.md)」を参照してください。

## <a name="add-project-output-to-the-solution-package"></a>ソリューションパッケージにプロジェクト出力を追加する
 パッケージ デザイナーを使用してパッケージにプロジェクト出力を追加することができます。 ただし、プロジェクト出力を追加する際には、そのプロジェクトのプラットフォームが SharePoint ソリューションのプラットフォームと一致していることを確認する必要があります。 SharePoint サーバーに配置するアセンブリには、 **ANY CPU** プラットフォームターゲットを使用することをお勧めします。 詳細については、「[ [コンパイル] ページ」、「プロジェクトデザイナー &#40;Visual Basic&#41;](../ide/reference/compile-page-project-designer-visual-basic.md) および [[コンパイラの詳細設定] ダイアログボックス &#40;Visual Basic&#41;](../ide/reference/advanced-compiler-settings-dialog-box-visual-basic.md)」を参照してください。

## <a name="validation-warnings-and-errors"></a>検証の警告とエラー
 Visual Studio の SharePoint 開発ツールでは、ソリューション パッケージが正しい形式になっていることを確認するために検証ステップが実行されます。 特定のフィーチャーやパッケージのためのカスタム検証ステップを作成することもできます。 詳細については、「[方法:SharePoint ソリューションのフィーチャーとパッケージのカスタム検証規則を作成する](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md)」を参照してください。

## <a name="deployment-conflict-resolution"></a>配置の競合解決
 SharePoint ソリューションを配置する際に、ソリューション パッケージ内の項目と同じ名前、URL、または ID を持つ項目がサーバー上にあると、競合が発生します。 [ **配置の競合の解決** ] プロパティを変更して、モジュール、Web パーツ、リストインスタンス、およびコンテンツタイプの競合を解決、報告、または無視することができます。

 次の表は、"展開の **競合の解決** " プロパティの設定を示しています。

|値|説明|
|-----------|-----------------|
|自動|競合を検出して自動的に解決します。|
|Prompt|競合を検出し、解決する前に開発者に報告します。|
|なし|競合を検出しません。|

## <a name="differences-between-f5-deployment"></a>F5 配置の違い
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] を使用してテストおよびデバッグのために SharePoint プロジェクトをローカル SharePoint サーバーに配置する際に、いくつかの追加の手順が [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって実行されます。

1. 配置手順の間にインターネット インフォメーション サービス (IIS) がリセットされます。

2. ワークフローが自動的に関連付けられます。

3. パッケージ デザイナーの階層構造に従ってフィーチャーのアクティブ化の順序が設定されます。

   カスタムの配置手順を追加して、 **F5** の動作をさらに変更することができます。 詳細については、「 [チュートリアル: SharePoint プロジェクトのカスタム配置手順を作成する](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)」を参照してください。

## <a name="delay-displaying-sharepoint-page-when-deploy-visual-web-part"></a>視覚的 web パーツの配置時に SharePoint ページを表示する遅延
 [!INCLUDE[wiprlhext](../sharepoint/includes/wiprlhext-md.md)]、[!INCLUDE[win7](../sharepoint/includes/win7-md.md)]、または [!INCLUDE[winsvr08](../sharepoint/includes/winsvr08-md.md)] の Bin フォルダーに可視 Web パーツを配置するときに、SharePoint ページの表示に時間がかかります。 これは、Bin ディレクトリなどの最上位の [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] ディレクトリのファイルを変更すると Web アプリケーション全体が再コンパイルされるためです。 結果として、SharePoint ページの表示に最大で 25 秒の遅延が生じます。

### <a name="error-message"></a>エラー メッセージ
 [なし] :

### <a name="resolution"></a>解像度
 この問題を回避するには、次の手順を実行します。

1. Microsoft サポートの記事で説明されているように、update KB967535 をインストールします [。 Windows Vista および Windows Server 2008 の IIS 7.0 で、ASP.NET の2つの問題を修正する修正プログラムを利用でき](https://support.microsoft.com/help/967535)ます。

2. 次の行を Web.config ファイルに追加します。

    ```xml
    <compilation batch="false" optimizeCompilations="true">
    ```

## <a name="sharepoint-project-deployment-fails-with-error-failed-to-extract-the-cab-file-in-the-solution"></a>SharePoint プロジェクトの配置が失敗し、"ソリューションで cab ファイルを抽出できませんでした" というエラーが発生する
 いずれかの SharePoint プロジェクト項目の名前にかっこが含まれると、そのソリューションの配置は次のエラーで失敗します。

### <a name="error-message"></a>エラー メッセージ
 配置手順 'ソリューションの追加' でエラーが発生しました: ソリューションで cab ファイルを抽出できませんでした

### <a name="resolution"></a>解像度
 この問題を回避するには、SharePoint プロジェクト項目の名前に含まれるかっこを削除してください。

## <a name="error-appears-when-deploying-a-visual-web-part-to-a-site-on-a-different-web-application"></a>別の web アプリケーションのサイトに視覚的 web パーツを配置するときにエラーが表示される
 可視 Web パーツの SiteUrl プロパティを変更することで、Web アプリケーション上のサイトに現在配置されているものとは異なる可視 Web パーツを初めて配置するときに、エラーが発生します。

### <a name="error-message"></a>エラー メッセージ
 配置手順 'ソリューションの追加' でエラーが発生しました: ID [#] の機能は既にこのファームにインストールされています。 機能を明示的に再インストールするには、force 属性を使用してください。

### <a name="resolution"></a>解像度
 このエラーは、可視 Web パーツ フィーチャーが SharePoint で取り消される方法によって発生します。 視覚的 Web パーツを正常に配置するには、F5 キーを **押し** てソリューションを再度配置します。

## <a name="warning-appears-when-deploying-nested-user-controls"></a>入れ子になったユーザーコントロールを配置するときに警告が表示される
 この警告は、ユーザー コントロールを含む可視 Web パーツや、可視 Web パーツや別のユーザー コントロールを含むユーザー コントロールなどの、入れ子になったユーザー コントロールが存在する SharePoint ソリューションを配置したときに発生します。 この警告は、コントロールを [ツールボックス] からドラッグするか、またはソースビューのディレクティブを使用してデザイナーに追加した場合に発生し @Register ます。

### <a name="error-message"></a>エラー メッセージ
 警告1要素 ' [*コントロール名*] ' は既知の要素ではありません。 Web サイトにコンパイル エラーがあるか、web.config ファイルが存在しない可能性があります。

### <a name="resolution"></a>解像度
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]入れ子になったユーザーコントロールがプロジェクトシステムで認識されない場合、IntelliSense を提供できず、警告が出力されます。 プロジェクト システムは、プロジェクトがビルドされずにデザイナーが閉じられ、再度開かれた場合、または、デバッグ後に SharePoint ハイブからユーザー コントロールを取り消す自動取り消しオプションが有効な場合は、入れ子になったユーザー コントロールを認識しません。

 この警告を除去するには、プロジェクトをビルドしてからデザイナーを閉じて再度開くか、プロジェクトに対する自動取り消しオプションを無効にします。 これを行うには、[プロジェクトのプロパティ] ダイアログボックスの [ **SharePoint** ] タブで、[**デバッグ後に自動取り消し**] チェックボックスをオフにします。

## <a name="see-also"></a>関連項目

- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)