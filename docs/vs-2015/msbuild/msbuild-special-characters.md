---
title: MSBuild の特殊文字 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
helpviewer_keywords:
- escape characters
- escape
- MSBuild Escape Characters
ms.assetid: 545e6a59-1093-4514-935e-78679a46fb3c
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a54f446cb82b3181ee057d4887b37940868a5920
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68150766"
---
# <a name="msbuild-special-characters"></a>MSBuild の特殊文字
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] では、特定の文脈で特別な使い方をするためにいくつかの文字が予約されています。 予約されている文脈でそのような文字を文字通り使用するには、エスケープする必要があります。 たとえば、アスタリスクは、項目定義の `Include` 属性と `Exclude` 属性、ならびに `CreateItem` の呼び出しで特別な意味を持ちます。 このような文脈でアスタリスクをアスタリスクとして表示するには、エスケープする必要があります。 その他の文脈では、アスタリスクを使う場所でそれを入力できます。  
  
 特殊文字をエスケープするには、構文%*xx*を使用します。ここで、 *xx* は文字の ASCII 16 進値を表します。 詳しくは、「[方法 : MSBuild で特殊文字をエスケープする](../msbuild/how-to-escape-special-characters-in-msbuild.md)」をご覧ください。  
  
## <a name="special-characters"></a>特殊文字  
 次の表は、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] の特殊文字をまとめたものです。  
  
|**文字**|**ASCII**|**予約済み使用量**|  
|-------------------|---------------|------------------------|  
|%|%25|メタデータを参照する|  
|$|%24|プロパティを参照する|  
|@|%40|項目一覧を参照する|  
|'|%27|条件とその他の式|  
|;|%3B|一覧の区切り記号|  
|?|%3F|`Include` 属性と `Exclude` 属性のファイル名のワイルドカード文字|  
|*|%2A|`Include` 属性と `Exclude` 属性のファイル名で使用するワイルドカード文字|  
  
## <a name="see-also"></a>参照  
 [高度な概念](../msbuild/msbuild-advanced-concepts.md)   
 [項目](../msbuild/msbuild-items.md)
