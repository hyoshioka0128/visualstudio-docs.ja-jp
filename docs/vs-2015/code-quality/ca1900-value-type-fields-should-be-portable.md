---
title: 'CA1900: 値型フィールドは portable | である必要があります。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1900
- ValueTypeFieldsShouldBePortable
helpviewer_keywords:
- ValueTypeFieldsShouldBePortable
- CA1900
ms.assetid: 1787d371-389f-4d39-b305-12b53bc0dfb9
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 23b5705b7ee81e56945050fe63dd2f086894bd08
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75917927"
---
# <a name="ca1900-value-type-fields-should-be-portable"></a>CA1900: 値型フィールドはポータブルでなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の最新のドキュメントについては、「 [CA1900: 値型フィールドはポータブルである必要があり](/visualstudio/code-quality/ca1900-value-type-fields-should-be-portable)ます」を参照してください。

|||
|-|-|
|TypeName|ValueTypeFieldsShouldBePortable|
|CheckId|CA1900|
|[カテゴリ]|Microsoft. 移植性|
|互換性に影響する変更点|中断-フィールドがアセンブリの外部に表示されるかどうか。<br /><br /> 非互換性-フィールドがアセンブリの外部で参照できない場合。|

## <a name="cause"></a>原因
 このルールでは、64ビットオペレーティングシステム上のアンマネージコードにマーシャリングするときに、明示的なレイアウトで宣言されている構造が正しく配置されていることを確認します。 IA-64 では、アライメントされていないメモリアクセスは許可されません。この違反が修正されない場合、プロセスはクラッシュします。

## <a name="rule-description"></a>規則の説明
 ミスアライメントのあるフィールドを含む明示的なレイアウトを持つ構造体は、64ビットのオペレーティングシステムでクラッシュします。

## <a name="how-to-fix-violations"></a>違反の修正方法
 8バイトより小さいすべてのフィールドには、そのサイズの倍数であるオフセットが必要です。また、8バイト以上のフィールドには、8の倍数であるオフセットが必要です。 もう1つの解決策は、`LayoutKind.Explicit`ではなく `LayoutKind.Sequential` を使用することです (適切な場合)。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この警告は、エラーが発生した場合にのみ抑制する必要があります。
