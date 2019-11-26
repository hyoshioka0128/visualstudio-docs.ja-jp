---
title: 'DA0012: リフレクションが頻繁に実行されています | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.rules.DAReflection
- vs.performance.12
- vs.performance.rules.DA0012
- vs.performance.DA0011
ms.assetid: c92a1d76-21fa-426e-8b1b-a3c08e9bcbca
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: deb6d8f759080caf1933c75f1f3f05428d3cff9d
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300296"
---
# <a name="da0012-significant-amount-of-reflection"></a>DA0012: リフレクションが頻繁に実行されています
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ルール Id |DA0012 |  
|Category |。NET Framework Usage |  
|プロファイル方法 |サンプリング |  
|Message |リフレクションを過度に使用している可能性があります。 これは負荷が高い操作です。|  
|ルールの種類 |警告 |  
  
## <a name="cause"></a>原因  
 InvokeMember および GetMember などの System.Reflection メソッドまたは MemberInvoke などの Type メソッドへの呼び出しが、プロファイリング データの大きな割合を占めています。 可能な場合は、事前バインディングを使用するこれらのメソッドを、依存アセンブリのメソッドに置き換えることを検討してください。  
  
## <a name="rule-description"></a>規則の説明  
 リフレクションは、.NET Framework の柔軟な機能です。この機能は、依存ランタイム アセンブリに対してアプリケーションの遅延バインディングを実行したり、実行時に新しい型を作成して動的に実行する場合に使用できます。 ただし、この手法は頻繁に使用したり短いループで呼び出したりすると、パフォーマンスが低下する可能性があります。  
  
 詳細については、MSDN の Microsoft Patterns and Practices (マイクロソフトのパターンと手法) ライブラリの「.NET アプリケーションのパフォーマンスとスケーラビリティの向上」の第 5 章「マネージド コード パフォーマンスの向上」の「[リフレクションと遅延バインディング](https://go.microsoft.com/fwlink/?LinkId=177826)」を参照してください。  
  
## <a name="how-to-investigate-a-warning"></a>警告の調査方法  
 [エラー一覧] ウィンドウに表示されたメッセージをダブルクリックして、プロファイル データの[関数の詳細ビュー](../profiling/function-details-view.md)に移動します。 System.Type メソッドまたは System.Reflection メソッドの呼び出し関数を調べ、.NET リフレクション API を最も頻繁に使用するプログラムのセクションを見つけます。 メタデータを返すメソッドは使用しないでください。 アプリケーションのパフォーマンスが重大である場合、状況によっては遅延バインディングの使用と、実行時の動的な型の作成を行わないようにする必要があります。
