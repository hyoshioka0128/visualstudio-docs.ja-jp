---
title: 'CA2211: 非定数フィールドを visible にすることはできません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2211
- NonConstantFieldsShouldNotBeVisible
helpviewer_keywords:
- NonConstantFieldsShouldNotBeVisible
- CA2211
ms.assetid: e1e42c40-0acd-4312-af29-70133739a304
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: aa67c33eac5d618c0a080323720775beea7b68c3
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548214"
---
# <a name="ca2211-non-constant-fields-should-not-be-visible"></a>CA2211:非定数フィールドは表示されません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|NonConstantFieldsShouldNotBeVisible|
|CheckId|CA2211|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリックまたはプロテクト静的フィールドは定数ではなく、読み取り専用です。

## <a name="rule-description"></a>ルールの説明
 定数でも読み取り専用でもない静的フィールドは、スレッド セーフではありません。 このようなフィールドへのアクセスは慎重に制御する必要があり、クラスオブジェクトへのアクセスを同期するための高度なプログラミング手法が必要です。 これらは習得して習得するのが困難であるため、このようなオブジェクトをテストすることで独自の課題が生じます。静的フィールドは、変更されないデータを格納するために最適に使用されます。 このルールは、ライブラリに適用されます。アプリケーションでは、フィールドを公開しないでください。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、静的フィールドを定数または読み取り専用にします。 これが不可能な場合は、基になるフィールドへのスレッドセーフなアクセスを管理するスレッドセーフなプロパティなど、別のメカニズムを使用するように型を再設計してください。 ロックの競合やデッドロックなどの問題が、ライブラリのパフォーマンスと動作に影響を与える可能性があることに注意してください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 アプリケーションを開発していて、静的フィールドを含む型へのアクセスを完全に制御できる場合は、この規則による警告を抑制することが安全です。 ライブラリデザイナーは、このルールからの警告を抑制しないでください。非定数の静的フィールドを使用すると、開発者が適切に使用するためにライブラリを使用することが難しくなります。

## <a name="example"></a>例
 次の例は、この規則に違反する型を示しています。

 [!code-csharp[FxCop.Usage.AvoidStaticNonConstants#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.AvoidStaticNonConstants/cs/FxCop.Usage.AvoidStaticNonConstants.cs#1)]
 [!code-vb[FxCop.Usage.AvoidStaticNonConstants#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.AvoidStaticNonConstants/vb/FxCop.Usage.AvoidStaticNonConstants.vb#1)]
