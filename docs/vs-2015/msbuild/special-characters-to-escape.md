---
title: エスケープする特殊文字 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- special characters to escape
- msbuild, special characters to escape
ms.assetid: 5b5172c3-41e4-4f38-a16f-2aeac831a5fc
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: beeed84db240ecf57ca18dd9aef08622f14b06fc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68161351"
---
# <a name="special-characters-to-escape"></a>エスケープする特殊文字
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

特殊文字は、使用するコンテキストで特別な意味を持つ場合にのみ、エスケープする必要があります。 たとえば、アスタリスク (*) は、項目定義の Include 属性と Exclude 属性、または <xref:Microsoft.Build.Tasks.CreateItem> の呼び出しでのみ、特殊文字となります。 その他のすべての場合において、アスタリスクはリテラルのアスタリスクとして扱われます。 プロジェクト ファイルではアスタリスクをエスケープする必要はありませんが、そのようにしても問題はありません。  
  
 特殊文字の代わりに % *xx* という表記を使用します。ここで、*xx* は ASCII 文字の 16 進値を表します。 たとえば、アスタリスク (*) をリテラル文字として使用するには、値 `%2A` を使用します。  
  
 エスケープする特殊文字の完全な一覧は次のとおりです。  
  
|文字|説明|  
|---------------|-----------------|  
|%|パーセント記号は、メタデータを参照するために使用します。|  
|$|ドル記号は、プロパティを参照するために使用します。|  
|@|アット マークは、項目一覧を参照するために使用します。|  
|(|左かっこは、一覧で使用します。|  
|)|右かっこは、一覧で使用します。|  
|`|アポストロフィは、条件やその他の式で使用します。|  
|;|セミコロンは、リスト区切り記号です。|  
|?|疑問符は、項目の Include/Exclude セクションでファイルの仕様を記述する場合のワイルドカード文字です。|  
|*|アスタリスクは、項目の Include/Exclude セクションでファイルの仕様を記述する場合のワイルドカード文字です。|  
  
## <a name="see-also"></a>参照  
 [方法: MSBuild で特殊文字をエスケープする](../msbuild/how-to-escape-special-characters-in-msbuild.md)   
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)
