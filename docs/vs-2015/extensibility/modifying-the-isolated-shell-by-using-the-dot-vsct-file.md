---
title: を使用して、分離シェルを変更します。Vsct ファイル |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell, isolated mode%2C .vsct file
ms.assetid: 6d147c2d-10e9-400e-b8ce-5566287b41ba
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8c106a04e809e772ac3b8a77192fb2f101161e9c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194235"
---
# <a name="modifying-the-isolated-shell-by-using-the-vsct-file"></a>.Vsct ファイルを使用した分離シェルの変更
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 分離シェルプロジェクトの UI プロジェクトには、アプリケーションで使用できるアプリケーショングループおよび個々のコマンドを指定できるようにするための、vsct ファイルが含まれています。 次に、変更されていない vsct ファイルからの抜粋を示します。  
  
```  
<!-- <Define name="No_WindowListCommand"/> -->  
<!-- <Define name="No_MoreWindowsCommand"/> -->  
<!-- <Define name="No_PaneNextPaneCommand"/> -->  
<!-- <Define name="No_PanePrevPaneCommand"/> -->  
```  
  
 既定では、ほとんどのコマンドとコマンドグループが含まれています。 コマンドまたはコマンドグループを除外するには、そのコマンドまたはグループのコメントを解除するだけです。  
  
 たとえば、次のペインと前のペインのコマンドを削除するには、とのエントリのコメントを解除し `No_PaneNextPaneCommand` `No_PanePrevPaneCommand` ます。  
  
```  
  
<Define name="No_PaneNextPaneCommand"/> <Define name="No_PanePrevPaneCommand"/>  
  
```  
  
 これらのカスタマイズの詳細な例については、「 [チュートリアル: 基本的な分離シェルアプリケーションの作成](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)」を参照してください。  
  
## <a name="referenced-files"></a>参照ファイル  
 アプリケーションの既定の vsct ファイルは、次のファイルを参照します。 これらのファイルは、Visual Studio SDK のインストールディレクトリの \VisualStudioIntegration\Common\Inc\ サブディレクトリにあります。  
  
|ファイル|説明|  
|----------|-----------------|  
|wbids. h|Web 参照パッケージの UI id。|  
|AppIDCmdUsed 使用されています。 vsct|Visual Studio の主要な UI 要素のコマンドテーブル。|  
|EmulatorCmdUsed|Emacs と Brief エディターのエミュレーション UI 要素のコマンドテーブルです。|  
|Vsdebugguids .h|コマンド、オプションページ、および Visual Studio デバッガーのその他の機能の Guid を定義します。|  
|VsDbgCmdUsed。 vsct|デバッガーのコマンドテーブルです。|  
  
 AppIDCmdUsed. vsct ファイルには、アプリケーションの vsct ファイルで定義されているシンボルに基づく Visual Studio UI 要素が含まれています。  
  
 詳細については、「XML コマンドテーブルのデザイン」 (を参照してください [。Vsct) ファイル](../extensibility/internals/designing-xml-command-table-dot-vsct-files.md) と [VSCT XML スキーマリファレンスを参照](../extensibility/vsct-xml-schema-reference.md)してください。  
  
## <a name="see-also"></a>参照  
 [Visual Studio の分離シェル](../extensibility/visual-studio-isolated-shell.md)
