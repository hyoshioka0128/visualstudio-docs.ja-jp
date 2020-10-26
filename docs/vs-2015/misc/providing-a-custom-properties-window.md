---
title: カスタムプロパティウィンドウの提供 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- property browsers, providing
- Properties window, providing your own
ms.assetid: 408dcdef-8ef9-4644-97d2-f311cd35824f
caps.latest.revision: 12
manager: jillfra
ms.openlocfilehash: a244463832ff5620efa74a2c7fd20d6d47d79e76
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62810704"
---
# <a name="providing-a-custom-properties-window"></a>カスタム プロパティ ウィンドウの提供
統合開発環境 (IDE: integrated development environment) によって提供される [**プロパティ**] ウィンドウを拡張するのではなく、特定のプロジェクトシステムの**プロパティ**ウィンドウを独自に用意することができ [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。 最も頻繁に発生するシナリオは、ウィンドウフレームに配置されたオブジェクトを自分で実装する場合です。  
  
 ウィンドウフレームに配置されたオブジェクトを実装せず、他の方法でもアクセスできる場合は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> このページの最後の手順で示したように、インターフェイスにアクセスする方法がいくつかあります。  
  
### <a name="to-provide-your-properties-window"></a>プロパティウィンドウを提供するには  
  
1. [ **プロパティ** ] ウィンドウの実装を表す GUID を定義します。  
  
2. の実装では、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> サービスを使用し <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> て、Visual Studio 環境にサービスとして **プロパティ** ウィンドウを proffer します。  
  
### <a name="to-call-your-properties-window"></a>プロパティウィンドウを呼び出すには  
  
1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane.SetSite%2A> メソッドを呼び出します。  
  
2. `QueryService`<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx> <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> メソッドに渡されるからの <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane.SetSite%2A> 。  
  
3. <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>サービスから取得 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx> します。  
  
4. <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx.OnElementValueChange%2A>最初のパラメーターを (列挙体から取得) に設定し、3番目のパラメーターを使用してを呼び出し `SEID_PropertyBrowserSID` ます。このパラメーターは、 <xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID> `varValue` **プロパティ**ウィンドウを表す GUID の文字列形式を表します。 この呼び出しは、最初に [ **プロパティ** ] ウィンドウのドキュメントウィンドウを作成したときに1回だけ行います。 呼び出しの後に、この [ **プロパティ** ] ウィンドウがウィンドウフレームに関連付けられます。  
  
### <a name="to-obtain-the-window-frame-object-when-you-are-not-the-implementer"></a>実装者ではないときにウィンドウフレームオブジェクトを取得するには  
  
- パラメーターを `QueryService` <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx> に設定して、のサービスを実行でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> `propid` <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID> ます。  
  
- アクティブなドキュメントウィンドウを取得するには、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCurrentSelection%2A> SVsMonitorSelection service を通じてを呼び出します。 `elementid`列挙体から取得したパラメーターをに設定し `SEID_WindowFrame` <xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID> ます。  
  
## <a name="see-also"></a>参照  
 [プロパティの拡張](../extensibility/internals/extending-properties.md)   
 [プロパティ ウィンドウのフィールドとインターフェイス](../extensibility/internals/properties-window-fields-and-interfaces.md)