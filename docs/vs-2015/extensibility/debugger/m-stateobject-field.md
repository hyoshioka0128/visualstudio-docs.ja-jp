---
title: m_stateObject Field |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- m_stateObject field, Task class [.NET Framework debug engines]
ms.assetid: 68c54b22-3e1c-4031-b9c7-b972c519d8a0
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8e9cfc6f689504bef2a8366f90282641d1e9e105
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68149054"
---
# <a name="m_stateobject-field"></a>m_stateObject フィールド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

アクションが使用するデータを表すオブジェクト。  
  
 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **アセンブリ:** mscorlib (mscorlib.dll)  
  
 .NET Framework からこの内部メンバーにアクセスすることはできないため、次の構文は、共通中間言語 (CIL) で提供されています。  
  
## <a name="syntax"></a>構文  
  
```  
.field assembly object m_stateObject  
```  
  
## <a name="remarks"></a>解説  
 これは、 `state` コンストラクターのパラメーターです <xref:System.Threading.Tasks.Task.%23ctor%2A> 。 これは、プロパティのバッキングフィールドでも <xref:System.Threading.Tasks.Task.AsyncState%2A?displayProperty=fullName> あります。  
  
## <a name="see-also"></a>参照  
 [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
