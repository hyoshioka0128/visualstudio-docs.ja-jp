---
title: AsyncTaskMethodBuilder &lt; TResult &gt; 構造体内部メンバー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- AsyncTaskMethodBuilder<TResult> structure [.NET Framework debug engines]
- debug engines, AsyncTaskMethodBuilder<TResult> structure [.NET Framework]
ms.assetid: 17ebc340-8170-4aff-bf54-dc4548c83632
caps.latest.revision: 5
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7e4999b71ae8f654aa3d362ba16c6cf5bc6574da
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68182262"
---
# <a name="asynctaskmethodbuilderlttresultgt-structure---internal-members"></a>AsyncTaskMethodBuilder &lt; TResult &gt; 構造体の内部メンバー
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このトピックでは、クラスの内部メンバーについて説明し <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601> ます。 このクラスに関する一般的な情報については、リファレンストピックを参照してください <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601> 。  
  
 **名前空間:** <xref:System.Runtime.CompilerServices?displayProperty=fullName>  
  
 **アセンブリ:** mscorlib (mscorlib.dll)  
  
 これらの内部メンバーには .NET Framework からアクセスできないため、次の構文は、共通中間言語 (CIL) で提供されています。  
  
## <a name="syntax"></a>Syntax  
  
```  
.class public sequential ansi sealed beforefieldinit System.Runtime.CompilerServices.AsyncTaskMethodBuilder`1<TResult>  
       extends System.ValueType  
       implements System.Runtime.CompilerServices.IAsyncMethodBuilder  
```  
  
## <a name="internal-members"></a>内部メンバー  
  
|名前|説明|  
|----------|-----------------|  
|[ObjectIdForDebugger プロパティ](../../extensibility/debugger/asynctaskmethodbuilder-tresult-objectidfordebugger-property.md)|デバッガーに対してこのビルダーを一意に識別するために使用できるオブジェクトを取得します。|  
|[m_task フィールド](../../extensibility/debugger/asynctaskmethodbuilder-tresult-m-task-field.md)|遅延初期化されたビルドタスクを表します。|  
  
## <a name="see-also"></a>参照  
 <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601>   
 [.NET Framework の並列拡張機能の内部](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
