---
title: プロファイルのコマンド ライン - 移植可能なデータ ファイルの作成
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 2ceb63a7-b835-4988-b756-2afc3fcc4808
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: d0584cd2a476a7552beec483dd72ad1e957800ec
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2020
ms.locfileid: "90808839"
---
# <a name="create-portable-profiling-data-files-from-the-command-line"></a>コマンド ラインからの移植可能なプロファイル データ ファイルの作成
プロファイル データの共有を簡単に行うために、[VSPerfReport](../profiling/vsperfreport.md) コマンドライン ツールを利用し、プロファイリング実行用のシンボルを .*vsp* ファイル内に埋め込むことができます。

 また、サイズが小さく、IDE にすばやく読み込むことのできる解析済みプロファイル データ (.*vsps*) ファイルを作成することもできます。

> [!NOTE]
> シンボル (.*pdb*) ファイルが **VSPerfReport** で利用できることを確認します。 詳細については、「[方法:コマンド ラインからシンボル ファイルの場所を指定する](../profiling/how-to-specify-symbol-file-locations-from-the-command-line.md)」を参照してください。
>
> **VSReport** のパスの詳細については、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関するページをご覧ください。
>
> .*vsps* ファイルのプロファイリング データはフィルター処理できません。

### <a name="to-embed-the-symbols-for-a-profiling-run-into-a-profiling-data-vsp-file"></a>プロファイリング実行のシンボルをプロファイリング データ (.*vsp*) ファイルに組み込むには

- [コマンド プロンプト] ウィンドウで、次のコマンドを入力します。

   \<Path><strong>VSPerfReport \<</strong>VSP File> **/PackSymbols**

   既定では、.*vsps* ファイルには、.*vsp* ファイルのベース名で名前が付けられます。 **Output** オプションを利用し、代替名を指定できます。

### <a name="to-create-a-summary-profiling-data-file"></a>概要プロファイリング データ ファイルを作成するには

- [コマンド プロンプト] ウィンドウで、次のコマンドを入力します。

   \<Path><strong>VSPerfReport \<</strong>VSP File> **/SummaryFile** [ **/Output:** \<File Name>]

   既定では、.*vsps* ファイルには、.*vsp* ファイルのベース名で名前が付けられます。 **Output** オプションを利用し、代替名を指定できます。
