---
title: ツールウィンドウの登録 |Microsoft Docs
description: ProvideToolWindowVisibilityAttribute を使用して、ツールウィンドウを Visual Studio に登録する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tool windows, registering managed
- tool windows, registering
ms.assetid: 8c8c4a24-3da4-497b-9db2-0ddd7cfbfdd2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 140375c3c708957343762b72102dcb8920628aba
ms.sourcegitcommit: dd96a95d87a039525aac86abe689c30e2073ae87
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97863803"
---
# <a name="register-a-tool-window"></a>ツールウィンドウを登録する
ツールウィンドウは、およびを使用して登録でき <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute>  <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute> ます。

## <a name="example"></a>例

```csharp

[ProvideToolWindow(typeof(PersistedWindowPane), Style = MsVsShell.VsDockStyle.Tabbed, Window = "3ae79031-e1bc-11d0-8f78-00a0c9110057")]
[ProvideToolWindow(typeof(DynamicWindowPane), PositionX=250, PositionY=250, Width=160, Height=180, Transient=true)]
[ProvideToolWindowVisibility(typeof(DynamicWindowPane), /*UICONTEXT_SolutionExists*/"f1536ef8-92ec-443c-9ed7-fdadf150da82")]
[ProvideMenuResource(1000, 1)]
[PackageRegistration(UseManagedResourcesOnly = true)]
[Guid("01069CDD-95CE-4620-AC21-DDFF6C57F012")]
public class PackageToolWindow : Package
{
```

 上記のコードでは、によって <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> `PersistedWindowPane` と `DynamicWindowPane` ツールウィンドウが Visual Studio に登録されます。 永続化されたツールウィンドウはドッキングされ、 **ソリューションエクスプローラー** でタブが付けられます。また、動的ウィンドウには、既定の開始位置とサイズが指定されます。 動的ウィンドウは一時的に作成されます。これは、起動時に作成されないことを示します。 これにより、 `DontForceCreate` システムレジストリのキーに値が書き込ま `ToolWindows` れます。 詳細については、「 [ツールウィンドウの表示構成](/previous-versions/visualstudio/visual-studio-2015/extensibility/tool-window-display-configuration?preserve-view=true&view=vs-2015)」を参照してください。