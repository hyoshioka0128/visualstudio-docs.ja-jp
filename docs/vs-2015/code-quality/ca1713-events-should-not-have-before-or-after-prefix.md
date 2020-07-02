---
title: 'CA1713: イベントは、before または after prefix | を含むことはできませんMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- EventsShouldNotHaveBeforeOrAfterPrefix
- CA1713
helpviewer_keywords:
- CA1713
- EventsShouldNotHaveBeforeOrAfterPrefix
ms.assetid: 855772a4-aa9e-410b-88c1-c5fba1ca63da
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b05c39a9d8a4a004359baf63919eb427c25fa5d9
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543963"
---
# <a name="ca1713-events-should-not-have-before-or-after-prefix"></a>CA1713:イベントは、before または after プレフィックスを含むことはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|EventsShouldNotHaveBeforeOrAfterPrefix|
|CheckId|CA1713|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 イベントの名前は、' Before ' または ' After ' で始まります。

## <a name="rule-description"></a>ルールの説明
 イベント名には、イベントを発生させるアクションが記述されている必要があります。 特定のシーケンスで発生する関連イベントに名前を付ける場合、現在時制または過去時制を使用して、アクション シーケンスの相対的な位置を示します。 たとえば、リソースを閉じるときに発生するイベントのペアに名前を付ける場合は、' BeforeClose ' や ' AfterClose ' ではなく ' Closed ' と ' Closed ' という名前を付けます。

 名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、新しいソフトウェア ライブラリを習得するまでの時間を短縮でき、マネージド コード開発の専門家によってライブラリが開発されたという信頼を顧客に与えることができます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 イベント名からプレフィックスを削除し、動詞の現在または過去の時制を使用するように名前を変更することを検討してください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。
