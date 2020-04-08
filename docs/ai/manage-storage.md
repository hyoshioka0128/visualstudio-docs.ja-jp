---
title: データをアップロードするストレージを参照する
author: jillre
ms.author: jillfra
manager: jillfra
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: conceptual
ms.workload:
- multiple
ms.openlocfilehash: ece3ffa3a273e903f403fd7df7005bfb54172f62
ms.sourcegitcommit: 9c1cecaff4d9955276eee7865b78d47679dd1e2a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/03/2020
ms.locfileid: "80638450"
---
# <a name="browse-storage-to-upload-data-or-download-models-and-logs"></a>データのアップロードまたはモデルとログのダウンロードを行うストレージを参照する

リモート マシンまたは Azure のファイル共有ですべての記憶域を参照して、データのアップロードまたはモデルとログのダウンロードを有効にすることができます。 または、特定のジョブのログ出力およびジョブ出力にアクセスする場合は、ジョブ ブラウザーからでもアクセスすることができます。

## <a name="to-access-all-data-on-the-remote-machine-or-file-share"></a>リモート マシンまたはファイル共有上のすべてのデータにアクセスするには

1. **サーバー エクスプローラー**を開きます。
2. リモート マシンまたは Batch AI 計算コンテキストを展開します。
3. **[ストレージ]** を右クリックしてから **[参照]** をクリックします。

    ![storage](media/manage-storage/browse-storage.png)

## <a name="to-access-job-specific-data-on-the-remote-machine-or-file-share"></a>リモート マシンまたはファイル共有上にあるジョブ固有のデータにアクセスするには

1. [[ジョブ履歴]](job-details.md) を開きます。
2. ジョブを選択します。
3. **[作業フォルダー]** をクリックします。あるいは、これらの重要なログ ファイルにすばやくアクセスするために **[StdOut] または [Stderr]** をクリックします。

    ![storage](media/manage-storage/job-workingfolder.png)
