---
title: 追加のインストルメンテーション オプションを指定する | Microsoft Docs
description: Visual Studio IDE またはコマンド ライン ツールを使用し、バイナリをインストルメント化する方法について学習します。
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
ms.openlocfilehash: aaa6a222ca320ff9e8e3d117c2218e170d67d683
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2021
ms.locfileid: "98721854"
---
# <a name="how-to-specify-additional-instrumentation-options"></a>方法: 追加のインストルメンテーション オプションを指定する

Visual Studio IDE またはコマンド ライン ツールを使用して、バイナリをインストルメント化できます。 IDE 内からバイナリをインストルメント化する場合は、[VSInstr](../profiling/vsinstr.md) ツールに追加のインストルメンテーション オプションを指定することで、インストルメンテーション中に収集されるデータの量を制御できます。 これらのオプションは、セッション レベルまたはターゲット レベルで使用できます。 たとえば、インストルメンテーション プロセスにおいて特定の関数を含めたり除外したりするには、ターゲット レベルで追加のインストルメンテーション オプションを使用します。

> [!IMPORTANT]
> プローブを挿入すると、必ず元のプログラムの動作がわずかに変化します。 この変化により、分析時にオーバーヘッドが発生します。 このオーバーヘッドの概算値を差し引いたとしても、マルチスレッド アプリケーションにおいてタイミング上の影響がわずかに残ります。 [VSInstr](../profiling/vsinstr.md) ツール オプションを使用すると、プロファイリング中のデータ収集を制御できます。

## <a name="to-specify-additional-instrumentation-option"></a>追加のインストルメンテーション オプションを指定するには

1. **パフォーマンス エクスプローラー** で、**パフォーマンス セッション** を選択して右クリックし、 **[プロパティ]** を選択します。

2. **[プロパティ ページ]** で **[詳細]** プロパティをクリックします。

3. **[追加インストルメンテーション オプション]** ボックスにオプションを入力します。

     たとえば、プロファイル レベルを指定するには「/CONTROL:THREAD」と入力します。 オプションの一覧については「[VSInstr](../profiling/vsinstr.md)」をご覧ください。

4. **[OK]** をクリックします。

## <a name="see-also"></a>関連項目

[パフォーマンス セッションの構成](../profiling/configuring-performance-sessions.md)
[コマンド ラインからのプロファイリング](../profiling/using-the-profiling-tools-from-the-command-line.md)
