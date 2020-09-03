---
title: 相互運用機能アセンブリを使用するコマンドとメニュー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- menus, using interop assemblies
- interop assemblies, using in commands and menus
- commands, handling using interop assemblies
- command handling with interop assemblies
ms.assetid: 8f4af525-39e5-4e69-92c8-d3efabe80bb2
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ad6b324953914df7103d0dec7371199e3cbbd937
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68195051"
---
# <a name="commands-and-menus-that-use-interop-assemblies"></a>相互運用機能アセンブリを使用するコマンドとメニュー
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

相互運用機能アセンブリを使用してメニューとツールバーのコマンドを実装する VSPackage は、次の操作を行う必要があります。  
  
- [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]統合開発環境 (IDE: integrated development environment) がサポートしているコマンドと、現在有効になっているかどうかについて通知します。  
  
- コマンドを処理するためのルール (コントラクト) に従います。  
  
- インターフェイスまたはインターフェイスを使用して、コマンド処理を明示的に実装し <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> ます。  
  
  以下では、これらのタスクを実行する方法について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [相互運用機能アセンブリを使用したコマンドのステータスの特定](../../extensibility/internals/determining-command-status-by-using-interop-assemblies.md)  
 VSPackage がどのコマンドをサポートしているか、および現在有効になっているかどうかを IDE に通知する方法について説明します。  
  
 [相互運用機能アセンブリでのコマンドのコントラクト](../../extensibility/internals/command-contracts-in-interop-assemblies.md)  
 相互運用機能アセンブリを使用してコマンドを実装するすべての Vspackage で使用される基本的なコマンドコントラクトの定義を提供します。  
  
 [実装](../../extensibility/internals/command-implementation.md)  
 VSPackage がコマンドを実装する方法の概要について説明します。  
  
 [相互運用機能アセンブリ コマンド ハンドラーの登録](../../extensibility/internals/registering-interop-assembly-command-handlers.md)  
 VSPackage がコマンドハンドラーを提供することを IDE に通知するために必要なレジストリエントリについて説明します。  
  
## <a name="related-sections"></a>関連項目  
 [利用可能性](../../extensibility/internals/command-availability.md)  
 使用できる VSPackage コマンドと、それらを処理するオブジェクトを決定するために IDE によって使用される条件について説明します。  
  
 [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)  
 コマンドサポートを使用する UI を作成する方法の詳細について説明 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] します。  
  
 [Vspackage のコマンド ルーティング](../../extensibility/internals/command-routing-in-vspackages.md)  
 オブジェクトを適切なコマンド要求に関連付けるために使用されるプロセスの概要です。
