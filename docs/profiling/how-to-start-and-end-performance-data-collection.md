---
title: パフォーマンス データの収集の開始と終了 | Microsoft Docs
description: プロファイリングを開始する前に、プロファイリング対象のバイナリをパフォーマンス セッションに追加する方法について学習します。
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.performance.wizard.summarypage
helpviewer_keywords:
- profiling tools, launching sessions
- performance sessions, launching
- performance sessions, ending
- profiling tools, ending sessions
ms.assetid: 9f6eb0d5-d9e9-4bec-b627-445065610bce
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: e28d582dbbe25d587611b6b3174a4d4277887a39
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99920701"
---
# <a name="how-to-start-and-end-performance-data-collection"></a>方法: パフォーマンス データの収集の開始と終了
プロファイリングを開始する前に、プロファイリング対象のバイナリをパフォーマンス セッションに追加する必要があります。 対象を追加するには、**パフォーマンス エクスプローラー** で **[ターゲット]** を右クリックし、 **[ターゲット バイナリの追加]** をクリックします。 **[ターゲット バイナリの追加]** ダイアログ ボックスで、ファイル名を選択して **[開く]** をクリックします。 新しいバイナリが追加されます。

### <a name="to-start-profiling"></a>プロファイリングを開始するには

1. **[パフォーマンス エクスプローラー]** ウィンドウでパフォーマンス セッションの名前を右クリックし、次のいずれかのオプションをクリックします。

    - **[プロファイルを使用して起動]** - アプリケーションを開始し、プロファイリングを即座に開始します。

    - **[プロファイルを一時停止して起動]** - アプリケーションを開始しますが、プロファイリングは開始しません。 プロファイリングを開始するには、 **[データ収集コントロール]** ウィンドウで **[収集の再開]** を選択します。 詳細については、「[方法:パフォーマンス データ収集の一時停止と再開](../profiling/how-to-pause-and-resume-performance-data-collection.md)」を参照してください。

### <a name="to-end-profiling"></a>プロファイリングを終了するには

- プロファイリング セッションを終了する最良の方法は、アプリケーションを終了することです。 プロファイリングをただちに終了するには、**パフォーマンス エクスプローラー** のツール バーで **[停止]** をクリックします。

## <a name="see-also"></a>関連項目
- [データ収集の制御](../profiling/controlling-data-collection.md)
- [方法: パフォーマンス データ収集の一時停止と再開](../profiling/how-to-pause-and-resume-performance-data-collection.md)
