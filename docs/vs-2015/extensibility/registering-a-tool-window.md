---
title: ツールウィンドウの登録 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- tool windows, registering managed
- tool windows, registering
ms.assetid: 8c8c4a24-3da4-497b-9db2-0ddd7cfbfdd2
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8178938715278bf69fe8f4cc1b336bbd19cec04e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62535640"
---
# <a name="registering-a-tool-window"></a>ツール ウィンドウの登録
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ツールウィンドウは、およびを使用して登録できます。 <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute><xref:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute>  
  
## <a name="example"></a>例  
  
```csharp  
  
      [ProvideToolWindow(typeof(PersistedWindowPane), Style = MsVsShell.VsDockStyle.Tabbed, Window = "3ae79031-e1bc-11d0-8f78-00a0c9110057")] [ProvideToolWindow(typeof(DynamicWindowPane), PositionX=250, PositionY=250, Width=160, Height=180, Transient=true)] [ProvideToolWindowVisibility(typeof(DynamicWindowPane), /*UICONTEXT_SolutionExists*/"f1536ef8-92ec-443c-9ed7-fdadf150da82")]  
[ProvideMenuResource(1000, 1)]  
[PackageRegistration(UseManagedResourcesOnly = true)]  
[Guid("01069CDD-95CE-4620-AC21-DDFF6C57F012")]  
public class PackageToolWindow : Package  
{  
```  
  
 上記のコードでは、によって <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> persistedwindowpane がおよび DynamicWindowPane ツールウィンドウが Visual Studio に登録されます。 永続化されたツールウィンドウはドッキングされ、 **ソリューションエクスプローラー**でタブが付けられます。また、動的ウィンドウには、既定の開始位置とサイズが指定されます。 動的ウィンドウは一時的に作成されます。これは、起動時に作成されないことを示します。 これにより、DontForceCreate 値がシステムレジストリの ToolWindows キーに書き込まれます。 詳細については、「 [ツールウィンドウの表示構成](../extensibility/tool-window-display-configuration.md)」を参照してください。
