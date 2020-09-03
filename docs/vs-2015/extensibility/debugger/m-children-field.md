---
title: m_children Field |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- m_children field, ContingentProperties class [.NET Framework debug engines]
ms.assetid: 0a3b5653-7bc0-4a7a-8963-9020bc52b9cb
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 749b7a8da2cbdf8377e7f2e1fcb39787e2f42303
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68149062"
---
# <a name="m_children-field"></a>m_children フィールド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このタスクに登録されている子タスクの一覧。  
  
 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **アセンブリ:** mscorlib (mscorlib.dll)  
  
 .NET Framework からこの内部メンバーにアクセスすることはできないため、次の構文は、共通中間言語 (CIL) で提供されています。  
  
## <a name="syntax"></a>構文  
  
```  
.field public class System.Collections.Generic.List`1<class System.Threading.Tasks.Task> m_children  
```  
  
## <a name="remarks"></a>解説  
 タスクの実行中は、タスクを実行するスレッドだけがこの配列にアクセスします。  
  
 タスクが完了している場合は、他のスレッドがこのフィールドにアクセスできない限り、他のスレッドがこのフィールドにアクセスできます。  
  
## <a name="see-also"></a>参照  
 [ContingentProperties クラス](../../extensibility/debugger/contingentproperties-class-internal-members.md)
