---
title: パフォーマンス規則を使用したデータの分析 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 1deed23e-b31b-4714-982f-08ceebfc3096
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: f5af6b366a1181187c23327449ade8e03e30107f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "74778064"
---
# <a name="use-performance-rules-to-analyze-data"></a>パフォーマンス規則を使用したデータの分析
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイリング ツールのパフォーマンスの警告は、プロファイリング対象のアプリケーションにおいてプログラムの実行速度が低下する問題を示します。 警告は、有用なデータを収集するために、収集メソッドを変更する必要があることを示している場合もあります。 パフォーマンスの警告は、プロファイル セッションで自動的に生成されます。 警告は、Visual Studio でプロファイル データ ファイルが開いたときに、 **[エラー一覧]** ウィンドウに表示されます。 **[エラー一覧]** ウィンドウでは、問題が発生しているソース コードを見つけたり、問題の解決方法に関する情報などのエラーの詳細情報を表示したりできます。 また、必要のない警告を無効にすることもできます。

> [!NOTE]
> プロファイラーのパフォーマンス警告はプログラム実行のダイナミック分析によって生成され、コード分析警告との関連はありません。 コード分析で、マネージド コードに対するパフォーマンス警告をソース コードのスタティック分析に基づいて生成することもできます。 詳細については、[マネージド コードの品質の分析](../code-quality/code-analysis-for-managed-code-overview.md)に関するページと「[パフォーマンスの警告](../code-quality/performance-warnings.md)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容
- [方法: パフォーマンスの警告を表示する](../profiling/how-to-view-performance-warnings.md)

 **[エラー一覧]** ウィンドウを開いて、プロファイラーのパフォーマンス警告を表示する方法について説明します。

- [方法: パフォーマンス規則を構成する](../profiling/how-to-configure-performance-rules.md)

 パフォーマンス警告を個別に有効または無効にする方法について説明します。

- [パフォーマンス規則リファレンス](../profiling/performance-rules-reference.md)

 プロファイラーのパフォーマンス警告について詳しく説明します。
