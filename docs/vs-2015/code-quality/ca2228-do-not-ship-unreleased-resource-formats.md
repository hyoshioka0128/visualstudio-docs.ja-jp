---
title: 'CA2228: 未公開: 配布されていないリソース形式 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotShipUnreleasedResourceFormats
- CA2228
helpviewer_keywords:
- CA2228
- DoNotShipUnreleasedResourceFormats
ms.assetid: 2c614edc-4e94-4b4f-8067-eea677a75cd9
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 4adcae1c1cc616cdbcf5a7aa15342d221c2f4300
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540583"
---
# <a name="ca2228-do-not-ship-unreleased-resource-formats"></a>CA2228:未公開のリソース形式を出荷しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DoNotShipUnreleasedResourceFormats|
|CheckId|CA2228|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 リソースファイルは、現在サポートされていないバージョンのを使用してビルドされました [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 。

## <a name="rule-description"></a>ルールの説明
 プレリリース版のを使用してビルドされたリソースファイルは、サポートされている [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] バージョンの .NET Framework では使用できない可能性があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、サポートされているバージョンの k を使用してリソースをビルドし [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。
