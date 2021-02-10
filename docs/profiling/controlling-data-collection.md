---
title: データ コレクションの制御 | Microsoft Docs
description: プロファイリング ツールのデータ収集を開始および停止する方法と、プロファイリング データを収集するオブジェクトを制限する方法について学習します。 この記事は概要です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- advanced tasks for profiling tools
- profiling tools, advanced tasks
ms.assetid: e713ad63-b948-46f3-8db9-59b30922ebe5
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 1ca23b5477cee37154f1334328745a5d2b066b39
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99910734"
---
# <a name="control-data-collection"></a>データ収集の制御
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイリング ツールを使用すると、パフォーマンス セッション中のプロファイリング データを収集するタイミングを制御し、プロファイリングする関数を指定することができます。 ここでは、**[パフォーマンス エクスプローラー]** ウィンドウおよび **[データ収集コントロール]** ウィンドウからデータ収集を開始および停止する方法と、プロファイリング データを収集するオブジェクトを制限する方法について説明します。

## <a name="common-tasks"></a>一般的なタスク

|タスク|関連コンテンツ|
|----------|---------------------|
|**プロファイリングの開始および停止:** アプリケーションのプロファイリングは、アプリケーションの起動時または既に実行中のプロセスにプロファイラーをアタッチすることで開始できます。 ターゲット アプリケーションの実行中は、データ コレクションを一時停止したり、再開することができます。 プロファイル セッションを終了するには、ターゲット アプリケーションを終了するか、プロファイラーを実行中のプロセスからデタッチします。|-   [方法: パフォーマンス データの収集の開始と終了](../profiling/how-to-start-and-end-performance-data-collection.md)<br />-   [方法: 実行中のプロセスに対するパフォーマンス ツールのアタッチとデタッチ](../profiling/how-to-attach-and-detach-performance-tools-to-running-processes.md)<br />-   [方法: パフォーマンス データ収集の一時停止と再開](../profiling/how-to-pause-and-resume-performance-data-collection.md)|
|**収集データを制限するようにインストルメンテーション プロファイリングを構成:** パフォーマンス セッションの構成プロパティを使用して、インストルメンテーション メソッドを使用するプロファイリング実行で収集されるデータを制限できます。 特定の .dll ファイル、名前空間、クラス、および関数を含めたり、除外することができます。 さらに、指定したサイズのしきい値に満たない関数を除外することもできます。|-   [方法: インストルメンテーションを特定の DLL に制限する](../profiling/how-to-limit-instrumentation-to-specific-dlls.md)<br />-   [方法: インストルメンテーションを特定の関数に制限する](../profiling/how-to-limit-instrumentation-to-specific-functions.md)<br />-   [方法: インストルメンテーションで短い関数を除外または含める](../profiling/how-to-exclude-or-include-short-functions-from-instrumentation.md)|

## <a name="related-sections"></a>関連項目
- [パフォーマンス セッションの構成](../profiling/configuring-performance-sessions.md)

## <a name="see-also"></a>関連項目
- [パフォーマンス エクスプローラー](../profiling/performance-explorer.md)
