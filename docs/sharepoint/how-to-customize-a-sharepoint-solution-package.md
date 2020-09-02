---
title: '方法: SharePoint ソリューションパッケージをカスタマイズする |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.PackageDesignerAdvanced
- VS.SharePointTools.RAD.PackageDesigner.Manifest
- VS.SharePointTools.RAD.PackageDesignerProperties
- VS.SharePointTools.RAD.PackageDesigner.SwitchView
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 77b66160d489f711b5588fdcdd024d13769d734f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86016869"
---
# <a name="how-to-customize-a-sharepoint-solution-package"></a>方法: SharePoint ソリューションパッケージをカスタマイズする
  パッケージデザイナーを使用して、パッケージ (*.wsp*) を作成およびカスタマイズできます。 たとえば、SharePoint プロジェクトのアイテムと機能を追加したり、ソリューションの配置時に Web サーバーをリセットするかどうかを指定したり、配置サーバーの種類を設定したりできます。

## <a name="open-the-package-designer"></a>パッケージデザイナーを開く

#### <a name="to-open-the-package-designer"></a>パッケージデザイナーを開くには

- **ソリューションエクスプローラー**で、[**パッケージ**] をダブルクリックするか、**パッケージ**のショートカットメニューの [**デザイナーの表示**] を選択します。

## <a name="view-the-packaged-manifestffile"></a>パッケージ化された manifestfFile を表示する
 パッケージデザイナーを使用して、パッケージ化されたマニフェストファイルを変更および生成できます。 その後、Visual Studio でこのファイルの XML コードを表示できます。

#### <a name="to-view-the-xml-source-file"></a>XML ソースファイルを表示するには

1. **パッケージデザイナー**で、[**マニフェスト**] を選択します。

#### <a name="to-view-the-packaged-manifest-file-by-using-solution-explorer"></a>ソリューションエクスプローラーを使用してパッケージマニフェストファイルを表示するには

1. **ソリューション エクスプローラー**で、**[すべてのファイルを表示]** をクリックします。

2. [パッケージ] を展開し、[パッケージ] を展開して、 *Package.Template.xml* ファイルを開きます。

    > [!NOTE]
    > パッケージテンプレートのマニフェスト XML ファイルを開くと、ファイルは自動的に検証されます。また、[エラー一覧] ウィンドウに表示される警告は無視してかまいません。

## <a name="change-the-manifest-template"></a>マニフェストテンプレートを変更する
 パッケージ化されたマニフェストファイルの XML コードは、Visual Studio の XML エディターまたは [マニフェストテンプレート] ペインで変更できます。 XML コードに対する変更は、パッケージのパッケージマニフェストファイルにマージされます。

#### <a name="to-change-the-manifest-template-by-using-the-xml-editor"></a>XML エディターを使用してマニフェストテンプレートを変更するには

1. **パッケージデザイナー**で [**マニフェスト**] タブを選択し、[**編集オプション**] ノードを展開して、[ **XML エディターで開く**] リンクをクリックします。

     XML への変更は、パッケージマニフェストファイルにマージされます。

#### <a name="to-change-the-manifest-template-by-using-the-manifest-template-pane"></a>マニフェストテンプレートペインを使用してマニフェストテンプレートを変更するには

1. **パッケージデザイナー**で [**マニフェスト**] タブを選択し、[**編集オプション**] ノードを展開して、[マニフェストテンプレート] ペインに表示される XML を変更します。

     XML への変更は、[ **パッケージマニフェストのプレビュー** ] ペインに表示されます。

## <a name="overwrite-the-packaged-manifest-file"></a>パッケージ化されたマニフェストファイルを上書きする
 パッケージデザイナーを無効にして、 *manifest.xml* ファイルを手動で作成することができます。 この手順を初めて実行すると、パッケージデザイナーの現在の設定がパッケージテンプレート XML ファイルに保存されます。 その後、XML コードを変更または上書きできます。

> [!NOTE]
> パッケージデザイナーが無効になっているときに、XML ファイル内の SharePoint プロジェクトの項目および機能を追加または削除した場合、これらのプロジェクトの項目と機能はパッケージ化されません。

#### <a name="to-overwrite-packaged-manifest-file-by-disabling-the-designer"></a>デザイナーを無効にしてパッケージマニフェストファイルを上書きするには

1. **パッケージデザイナー**で、[**マニフェスト**] タブを選択します。

2. [ **編集オプション** ] ノードを展開し、[ **xml エディター] リンクで [生成された xml を上書きしてマニフェストを編集** する] を選択し、[ **はい** ] をクリックします。

     テンプレートは、現在のパッケージマニフェストファイルで更新されます。

## <a name="enable-the-package-designer"></a>パッケージデザイナーを有効にする
 パッケージデザイナーを再度有効にして、 *manifest.xml* ファイルをカスタマイズできます。

#### <a name="to-re-enable-the-designer"></a>デザイナーを再び有効にするには

1. **パッケージデザイナー**で、[マニフェストの**編集を破棄**] を選択し、デザイナーのリンクを再度有効にして、[**はい**] をクリックします。

     テンプレートは元のテキストで更新され、XML に対する変更はすべて失われます。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
