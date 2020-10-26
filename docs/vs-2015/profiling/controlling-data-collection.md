---
title: データ コレクションの制御 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- advanced tasks for profiling tools
- profiling tools, advanced tasks
ms.assetid: e713ad63-b948-46f3-8db9-59b30922ebe5
caps.latest.revision: 32
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e34c4db965cacefabe752774e393a4339042040e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68182711"
---
# <a name="controlling-data-collection"></a>データ収集の制御
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロファイリング ツールを使用すると、パフォーマンス セッション中のプロファイリング データを収集するタイミングを制御し、プロファイリングする関数を指定することができます。 ここでは、 **[パフォーマンス エクスプローラー]** ウィンドウおよび **[データ収集コントロール]** ウィンドウからデータ収集を開始および停止する方法と、プロファイリング データを収集するオブジェクトを制限する方法について説明します。  
  
## <a name="common-tasks"></a>一般的なタスク  
  
|タスク|関連コンテンツ|  
|----------|---------------------|  
|**プロファイリングの開始および停止:** アプリケーションのプロファイリングは、アプリケーションの起動時または既に実行中のプロセスにプロファイラーをアタッチすることで開始できます。 ターゲット アプリケーションの実行中は、データ コレクションを一時停止したり、再開することができます。 プロファイル セッションを終了するには、ターゲット アプリケーションを終了するか、プロファイラーを実行中のプロセスからデタッチします。|-   [方法: パフォーマンスデータの収集を開始および終了する](../profiling/how-to-start-and-end-performance-data-collection.md)<br />-   [方法: 実行中のプロセスにパフォーマンスツールをアタッチおよびデタッチする](../profiling/how-to-attach-and-detach-performance-tools-to-running-processes.md)<br />-   [方法: パフォーマンスデータの収集を一時停止および再開する](../profiling/how-to-pause-and-resume-performance-data-collection.md)|  
|**収集データを制限するようにインストルメンテーション プロファイリングを構成:** パフォーマンス セッションの構成プロパティを使用して、インストルメンテーション メソッドを使用するプロファイリング実行で収集されるデータを制限できます。 特定の .dll ファイル、名前空間、クラス、および関数を含めたり、除外することができます。 さらに、指定したサイズのしきい値に満たない関数を除外することもできます。|-   [方法: インストルメンテーションを特定の Dll に制限する](../profiling/how-to-limit-instrumentation-to-specific-dlls.md)<br />-   [方法: インストルメンテーションを特定の関数に制限する](../profiling/how-to-limit-instrumentation-to-specific-functions.md)<br />-   [方法: インストルメンテーションから短い関数を除外または含める](../profiling/how-to-exclude-or-include-short-functions-from-instrumentation.md)|  
  
## <a name="related-sections"></a>関連項目  
 [パフォーマンスセッションの構成](../profiling/configuring-performance-sessions.md)  
  
## <a name="see-also"></a>参照  
 [パフォーマンス エクスプ ローラー](../profiling/performance-explorer.md)
