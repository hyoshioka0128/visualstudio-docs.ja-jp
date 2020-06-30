---
title: 'CA1823: 使用されていないプライベートフィールドを回避する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidUnusedPrivateFields
- CA1823
helpviewer_keywords:
- AvoidUnusedPrivateFields
- CA1823
ms.assetid: 614f94f6-0dc7-430f-8124-cb889a4a720f
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 01f2ef59ceb6d10cc33276fdd3e5388f39175f8b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545302"
---
# <a name="ca1823-avoid-unused-private-fields"></a>CA1823:使用されていないプライベート フィールドを使用しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|AvoidUnusedPrivateFields|
|CheckId|CA1823|
|カテゴリ|Microsoft. パフォーマンス|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 このルールは、コード内のプライベートフィールドが存在するが、どのコードパスでも使用されていない場合に報告されます。

## <a name="rule-description"></a>ルールの説明
 アセンブリ内でアクセスされていないと思われるプライベート フィールドが検出されました。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、フィールドを削除するか、そのフィールドを使用するコードを追加します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 このルールからの警告を抑制するのは安全です。

## <a name="related-rules"></a>関連規則
 [CA1812:インスタンス化されていない内部クラスを使用しません](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

 [CA1801:使用されていないパラメーターの確認](../code-quality/ca1801-review-unused-parameters.md)

 [CA1804:使用されていないローカルを削除します](../code-quality/ca1804-remove-unused-locals.md)

 [CA1811:呼び出されていないプライベート コードを使用しません](../code-quality/ca1811-avoid-uncalled-private-code.md)
