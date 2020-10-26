---
title: マネージコードの "グローバリゼーション規則" 規則セット |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
ms.assetid: 3c4032ee-0805-4581-8c48-b1827cd6b213
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1630769b5150d9cef7b00e575ac9c555f5bc5be1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667606"
---
# <a name="globalization-rules-rule-set-for-managed-code"></a>マネージド コードの "グローバリゼーション規則" 規則セット
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Microsoft グローバリゼーションルールのルールセットを使用して、アプリケーションのデータが異なる言語、ロケール、およびカルチャで正しく表示されない可能性がある問題に焦点を当てることができます。 アプリケーションがローカライズ、グローバル化、またはその両方である場合は、この規則セットを含める必要があります。

|ルール|説明|
|----------|-----------------|
|[CA1300](../code-quality/ca1300-specify-messageboxoptions.md)|MessageBoxOption を指定します|
|[CA1301](../code-quality/ca1301-avoid-duplicate-accelerators.md)|重複するアクセラレータを使用しません|
|[CA1302](../code-quality/ca1302-do-not-hardcode-locale-specific-strings.md)|ロケール特有の文字列をハードコードしません|
|[CA1303](../code-quality/ca1303-do-not-pass-literals-as-localized-parameters.md)|ローカライズされるパラメーターとしてリテラルを渡さない|
|[CA1304](../code-quality/ca1304-specify-cultureinfo.md)|CultureInfo を指定します|
|[CA1305](../code-quality/ca1305-specify-iformatprovider.md)|IFormatProvider を指定します|
|[CA1306](../code-quality/ca1306-set-locale-for-data-types.md)|データ型のロケールを設定します|
|[CA1307](../code-quality/ca1307-specify-stringcomparison.md)|StringComparison の指定|
|[CA1308](../code-quality/ca1308-normalize-strings-to-uppercase.md)|文字列を大文字に標準化します|
|[CA1309](../code-quality/ca1309-use-ordinal-stringcomparison.md)|順序を示す StringComparison を使用します|
|[CA2101](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)|P/Invoke 文字列引数に対してマーシャリングを指定します|
