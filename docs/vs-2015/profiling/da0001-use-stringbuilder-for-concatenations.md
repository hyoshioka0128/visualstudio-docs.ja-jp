---
title: 'DA0001: StringBuilder を使用して連結してください | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.DA0001
- vs.performance.rules.DAUseStringBuilder
- vs.performance.1
- vs.performance.rules.DA0001
ms.assetid: a7cc7613-ad5f-48c8-bd2b-56372cc12dfc
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cb8da704832031d69156eee8863b689e7956f025
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295958"
---
# <a name="da0001-use-stringbuilder-for-concatenations"></a>DA0001: StringBuilder を使用して連結してください
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の最新のドキュメントについては、「 [DA0001: StringBuilder を使用](https://docs.microsoft.com/visualstudio/profiling/da0001-use-stringbuilder-for-concatenations)した連結」を参照してください。  
  
|||  
|-|-|  
|ルール ID|DA0001|  
|カテゴリ|.NET Framework の使用|  
|プロファイル方法|サンプリング<br /><br /> インストルメンテーション|  
|Message|文字列の連結に StringBuilder を使用することを検討してください。|  
|［メッセージの種類］|［警告］|  
  
## <a name="cause"></a>原因  
 System.String.Concat の呼び出しがプロファイル データの大きな割合を占めています。 <xref:System.Text.StringBuilder> クラスを使用して、複数のセグメントからの文字列を連結することを検討してください。  
  
## <a name="rule-description"></a>規則の説明  
 <xref:System.String> オブジェクトは、変更できません。 このため、文字列に変更を加えると、新しい文字列オブジェクトと元のオブジェクトのガベージ コレクションが作成されます。 この動作は、String.Concat を明示的に呼び出しても、+ や += などの文字列連結演算子を使用しても同じです。 これらのメソッドが頻繁に呼び出される場合 (文字列への文字の追加が短いループ内で発生する場合など)、プログラムのパフォーマンスが低下することがあります。  
  
 StringBuilder クラスは System.String とは異なり、変更可能なオブジェクトであるため、このクラスのインスタンスを変更する StringBuilder のメソッドの大多数はその同じインスタンスへの参照を返します。 StringBuilder インスタンスには、文字を挿入したり、テキストを付加することができ、新しいインスタンスを割り当てたり、元のインスタンスを削除しなくても、インスタンスの文字を削除または置換することができます。  
  
## <a name="how-to-investigate-a-warning"></a>警告の調査方法  
 [エラー一覧] ウィンドウに表示されたメッセージをダブルクリックして、サンプリング プロファイル データの[関数の詳細ビュー](../profiling/function-details-view.md)に移動します。 文字列連結を最も頻繁に使用するプログラムをセクションを特定します。 頻繁な文字列連結など、複雑な文字列操作には StringBuilder クラスを使用します。  
  
 文字列の使用方法の詳細については、Microsoft Patterns and Practices (マイクロソフトのパターンと手法) ライブラリの[第 5 章「マネージド コード パフォーマンスの向上](https://go.microsoft.com/fwlink/?LinkId=177816)」の「[文字列処理](https://go.microsoft.com/fwlink/?LinkId=177817)」を参照してください。
