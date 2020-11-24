---
title: '[URL の選択] ダイアログボックス (SharePoint 開発)'
description: '[URL ピッカー] ダイアログボックスについて説明します。このダイアログボックスでは、ユーザーは、プロジェクトまたは SharePoint を実行しているローカルサーバーにあるファイルを選択できます。'
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.VWD.URLPicker
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, URL picker
- SharePoint development in Visual Studio, designer
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 584b77ab714cb692069fadd6c6fad50e20d46f80
ms.sourcegitcommit: 02f14db142dce68d084dcb0a19ca41a16f5bccff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "95442535"
---
# <a name="url-picker-dialog-box-sharepoint-development-in-visual-studio"></a>[URL の選択] ダイアログボックス (Visual Studio での SharePoint 開発)
  [URL ピッカー] ダイアログボックスでは、プロジェクトまたは SharePoint を実行しているローカルサーバー上にあるマスターページファイルやイメージファイルなどのファイルを選択できます。

 このダイアログボックスは、プロパティを設定するファイルを選択するオプションがある場合に表示されます。 このダイアログボックスを開くには、[**プロパティ**] ウィンドウのさまざまなプロパティの横にある省略記号ボタン (![ASP.NET Mobile Designer 楕円](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) を選択します。 デザイナーの **ソース** ビューで特定の属性に値を割り当てた場合、省略記号ボタンも IntelliSense プロンプトとして表示されます。

## <a name="uielement-list"></a>UIElement の一覧
 **プロジェクトフォルダー** プロジェクトまたは SharePoint を実行しているローカルサーバーで定義されているフォルダーの一覧を表示します。 [展開] ボタンをクリックしてサブフォルダーを表示します。

 **プロジェクトノードを** 展開して、プロジェクト内のファイルを選択します。 ダイアログボックスで選択可能なものとして表示するには、プロジェクト内のファイルが次の条件を満たしている必要があります。

- ファイルは、マップされたフォルダーに格納されている必要があります。

- ファイルをソリューションパッケージに追加する必要があります。

- ファイルが別のプロジェクトに見つかりません。

  これらの条件を満たしていないファイルを参照する場合は、ファイルのパスを手動で入力する必要があります。

  **サーバー** ノードを展開して、SharePoint を実行しているローカルサーバー上にあるファイルを選択します。 ダイアログボックスで選択可能として表示するには、これらのファイルが次の条件を満たしている必要があります。

- ファイルは、 **画像**、 **レイアウト**、または **コントロールテンプレート** のいずれかのマップされたフォルダーに配置する必要があります。

- ファイルが SharePoint コンテンツデータベースに見つかりません。

  これらの条件を満たしていないファイルを参照する場合は、ファイルのパスを手動で入力する必要があります。

  **フォルダーの内容** 選択したフォルダー内のファイルの一覧を表示します。 ファイルを選択し、[ **OK** ] をクリックしてダイアログボックスを閉じ、選択内容を呼び出したプロセスに送信します。

  **ファイルの種類** 実行中のタスクに適したファイルの一覧から選択できます。

## <a name="see-also"></a>関連項目
- [SharePoint のアプリケーション ページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)
- [SharePoint の Web パーツを作成する](../sharepoint/creating-web-parts-for-sharepoint.md)
- [Web パーツまたはアプリケーション ページの再利用できるコントロールを作成する](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
