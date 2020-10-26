---
title: 'CA1707: 識別子にはアンダースコア | を含めることはできませんMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- IdentifiersShouldNotContainUnderscores
- CA1707
helpviewer_keywords:
- CA1707
- IdentifiersShouldNotContainUnderscores
ms.assetid: 5fb539ef-c304-4323-90c0-b14386da9774
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: fe6b90ef971bd00392381f47860d85f34e10dc26
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85544028"
---
# <a name="ca1707-identifiers-should-not-contain-underscores"></a>CA1707:識別子はアンダースコアを含むことはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の最新のドキュメントについては、「 [CA1707: identifier にアンダースコアを含めることはできません](/visualstudio/code-quality/ca1707-identifiers-should-not-contain-underscores)」を参照してください。

|Item|値|
|-|-|
|TypeName|IdentifiersShouldNotContainUnderscores|
|CheckId|CA1707|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|中断 (アセンブリで発生した場合)<br /><br /> 非中断 (型パラメーターで発生した場合)|

## <a name="cause"></a>原因
 識別子の名前にアンダースコア (_) 文字が含まれています。

## <a name="rule-description"></a>ルールの説明
 名前付け規則では、識別子名にアンダースコア (_) 文字を含めることができません。 このルールは、名前空間、型、メンバー、およびパラメーターを確認します。

 名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、新しいソフトウェア ライブラリを習得するまでの時間を短縮でき、マネージド コード開発の専門家によってライブラリが開発されたという信頼を顧客に与えることができます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 名前からすべてのアンダースコア文字を削除します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="related-rules"></a>関連規則
 [CA1709:識別子では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

 [CA1708:識別子は、大文字と小文字の区別以外にも相違していなければなりません](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)
