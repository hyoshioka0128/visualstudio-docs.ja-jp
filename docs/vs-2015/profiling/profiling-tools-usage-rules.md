---
title: プロファイリング ツールの使用に関する規則 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: afa7db3b-8c1d-473a-81ac-24ede112a17f
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4158a6a393ed6e64dedddfca10c1ae04a95e3d3a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535552"
---
# <a name="profiling-tools-usage-rules"></a>プロファイリング ツールの使用に関する規則
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プロファイリング ツールの使用カテゴリのパフォーマンス規則は、プロファイラーを使用してデータを最も効率よく収集する方法に関するガイダンスを提供します。  
  
|ルール|説明|  
|-|-|  
|[DA0002:VSPerfCorProf.dll がありません](../profiling/da0002-vsperfcorprof-dll-is-missing.md)|コマンド ライン プロファイリングに、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] バイナリに関する不完全なデータが含まれている可能性があります。 正しい環境変数が設定されていないことが原因である場合があります。|  
|[DA0003:カーネル サンプルが多数存在します](../profiling/da0003-many-kernel-samples.md)|対象バイナリの実行と無関係なプロファイリング サンプルが多数生成され、記録されました。 より正確なデータを収集するには、インストルメンテーション メソッドの使用をご検討ください。|  
|[DA0004:プロセッサ使用率が高くなっています](../profiling/da0004-high-processor-usage.md)|プロファイル データは、プロファイリングの実行中にプロセッサが常にビジー状態であったことを示しています。 より正確なデータを収集するには、サンプリング メソッドの使用をご検討ください。|  
|[DA0008:少数のサンプルしか収集されていません](../profiling/da0008-few-samples-collected.md)|プロファイリングの実行時に収集されたサンプルの数が、統計的に有意な数には足りませんでした。 もう一度プロファイリングを実行し、これまでよりも長い時間アプリケーションを実行することをご検討ください。 インストルメンテーション メソッドを使用してデータを収集することも検討できます。|  
|[DA0026: 過剰なカーネル CPU 処理時間](../profiling/da0026-excessive-kernel-cpu-time-processing.md)|プロセッサのカーネル モードで、プロファイリングの実行に非常に時間がかかりました。 サンプリングで、時間をメトリックとして使用するのではなく、システム コールをメトリックとして使用することをご検討ください。|  
|[DA0029:サポートされていない CLR バージョンです](../profiling/da0029-unsupported-clr-version.md)|プロファイリングされるバイナリが、プロファイラーでサポートされないバージョンの [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] を使用しています。 プロファイラー レポートはシンボル名を解決できません。|  
|[DA0030: データベース プロジェクトの階層の相互作用の測定を収集します](../profiling/da0030-gather-tier-interaction-measurements-for-database-projects.md)|<xref:System.Data?displayProperty=fullName> 名前空間で多数のメソッドの呼び出しが収集されました。 データベース呼び出しに関するデータを含めるには、プロファイリングの実行時に階層相互作用データを収集することをご検討ください。|
