---
title: 'CA1725: パラメーター名は、基本宣言 | と一致しなければなりません。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ParameterNamesShouldMatchBaseDeclaration
- CA1725
helpviewer_keywords:
- CA1725
- ParameterNamesShouldMatchBaseDeclaration
ms.assetid: 9b657ab0-fe81-4f4c-9481-ba746988c922
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: f1fb30cd37ebffcee7619190cef83560813b25db
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85547369"
---
# <a name="ca1725-parameter-names-should-match-base-declaration"></a>CA1725:パラメーター名は基本宣言と同一でなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|ParameterNamesShouldMatchBaseDeclaration|
|CheckId|CA1725|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 外部から参照できるメソッドのオーバーライドのパラメーターの名前が、メソッドの基本宣言内のパラメーターの名前と一致しないか、またはメソッドのインターフェイス宣言内のパラメーターの名前と一致しません。

## <a name="rule-description"></a>ルールの説明
 オーバーライド階層のパラメーターに対する一貫性のある名前付けによって、メソッド オーバーライドの有用性が高まります。 派生メソッドのパラメーター名が基本宣言のパラメーター名と異なる場合、メソッドが基本メソッドのオーバーライドであるか、またはメソッドの新しいオーバーライドであるかについて混乱が生じる可能性があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、基本宣言に一致するようにパラメーターの名前を変更します。 この修正は、COM 参照可能なメソッドの互換性に影響する変更点です。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 以前に出荷されたライブラリ内の COM 参照可能なメソッドを除き、この規則からの警告を抑制しないでください。
