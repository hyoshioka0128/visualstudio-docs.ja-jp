---
title: データをアップロードするストレージを参照する
description: リモート マシンまたは Azure ファイル共有ですべての記憶域を参照して、データのアップロードまたはモデルとログのダウンロードを有効にする方法について説明します。
ms.custom: SEO-VS-2020
author: jillre
ms.author: jillfra
manager: jillfra
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: how-to
ms.workload:
- multiple
ms.openlocfilehash: b145c4acf4047356b8996d09d746679900314f1b
ms.sourcegitcommit: fcfd0fc7702a47c81832ea97cf721cca5173e930
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2020
ms.locfileid: "97726567"
---
# <a name="browse-storage-to-upload-data-or-download-models-and-logs"></a>データのアップロードまたはモデルとログのダウンロードを行うストレージを参照する

リモート マシンまたは Azure のファイル共有ですべての記憶域を参照して、データのアップロードまたはモデルとログのダウンロードを有効にすることができます。 または、特定のジョブのログ出力およびジョブ出力にアクセスする場合は、ジョブ ブラウザーからでもアクセスすることができます。

## <a name="to-access-all-data-on-the-remote-machine-or-file-share"></a>リモート マシンまたはファイル共有上のすべてのデータにアクセスするには

1. **サーバー エクスプローラー** を開きます。
2. リモート マシンまたは Batch AI 計算コンテキストを展開します。
3. **[ストレージ]** を右クリックしてから **[参照]** をクリックします。

    ![サーバー エクスプローラーのスクリーンショット。[リモート マシン] フォルダーが展開されています。 フォルダー ツリーで [ストレージ] が強調されています。コンテキスト メニューで [参照] が選択されています。](media/manage-storage/browse-storage.png)

## <a name="to-access-job-specific-data-on-the-remote-machine-or-file-share"></a>リモート マシンまたはファイル共有上にあるジョブ固有のデータにアクセスするには

1. [[ジョブ履歴]](job-details.md) を開きます。
2. ジョブを選択します。
3. **[作業フォルダー]** をクリックします。あるいは、これらの重要なログ ファイルにすばやくアクセスするために **[StdOut] または [Stderr]** をクリックします。

    ![サーバー エクスプローラーの [ジョブ ブラウザー] ウィンドウのスクリーンショット。 train_mnist ジョブが選択されています。[ジョブ詳細] で [作業フォルダー] リンクが選択されています。](media/manage-storage/job-workingfolder.png)
