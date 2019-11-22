---
title: Blend におけるデータの表示 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 87d31b6c-4607-4121-bb7d-cfc80390ab93
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2ed51eaef8594695d4d594401ab9375563525b10
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74294572"
---
# <a name="display-data-in-blend"></a>Blend におけるデータの表示
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ページのレイアウトをカスタマイズする際、デザイナーでサンプル データを表示できます。 サンプル データは最初から、または既存のクラスを使用して生成できます。 また、アプリの実行時にアプリに表示される *ライブ データ* にも接続できます。

 **このトピックの内容**

- [サンプル データの生成](#Scratch)

- [クラスからサンプル データを生成する](#Existing)

- [WPF アプリケーションでライブ データを表示する](#LiveWPF)

- [ストアまたは Phone アプリでライブ データを表示する](#LiveStore)

## <a name="Scratch"></a> サンプル データの生成
 サンプル データを生成するには、XAML ドキュメントを開きます。 In the **Data** panel, choose the **Create sample data**![](../designers/media/30540d76-7256-43ce-b5d9-4b2edf3d339f.png "30540d76-7256-43ce-b5d9-4b2edf3d339f") button, and then choose **New Sample Data**.

 **[データ]** パネルでデータ構造を定義してから、いずれかのページの UI 要素にバインドします。

 ![](../designers/media/496d7ebc-fe46-42f6-95a8-57b0e5be5d49.png "496d7ebc-fe46-42f6-95a8-57b0e5be5d49")

 If you want your sample data to appear in your pages when you run the app, choose **Data source options** ![](../designers/media/ae1fd260-4f84-420d-b196-45fde357d81d.png "ae1fd260-4f84-420d-b196-45fde357d81d"), and then choose **Enable When Running Application**.

 ![](../designers/media/05d5356d-91bb-4e6b-b3f7-29b76852c4b3.png "05d5356d-91bb-4e6b-b3f7-29b76852c4b3")

 **Watch a short video:** ![Configure Installed Features](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Create sample data from scratch](https://www.bing.com/videos/search?q=blend%20data&qs=n&form=QBVR&pq=blend%20data&sc=8-7&sp=-1&sk=#view=detail&mid=F8F2449A76956D480FD2F8F2449A76956D480FD2).

 **Watch a short video:** ![Configure Installed Features](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Mixing up some data binding with Blend](https://www.youtube.com/watch?v=LSwPB6CAvjg).

## <a name="Existing"></a> クラスからサンプル データを生成する
 データの構造を記述するクラスを既に作成した場合は、そこからサンプル データを生成できます。

 To generate sample data from a class, open a XAML document, and then in the **Data** panel, click the **Create sample data**![](../designers/media/30540d76-7256-43ce-b5d9-4b2edf3d339f.png "30540d76-7256-43ce-b5d9-4b2edf3d339f") button, and then click **Create Sample Data from Class**.

 **Watch a short video:** ![Configure Installed Features](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Create sample data from a class](https://channel9.msdn.com/Shows/Inside+Windows+Phone/IWP54--Windows-Phone-Data-Binding-and-the-Magic-of-XAML).

 **Watch a short video:** ![Configure Installed Features](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Mixing up some data binding with Blend](https://www.youtube.com/watch?v=LSwPB6CAvjg).

## <a name="LiveWPF"></a> WPF アプリケーションでライブ データを表示する
 **Watch a short video:** ![Configure Installed Features](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Create an XML data source](https://www.youtube.com/watch?v=RjQueappjqk&feature=youtube_gdata).

## <a name="LiveStore"></a> ストアまたは Phone アプリでライブ データを表示する
 「 [データとファイルの操作 (XAML)](https://msdn.microsoft.com/library/windows/apps/xaml/br229562.aspx)」を参照してください。

## <a name="see-also"></a>参照
 [Blend for Visual Studio を使用して UI を作成する](../designers/creating-a-ui-by-using-blend-for-visual-studio.md)
