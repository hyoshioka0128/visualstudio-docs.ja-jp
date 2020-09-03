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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "74294572"
---
# <a name="display-data-in-blend"></a>Blend におけるデータの表示
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ページのレイアウトをカスタマイズする際、デザイナーでサンプル データを表示できます。 サンプル データは最初から、または既存のクラスを使用して生成できます。 また、アプリの実行時にアプリに表示される *ライブ データ* にも接続できます。

 **このトピックの内容:**

- [サンプル データを作成する](#Scratch)

- [クラスからサンプル データを生成する](#Existing)

- [WPF アプリケーションでライブ データを表示する](#LiveWPF)

- [ストアまたは Phone アプリでライブデータを表示する](#LiveStore)

## <a name="generate-sample-data"></a><a name="Scratch"></a> サンプルデータの生成
 サンプル データを生成するには、XAML ドキュメントを開きます。 **[データ]** パネルで、**[サンプル データの作成]**![](../designers/media/30540d76-7256-43ce-b5d9-4b2edf3d339f.png "作成] 30540d76-7256-43ce-b5d9-4b2edf3d339f") ボタン、**[新しいサンプル データ]** の順に選びます。

 **[データ]** パネルでデータ構造を定義してから、いずれかのページの UI 要素にバインドします。

 ![](../designers/media/496d7ebc-fe46-42f6-95a8-57b0e5be5d49.png "496d7ebc-fe46-42f6-95a8-57b0e5be5d49")

 アプリの実行時にページにサンプル データを表示する場合は、 **[データ ソース オプション]** ![](../designers/media/ae1fd260-4f84-420d-b196-45fde357d81d.png "ae1fd260-4f84-420d-b196-45fde357d81d")を選択してから、 **[アプリケーション実行中に有効にする]** を選択します。

 ![](../designers/media/05d5356d-91bb-4e6b-b3f7-29b76852c4b3.png "05d5356d-91bb-4e6b-b3f7-29b76852c4b3")

 **短いビデオを見る:** ![インストール済みフィーチャーの構成](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon")[サンプルデータをゼロから作成](https://www.bing.com/videos/search?q=blend%20data&qs=n&form=QBVR&pq=blend%20data&sc=8-7&sp=-1&sk=#view=detail&mid=F8F2449A76956D480FD2F8F2449A76956D480FD2)します。

 **短いビデオを見る:** ![インストール済みフィーチャーの構成](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Blend を使用したデータバインドの混在](https://www.youtube.com/watch?v=LSwPB6CAvjg)

## <a name="generate-sample-data-from-a-class"></a><a name="Existing"></a> クラスからサンプルデータを生成する
 データの構造を記述するクラスを既に作成した場合は、そこからサンプル データを生成できます。

 クラスからサンプル データを生成するには、XAML ドキュメントを開いてから、**[データ]** パネルで **[サンプル データの作成]**![](../designers/media/30540d76-7256-43ce-b5d9-4b2edf3d339f.png "作成] 30540d76-7256-43ce-b5d9-4b2edf3d339f") ボタン、**[クラスからのサンプル データの作成]** の順に選択します。

 **短いビデオを見る:** ![インストール済みフィーチャーの構成](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon")[クラスからサンプルデータを作成](https://channel9.msdn.com/Shows/Inside+Windows+Phone/IWP54--Windows-Phone-Data-Binding-and-the-Magic-of-XAML)する

 **短いビデオを見る:** ![インストール済みフィーチャーの構成](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Blend を使用したデータバインドの混在](https://www.youtube.com/watch?v=LSwPB6CAvjg)

## <a name="show-live-data-in-a-wpf-application"></a><a name="LiveWPF"></a> WPF アプリケーションでライブデータを表示する
 **短いビデオを見る:** ![インストール済みフィーチャーの構成](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [XML データソースの作成](https://www.youtube.com/watch?v=RjQueappjqk&feature=youtube_gdata)

## <a name="show-live-data-in-a-store-or-phone-app"></a><a name="LiveStore"></a> ストアまたは Phone アプリでライブデータを表示する
 「 [データとファイルの操作 (XAML)](https://msdn.microsoft.com/library/windows/apps/xaml/br229562.aspx)」を参照してください。

## <a name="see-also"></a>参照
 [Blend for Visual Studio を使用して UI を作成する](../designers/creating-a-ui-by-using-blend-for-visual-studio.md)
