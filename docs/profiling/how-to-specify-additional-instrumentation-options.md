---
title: 追加のインストルメンテーション オプションを指定する | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.performance.property.advanced
helpviewer_keywords:
- instrumentation, options
- profiling tools, session options
- performance sessions, options
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 42c5500d03e815bad1666da7b52918479715e861
ms.sourcegitcommit: 062615c058d2ff44751e8d0c704ccfa3c5543469
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90851815"
---
# <a name="how-to-specify-additional-instrumentation-options"></a>方法: 追加のインストルメンテーション オプションを指定する

Visual Studio IDE またはコマンド ライン ツールを使用して、バイナリをインストルメント化できます。 IDE 内からバイナリをインストルメント化する場合は、[VSInstr](../profiling/vsinstr.md) ツールに追加のインストルメンテーション オプションを指定することで、インストルメンテーション中に収集されるデータの量を制御できます。 これらのオプションは、セッション レベルまたはターゲット レベルで使用できます。 たとえば、インストルメンテーション プロセスにおいて特定の関数を含めたり除外したりするには、ターゲット レベルで追加のインストルメンテーション オプションを使用します。

> [!IMPORTANT]
> プローブを挿入すると、必ず元のプログラムの動作がわずかに変化します。 この変化により、分析時にオーバーヘッドが発生します。 このオーバーヘッドの概算値を差し引いたとしても、マルチスレッド アプリケーションにおいてタイミング上の影響がわずかに残ります。 [VSInstr](../profiling/vsinstr.md) ツール オプションを使用すると、プロファイリング中のデータ収集を制御できます。

## <a name="to-specify-additional-instrumentation-option"></a>追加のインストルメンテーション オプションを指定するには

1. **パフォーマンス エクスプローラー**で、**パフォーマンス セッション**を選択して右クリックし、 **[プロパティ]** を選択します。

2. **[プロパティ ページ]** で **[詳細]** プロパティをクリックします。

3. **[追加インストルメンテーション オプション]** ボックスにオプションを入力します。

     たとえば、プロファイル レベルを指定するには「/CONTROL:THREAD」と入力します。 オプションの一覧については「[VSInstr](../profiling/vsinstr.md)」をご覧ください。

4. **[OK]** をクリックします。

## <a name="see-also"></a>関連項目

[パフォーマンス セッションの構成](../profiling/configuring-performance-sessions.md)
[コマンド ラインからのプロファイリング](../profiling/using-the-profiling-tools-from-the-command-line.md)
