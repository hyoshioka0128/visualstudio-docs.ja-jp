---
title: 相互運用機能アセンブリを使用してコマンドの状態を確認する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- interop assemblies, determining command status
- command handling with interop assemblies, status
ms.assetid: 2f5104d1-7b4c-4ca0-a626-50530a8f7f5c
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fc67123e082258932ab5df6613941f869d6049a6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196789"
---
# <a name="determining-command-status-by-using-interop-assemblies"></a>相互運用機能アセンブリを使用したコマンドのステータスの特定
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

VSPackage は、処理可能なコマンドの状態を追跡する必要があります。 環境では、VSPackage 内で処理されたコマンドが有効または無効になるタイミングを判断できません。 **切り取り**、**コピー**、**貼り付け**などの一般的なコマンドの状態など、コマンドの状態について環境に通知するのは、VSPackage の役割です。  
  
## <a name="status-notification-sources"></a>状態通知のソース  
 環境は、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> インターフェイスの VSPackage の実装の一部である vspackage ' メソッドを使用して、コマンドに関する情報を受け取り <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ます。 環境は、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 次の2つの条件下で VSPackage のメソッドを呼び出します。  
  
- ユーザーがメインメニューまたはコンテキストメニュー (右クリック) を開くと、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> そのメニューのすべてのコマンドに対してメソッドが実行され、その状態が決定されます。  
  
- VSPackage は、環境が現在のユーザーインターフェイス (UI) を更新することを要求します。 これは、現在ユーザーに表示されているコマンド ([標準] ツールバーの [ **切り取り**]、[ **コピー**]、[ **貼り付け** ] のグループなど) が、コンテキストとユーザーの操作に応じて有効または無効になるためです。  
  
  シェルは複数の Vspackage をホストするため、各 VSPackage をポーリングしてコマンドの状態を確認する必要があった場合、シェルのパフォーマンスが低下する可能性があります。 代わりに、VSPackage は、変更時に UI が変更されたときに環境に対して積極的に通知する必要があります。 更新通知の詳細については、「 [ユーザーインターフェイスの更新](../../extensibility/updating-the-user-interface.md)」を参照してください。  
  
## <a name="status-notification-failure"></a>状態通知エラー  
 VSPackage がコマンドの状態の変更を環境に通知するのに失敗すると、UI が不整合な状態になる可能性があります。 メニューまたはコンテキストメニューのコマンドは、ユーザーがツールバー上に配置できることに注意してください。 そのため、メニューまたはコンテキストメニューが開いている場合にのみ UI を更新するだけでは十分ではありません。  
  
## <a name="see-also"></a>参照  
 [Vspackage のユーザーインターフェイス要素の追加方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [実装](../../extensibility/internals/command-implementation.md)
