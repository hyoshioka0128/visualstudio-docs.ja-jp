---
title: DA0001 - 連結には StringBuilder を使用してください | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.DA0001
- vs.performance.rules.DAUseStringBuilder
- vs.performance.1
- vs.performance.rules.DA0001
ms.assetid: a7cc7613-ad5f-48c8-bd2b-56372cc12dfc
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 6a645816ed046c2ce253a9f882c1425c48347573
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541740"
---
# <a name="da0001-use-stringbuilder-for-concatenations"></a>DA0001:連結には StringBuilder を使用してください

|アイテム|[値]|
|-|-|
|規則 ID|DA0001|
|カテゴリ|.NET Framework の使用|
|プロファイル方法|サンプリング<br /><br /> インストルメンテーション|
|メッセージ|文字列の連結に StringBuilder を使用することを検討してください。|
|メッセージの種類|警告|

## <a name="cause"></a>原因
 System.String.Concat の呼び出しがプロファイル データの大きな割合を占めています。 <xref:System.Text.StringBuilder> クラスを使用して、複数のセグメントからの文字列を連結することを検討してください。

## <a name="rule-description"></a>規則の説明
 <xref:System.String> オブジェクトは、変更できません。 このため、文字列に変更を加えると、新しい文字列オブジェクトと元のオブジェクトのガベージ コレクションが作成されます。 この動作は、String.Concat を明示的に呼び出しても、+ や += などの文字列連結演算子を使用しても同じです。 これらのメソッドが頻繁に呼び出される場合 (文字列への文字の追加が短いループ内で発生する場合など)、プログラムのパフォーマンスが低下することがあります。

 StringBuilder クラスは System.String とは異なり、変更可能なオブジェクトであるため、このクラスのインスタンスを変更する StringBuilder のメソッドの大多数はその同じインスタンスへの参照を返します。 StringBuilder インスタンスには、文字を挿入したり、テキストを付加することができ、新しいインスタンスを割り当てたり、元のインスタンスを削除しなくても、インスタンスの文字を削除または置換することができます。

## <a name="how-to-investigate-a-warning"></a>警告の調査方法
 **[エラー一覧]** ウィンドウに表示されたメッセージをダブルクリックして、サンプリング プロファイル データの[関数の詳細ビュー](../profiling/function-details-view.md)に移動します。 文字列連結を最も頻繁に使用するプログラムをセクションを特定します。 頻繁な文字列連結など、複雑な文字列操作には StringBuilder クラスを使用します。

 文字列の使用方法の詳細については、Microsoft Patterns and Practices (マイクロソフトのパターンと手法) ライブラリの[第 5 章「マネージド コード パフォーマンスの向上](/previous-versions/msp-n-p/ff647790(v=pandp.10))」の「[文字列処理](/previous-versions/msp-n-p/ff647790(v=pandp.10)#string-operations)」を参照してください。
