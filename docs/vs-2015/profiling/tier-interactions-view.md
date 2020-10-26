---
title: 階層相互作用のビュー | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.view.tierinteraction
helpviewer_keywords:
- Tier Interactions view
ms.assetid: bb4fb21c-f3f7-473a-8b5e-442da4c2c445
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: bd60c855bacaf62beec47c9f977d0ab220ce7ca6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68145545"
---
# <a name="tier-interactions-view"></a>階層相互作用のビュー
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

階層相互作用プロファイリングにより、[!INCLUDE[vstecado](../includes/vstecado-md.md)] を通じてデータベースと通信する多階層アプリケーションでの関数の実行時間に関する追加情報が提供されます。 データは同期の関数呼び出しについてのみ収集されます。  
  
 **必要条件**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]  
  
  相互作用ビューでは、2 つのウィンドウに階層相互作用データが表示されます。  
  
- マスター ウィンドウは階層ツリーです。 最上位の行には、[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ページまたはプロセスのデータベース接続の集計データが含まれています。 子ノードには、親のデータベース接続の集計データが含まれています。  
  
- マスター ウィンドウでデータベース呼び出しノードをクリックすると、データベース呼び出しのインスタンスのデータが詳細ウィンドウに表示されます。  
  
  時間は、ミリ秒数または CPU クロック ティック数として表示されます。 表示される時間単位を変更するには、**[ツール]** メニュー、**[オプション]** の順にクリックして、**[時間の値を次の単位で表示]** オプションのいずれかを選択します。  
  
## <a name="master-pane"></a>マスター ウィンドウ  
  
|列|説明|  
|------------|-----------------|  
|**名前**|- 最上位の行の場合は、プロファイリングされたプロセスまたは Web ページの名前。<br />- データベース接続の行の場合は、データベースをホストするサーバーの名前。|  
|**データベース**|データベースの名前 (データベース接続の行の場合のみ)。|  
|**Count**|プロセス、Web ページ、またはデータベース接続によって生成された要求の合計数。|  
|**経過時間の合計**|プロセス、Web ページ、またはデータベース接続からのいずれか 1 つの要求の実行に費やされた時間の合計。|  
|**最大経過時間**|プロセス、Web ページ、またはデータベース接続からのいずれか 1 つの要求の実行に費やされた時間の最大値。|  
|**最小経過時間**|プロセス、Web ページ、またはデータベース接続からのいずれか 1 つの要求の実行に費やされた時間の最小値。|  
|**平均経過時間**|プロセス、Web ページ、またはデータベース接続からの 1 つの要求の実行に費やされた時間の平均値。|  
  
## <a name="database-connection-details-pane"></a>データベース接続の詳細ウィンドウ  
  
|列|説明|  
|------------|-----------------|  
|**コマンド テキスト**|要求の SQL クエリ。|  
|**クエリ数**|クエリが実行された回数。|  
|**経過時間の合計**|クエリのインスタンスの実行に費やされた時間の合計。|  
|**最大経過時間**|クエリのいずれか 1 つのインスタンスの実行に費やされた時間の最大値。|  
|**最小経過時間**|クエリのいずれか 1 つのインスタンスの実行に費やされた時間の最小値。|  
|**平均経過時間**|クエリの 1 つのインスタンスの実行に費やされた時間の平均値。|
