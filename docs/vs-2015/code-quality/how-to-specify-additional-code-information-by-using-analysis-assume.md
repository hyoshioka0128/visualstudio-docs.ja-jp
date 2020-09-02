---
title: '方法: __analysis_assume | を使用して追加のコード情報を指定するMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- __analysis_assume
helpviewer_keywords:
- __analysis_assume
ms.assetid: 51205d97-4084-4cf4-a5ed-3eeaf67deb1b
caps.latest.revision: 12
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: f2f18c9284ec96de7a7b8663aff485962d194282
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "77277976"
---
# <a name="how-to-specify-additional-code-information-by-using-__analysis_assume"></a>方法: __analysis_assume を使用して追加のコード情報を指定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

C/c + + コードのコード分析ツールにヒントを提供して、分析プロセスを支援し、警告を減らすことができます。 追加情報を提供するには、次の関数を使用します。  
  
 `__analysis_assume(`  `expr`  `)`  
  
 `expr` -true として評価されることを前提とする任意の式。  
  
 コード分析ツールでは、式によって表される条件が、関数が出現する位置で true であることを前提としています。また、変数への代入などによって、式が変更されるまでは true のままです。  
  
> [!NOTE]
> `__analysis_assume` コードの最適化には影響しません。 コード分析ツールの外部で `__analysis_assume` は、は非 op として定義されます。  
  
## <a name="example"></a>例  
 次のコードでは、を使用して `__analysis_assume` 、コード分析の警告 [C6388](../code-quality/c6388.md)を修正します。  
  
```  
#include<windows.h>  
#include<codeanalysis\sourceannotations.h>  
  
using namespace vc_attributes;  
  
// calls free and sets ch to null  
void FreeAndNull(char* ch);  
  
//requires pc to be null  
void f([Pre(Null=Yes)] char* pc);  
  
void test( )  
{  
  char *pc = (char*)malloc(5);  
  FreeAndNull(pc);  
  __analysis_assume(pc == NULL);   
  f(pc);  
}  
```  
  
## <a name="see-also"></a>参照  
 [__assume](https://msdn.microsoft.com/library/d8565123-b132-44b1-8235-5a8c8bff85a7)
