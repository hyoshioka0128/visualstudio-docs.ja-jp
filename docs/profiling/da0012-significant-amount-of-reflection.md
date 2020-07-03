---
title: DA0012 - リフレクションが頻繁に実行されています | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.rules.DAReflection
- vs.performance.12
- vs.performance.rules.DA0012
- vs.performance.DA0011
ms.assetid: c92a1d76-21fa-426e-8b1b-a3c08e9bcbca
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: df8b9c80b3d3b12cb556947a7ca77b3141fb853d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520642"
---
# <a name="da0012-significant-amount-of-reflection"></a>DA0012:リフレクションが頻繁に実行されています

|アイテム|[値]|
|-|-|
|規則 ID|DA0012|
|カテゴリ|.NET Framework の使用|
|プロファイル方法|サンプリング|
|メッセージ|リフレクションを使いすぎている可能性があります。 これは負荷が高い操作です。|
|規則の種類|警告|

## <a name="cause"></a>原因
 InvokeMember および GetMember などの System.Reflection メソッドまたは MemberInvoke などの Type メソッドへの呼び出しが、プロファイリング データの大きな割合を占めています。 可能な場合は、事前バインディングを使用するこれらのメソッドを、依存アセンブリのメソッドに置き換えることを検討してください。

## <a name="rule-description"></a>規則の説明
 リフレクションは、.NET Framework の柔軟な機能です。この機能は、依存ランタイム アセンブリに対してアプリケーションの遅延バインディングを実行したり、実行時に新しい型を作成して動的に実行する場合に使用できます。 ただし、この手法は頻繁に使用したり短いループで呼び出したりすると、パフォーマンスが低下する可能性があります。

 詳細については、MSDN の Microsoft Patterns and Practices (マイクロソフトのパターンと手法) ライブラリの「.NET アプリケーションのパフォーマンスとスケーラビリティの向上」の第 5 章「マネージド コード パフォーマンスの向上」の「[リフレクションと遅延バインディング](/previous-versions/msp-n-p/ff647790(v=pandp.10)#reflection-and-late-binding)」を参照してください。

## <a name="how-to-investigate-a-warning"></a>警告の調査方法
 [エラー一覧] ウィンドウに表示されたメッセージをダブルクリックして、プロファイル データの[関数の詳細ビュー](../profiling/function-details-view.md)に移動します。 System.Type メソッドまたは System.Reflection メソッドの呼び出し関数を調べ、.NET リフレクション API を最も頻繁に使用するプログラムのセクションを見つけます。 メタデータを返すメソッドは使用しないでください。 アプリケーションのパフォーマンスが重大である場合、状況によっては遅延バインディングの使用と、実行時の動的な型の作成を行わないようにする必要があります。
