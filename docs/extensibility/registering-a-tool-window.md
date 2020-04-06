---
title: ツール ウィンドウの登録 |マイクロソフトドキュメント
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
ms.openlocfilehash: 2e7971de5ae5301d99147bbfc374dda6b039662a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701595"
---
# <a name="register-a-tool-window"></a>ツール ウィンドウを登録する
ツール ウィンドウは、 と<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute><xref:Microsoft.VisualStudio.Shell.ProvideToolWindowVisibilityAttribute>を使用して登録できます。

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

 上記のコードでは、<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute>と`DynamicWindowPane`ツール`PersistedWindowPane`ウィンドウを Visual Studio に登録します。 永続化されたツール ウィンドウは **、ソリューション エクスプローラ**でドッキングされ、タブ付きにされ、動的ウィンドウには既定の開始位置とサイズが与えられます。 動的ウィンドウは一時的に作成され、スタートアップ時には作成されないことを示します。 これにより、`DontForceCreate`システム レジストリの`ToolWindows`キーに値が書き込まれます。 詳細については、「ツール[ウィンドウの表示設定](/visualstudio/extensibility/tool-window-display-configuration?view=vs-2015)」を参照してください。
