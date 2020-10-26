---
title: 'CA1308: 文字列を大文字に正規化する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1308
- NormalizeStringsToUppercase
helpviewer_keywords:
- NormalizeStringsToUppercase
- CA1308
ms.assetid: 7e9a7457-3f93-4938-ac6f-1389fba8d9cc
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: c068fcda7d03ae91435c040d2110d632668d832a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85538737"
---
# <a name="ca1308-normalize-strings-to-uppercase"></a>CA1308:文字列を大文字に標準化します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|NormalizeStringsToUppercase|
|CheckId|CA1308|
|カテゴリ|Microsoft のグローバリゼーション|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 操作は、文字列を小文字に正規化します。

## <a name="rule-description"></a>ルールの説明
 文字列は大文字に正規化する必要があります。 小文字に変換された小さな文字グループは、ラウンドトリップを行うことができません。 ラウンドトリップを行うには、あるロケールから文字データを表す別のロケールに文字を変換し、変換された文字から元の文字を正確に取得することを意味します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 文字列を小文字に変換する操作を変更して、文字列を大文字に変換します。 たとえば、`String.ToLower(CultureInfo.InvariantCulture)` を `String.ToUpper(CultureInfo.InvariantCulture)` に変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 結果に基づいてセキュリティを決定しない場合 (たとえば、UI に表示する場合)、警告メッセージを抑制するのは安全です。

## <a name="see-also"></a>参照
 [グローバリゼーションの警告](../code-quality/globalization-warnings.md)
