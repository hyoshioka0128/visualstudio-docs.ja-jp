---
title: 方法 - パフォーマンス データの収集の開始と終了 | Microsoft Docs
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
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: eedc7f42f2372452fa2cb96279e8b936bdc15e27
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85331335"
---
# <a name="how-to-start-and-end-performance-data-collection"></a>方法: パフォーマンス データの収集の開始と終了
プロファイリングを開始する前に、プロファイリング対象のバイナリをパフォーマンス セッションに追加する必要があります。 対象を追加するには、**パフォーマンス エクスプローラー**で **[ターゲット]** を右クリックし、 **[ターゲット バイナリの追加]** をクリックします。 **[ターゲット バイナリの追加]** ダイアログ ボックスで、ファイル名を選択して **[開く]** をクリックします。 新しいバイナリが追加されます。

### <a name="to-start-profiling"></a>プロファイリングを開始するには

1. **[パフォーマンス エクスプローラー]** ウィンドウでパフォーマンス セッションの名前を右クリックし、次のいずれかのオプションをクリックします。

    - **[プロファイルを使用して起動]** - アプリケーションを開始し、プロファイリングを即座に開始します。

    - **[プロファイルを一時停止して起動]** - アプリケーションを開始しますが、プロファイリングは開始しません。 プロファイリングを開始するには、 **[データ収集コントロール]** ウィンドウで **[収集の再開]** を選択します。 詳細については、「[方法:パフォーマンス データ収集の一時停止と再開](../profiling/how-to-pause-and-resume-performance-data-collection.md)」を参照してください。

### <a name="to-end-profiling"></a>プロファイリングを終了するには

- プロファイリング セッションを終了する最良の方法は、アプリケーションを終了することです。 プロファイリングをただちに終了するには、**パフォーマンス エクスプローラー**のツール バーで **[停止]** をクリックします。

## <a name="see-also"></a>関連項目
- [データ収集の制御](../profiling/controlling-data-collection.md)
- [方法: パフォーマンス データ収集の一時停止と再開](../profiling/how-to-pause-and-resume-performance-data-collection.md)
