---
title: パフォーマンス規則を構成する | Microsoft Docs
description: Visual Studio プロファイル ツールの警告に注意を払ってください。それらから収集メソッドを改善できる場合があります。 それらは [エラー一覧] ウィンドウにあります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.performance.ruleseditor
ms.assetid: a148b468-b849-4858-880a-808a6b47e596
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 788cc8d8a0988740ae78e5b2b21368eb5658ec7a
ms.sourcegitcommit: 589d96700208bf22c8da9e26a1d2041fbf39b8f9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98800337"
---
# <a name="how-to-configure-performance-rules"></a>方法: パフォーマンス規則を構成する
Visual Studio プロファイル ツールのパフォーマンスの警告には、プログラムの実行速度を低下させる可能性があるプロファイリング対象のアプリケーションの問題が示されます。 警告は、有用なデータを収集するために、収集メソッドを変更する必要があることを示している場合もあります。 パフォーマンスの警告は、プロファイル セッションで自動的に生成され、[!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] でプロファイル データ ファイルを開いたときに、 **[エラー一覧]** ウィンドウに表示されます。 ただし、警告によっては、目的のシナリオに当てはまらないものや、誤って生成されるものもあります。 このため、特定の警告を表示または非表示にするよう、パフォーマンスの警告を構成できます。

### <a name="to-configure-profiler-performance-warnings"></a>プロファイラーのパフォーマンス警告を構成するには

1. **[ツール]** メニューの **[オプション]** をクリックします。

2. **[パフォーマンス ツール]** を展開し、 **[規則]** をクリックします。

3. 警告の **[ID]** および名前の隣にあるチェック ボックスをオンまたはオフにすることで、警告を有効または無効にすることができます。

4. 規則の警告レベルを指定するには、規則の横の **[アクション]** セルをクリックして警告レベルをクリックします。

    - **[無効]** - 規則を無効にします (これは、規則 ID の横のチェック ボックスをオフにするのと同じです)。

    - **[警告]** - 規則を警告として表示します。

    - **[エラー]** - プロファイリングの実行を停止し、規則をエラーとして表示します。

    - **[情報]** - 規則を情報としてだけ表示します。
