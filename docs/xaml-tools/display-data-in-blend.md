---
title: XAML UI でサンプル データを視覚化する
titleSuffix: Blend for Visual Studio
ms.date: 03/06/2018
ms.topic: conceptual
ms.assetid: 87d31b6c-4607-4121-bb7d-cfc80390ab93
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c2c71ca21e0d346561435c9cbe079d17dac1d0b5
ms.sourcegitcommit: 3e05bd4bfac6f0b8b3534d8c013388f67e288651
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2020
ms.locfileid: "91959849"
---
# <a name="display-data-in-blend-for-visual-studio"></a>Blend for Visual Studio でデータを表示する

ページのレイアウトをカスタマイズする際、デザイナーでサンプル データを表示できます。 サンプル データは最初から、または既存のクラスを使用して生成できます。 また、アプリの実行時にアプリに表示される*ライブ データ*にも接続できます。

> [!NOTE]
> Blend の [ **データ** ] パネルは、.NET Framework を対象とするプロジェクトでのみサポートされます。 これは、.NET Core を対象とする UWP プロジェクトまたはプロジェクトではサポートされていません。

## <a name="generate-sample-data"></a>サンプル データを作成する

サンプル データを生成するには、XAML ドキュメントを開きます。 **[データ]** パネルで、**[サンプル データの作成]** ![[サンプル データの作成] アイコン](../designers/media/30540d76-7256-43ce-b5d9-4b2edf3d339f.png) ボタンを選択し、**[新しいサンプル データ]** を選びます。

**[データ]** パネルでデータ構造を定義してから、いずれかのページの UI 要素にバインドします。

![データ パネル](../designers/media/496d7ebc-fe46-42f6-95a8-57b0e5be5d49.png)

アプリの実行時にページにサンプル データを表示する場合は、**[データ ソース オプション]** ![[データ ソース オプション] アイコン](../designers/media/ae1fd260-4f84-420d-b196-45fde357d81d.png) を選択し、**[アプリケーション実行中に有効にする]** を選択します。

![[アプリケーション実行中に有効にする] メニュー項目](../designers/media/05d5356d-91bb-4e6b-b3f7-29b76852c4b3.png)

**短いビデオを見る:** ![[再生] アイコン](../designers/media/bldadminconsoleinitialconfigicon.PNG) [サンプル データを新規に作成する](https://www.bing.com/videos/search?q=blend%20data&qs=n&form=QBVR&pq=blend%20data&sc=8-7&sp=-1&sk=#view=detail&mid=F8F2449A76956D480FD2F8F2449A76956D480FD2&preserve-view=true)

## <a name="generate-sample-data-from-a-class"></a>クラスからサンプル データを生成する

データの構造を記述するクラスを既に作成した場合は、そこからサンプル データを生成できます。

クラスからサンプル データを生成するには、XAML ドキュメントを開いてから、**[データ]** パネルで **[サンプル データの作成]** ![[サンプル データの作成] アイコン](../designers/media/30540d76-7256-43ce-b5d9-4b2edf3d339f.png) ボタンをクリックし、**[クラスからのサンプル データの作成]** の順に選択します。

**短いビデオを見る:** ![[再生] アイコン](../designers/media/bldadminconsoleinitialconfigicon.PNG) [Blend を使用していくつかのデータ バインドを組み合わせる](https://www.youtube.com/watch?v=LSwPB6CAvjg)

## <a name="see-also"></a>関連項目

- [Blend for Visual Studio を使用して UI を作成する](../xaml-tools/creating-a-ui-by-using-blend-for-visual-studio.md)