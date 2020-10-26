---
title: '方法: SharePoint フィーチャーをカスタマイズする |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.FeatureDesigner.SwitchView
- VS.SharePointTools.RAD.featureDesigner.Manifest
- VS.SharePointTools.RAD.FeatureDesignerProperties
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a330f3c4cbe1e410ddc6a1612796c92eeda281b8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86016894"
---
# <a name="how-to-customize-a-sharepoint-feature"></a>方法: SharePoint 機能をカスタマイズする
  SharePoint 機能は、Visual Studio のフィーチャーデザイナーを使用して作成およびカスタマイズできます。 たとえば、機能のスコープを設定し、その他の機能を依存関係として追加できます。 既定では、ソリューションエクスプローラーまたは SharePoint パッケージエクスプローラーに新しい機能を追加すると、フィーチャーデザイナーが開きます。

## <a name="opening-the-feature-designer"></a>フィーチャーデザイナーを開く
 フィーチャーデザイナーを使用して、SharePoint プロジェクトアイテムをフィーチャーに追加または削除できます。

#### <a name="to-open-the-feature-designer"></a>フィーチャーデザイナーを開くには

1. **ソリューションエクスプローラー**で、[**機能**] を展開します。

2. *Feature1.feature*項目をダブルクリックするか、 *feature1.feature*項目のショートカットメニューを開き、[**デザイナーの表示**] をクリックします。

## <a name="view-the-packaged-manifest-file"></a>パッケージ化されたマニフェストファイルを表示する
 フィーチャーデザイナーを使用して、機能のパッケージ化されたマニフェストファイル (*feature.xml*) を変更および生成できます。 その後、Visual Studio でこのファイルの XML コードを表示できます。

#### <a name="to-view-the-packaged-manifest-file"></a>パッケージ化されたマニフェストファイルを表示するには

1. **フィーチャーデザイナー**で、[**マニフェスト**] タブを選択します。

#### <a name="to-view-the-packaged-manifest-file-by-using-solution-explorer"></a>ソリューションエクスプローラーを使用してパッケージマニフェストファイルを表示するには

1. **ソリューションエクスプローラー**で、[**すべてのファイルを表示**] アイコンを選択します。

2. [機能] を展開し、[FeatureName]、[FeatureName] の順に展開して、 * \<FeatureName>.Template.xml*ファイルを開きます。

    > [!NOTE]
    > フィーチャーテンプレートマニフェスト XML ファイルを開くと、ファイルは自動的に検証され、[エラー一覧] ウィンドウに表示される警告は無視できます。

## <a name="change-the-manifest-template"></a>マニフェストテンプレートを変更する
 フィーチャーマニフェストファイルの XML コードを変更するには、Visual Studio の XML エディターまたは [マニフェストテンプレート] ペインを使用します。 XML コードに対する変更は、その機能のパッケージマニフェストファイルにマージされます。 たとえば、機能プロパティをカスタマイズするためにマニフェストテンプレートを変更することができます。

#### <a name="to-change-the-manifest-template-by-using-the-xml-editor"></a>XML エディターを使用してマニフェストテンプレートを変更するには

1. **フィーチャーデザイナー**で [**マニフェスト**] タブを選択し、[**編集オプション**] ノードを展開して、[ **XML エディターで開く**] リンクをクリックします。

     XML への変更は、パッケージマニフェストファイルにマージされます。

#### <a name="to-change-the-manifest-template-by-using-the-manifest-template-pane"></a>マニフェストテンプレートペインを使用してマニフェストテンプレートを変更するには

1. **フィーチャーデザイナー**で [**マニフェスト**] タブを選択し、[**編集オプション**] ノードを展開して、[マニフェストテンプレート] ペインに表示される XML を変更します。

     XML への変更は、[ **パッケージマニフェストのプレビュー** ] ペインに表示されます。

## <a name="overwrite-the-packaged-manifest-file"></a>パッケージ化されたマニフェストファイルを上書きする
 フィーチャーデザイナーを無効にして、 *feature.xml* ファイルを手動で作成することができます。 この手順を初めて実行すると、フィーチャーデザイナーの現在の設定が機能テンプレート XML ファイルに保存されます。 その後、XML コードを変更または上書きできます。

> [!NOTE]
> フィーチャーデザイナーの無効化中に XML ファイル内の SharePoint プロジェクト項目を追加または削除した場合、これらのプロジェクト項目はパッケージ化されません。

#### <a name="to-overwrite-packaged-manifest-file-by-disabling-the-designer"></a>デザイナーを無効にしてパッケージマニフェストファイルを上書きするには

1. **フィーチャーデザイナー**で、[**マニフェスト**] タブを選択します。

2. [ **編集オプション** ] ノードを展開し、[ **xml エディター] リンクで [生成された xml を上書きしてマニフェストを編集** する] を選択し、[ **はい** ] をクリックします。

     テンプレートは、現在のパッケージマニフェストファイルで更新されます。

## <a name="enable-the-feature-designer"></a>機能デザイナーを有効にする
 フィーチャーデザイナーを再度有効にして、 *feature.xml* ファイルをカスタマイズできます。

#### <a name="to-re-enable-the-designer"></a>デザイナーを再び有効にするには

1. **フィーチャーデザイナー**で、[マニフェストの**編集を破棄**] を選択し、デザイナーのリンクを再度有効にして、[**はい**] をクリックします。

2. テンプレートは元のテキストで更新され、XML に対する変更はすべて失われます。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
