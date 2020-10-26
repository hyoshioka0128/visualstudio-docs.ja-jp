---
title: MSBuild ベスト プラクティス | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
helpviewer_keywords:
- best practices, MSBuild
- MSBuild, best practices
ms.assetid: 90ef8693-e921-410a-a377-fe4d13f58c48
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e597b10913ad495193545ab304b3b324d8f66b41
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68181121"
---
# <a name="msbuild-best-practices"></a>MSBuild のベスト プラクティス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

MSBuild スクリプトを記述するための次のベスト プラクティスを推奨します。  
  
- 既定のプロパティ値は、コマンド ラインで既定値をオーバーライドできるプロパティを宣言するのではなく、`Condition` 属性を使用して処理することをお勧めします。 たとえば、次を使用します。  
  
     `<MyProperty Condition="$(MyProperty)" == ''>`  
  
     `MyDefaultValue`  
  
     `</MyProperty>`  
  
- 項目を選択するときに、ワイルドカードを避けます。 代わりに、ファイルを明示的に指定します。 ファイルを追加または削除する場合に発生する可能性のあるエラーを追跡しやすくなります。  
  
## <a name="see-also"></a>参照  
 [高度な概念](../msbuild/msbuild-advanced-concepts.md)
