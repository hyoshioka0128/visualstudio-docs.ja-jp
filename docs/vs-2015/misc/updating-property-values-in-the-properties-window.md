---
title: プロパティウィンドウでプロパティ値を更新する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- Properties window, updating property values
- property values, updating in Properties window
ms.assetid: 9358e8c3-b9d2-4fd4-aaab-cf48d1526db4
caps.latest.revision: 9
manager: jillfra
ms.openlocfilehash: 18ecf0a21c5b2d73bdf8e439d25765b6b275cbd9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62434190"
---
# <a name="updating-property-values-in-the-properties-window"></a>[プロパティ] ウィンドウでプロパティ値を更新
**[プロパティ]** ウィンドウをプロパティ値の変更と同期するには、2 つの方法があります。 1 番目の方法は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> インターフェイスを呼び出すことです。このインターフェイスは、環境によって用意されているツール ウィンドウやドキュメント ウィンドウのアクセスや作成を含む、基本的なウィンドウ操作機能へのアクセスを提供します。 次の手順は、この同期プロセスを説明したものです。  
  
## <a name="updating-property-values-using-ivsuishell"></a>IVsUIShell を使ってプロパティ値を更新する  
  
#### <a name="to-update-property-values-using-the-ivsuishell-interface"></a>IVsUIShell インターフェイスを使ってプロパティ値を更新するには  
  
1. VSPackage、プロジェクト、エディターがツール ウィンドウまたはドキュメント ウィンドウを作成したり列挙したりする必要が生じた時点で、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> を (<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> サービスを通じて) 呼び出します。  
  
2. <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.RefreshPropertyBrowser%2A>を実装して、イベントを実装および実行せずに、プロジェクト (または [**プロパティ**] ウィンドウによって参照される他の選択されたオブジェクト) のプロパティの変更とプロパティウィンドウの同期を維持し**Properties** <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> <xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink.OnChanged%2A> ます。  
  
3. <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> のメソッド <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.AdviseHierarchyEvents%2A> および <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.UnadviseHierarchyEvents%2A> を実装します。この 2 つのメソッドは、それぞれ、階層イベントのクライアント通知を設定および無効化します。これにより、階層で <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> を実装する必要がなくなります。  
  
## <a name="updating-property-values-using-iconnection"></a>IConnection を使ってプロパティ値を更新する  
 **[プロパティ]** ウィンドウとプロパティ値の変更を同期する 2 番目の方法は、接続可能なオブジェクトに `IConnection` を実装することにより、発信インターフェイスの存在を示すことです。 プロパティ名をローカライズする場合は、オブジェクトを <xref:System.ComponentModel.ICustomTypeDescriptor> から派生させます。 <xref:System.ComponentModel.ICustomTypeDescriptor> の実装では、実装から返すプロパティ記述子を変更し、プロパティの名前を変更できます。 説明をローカライズするには、<xref:System.ComponentModel.DescriptionAttribute> から派生させた属性を作成し、Description プロパティをオーバーライドします。  
  
#### <a name="considerations-in-implementing-the-iconnection-interface"></a>IConnection インターフェイスを実装する際の考慮事項  
  
1. `IConnection` は、<xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> インターフェイスを持つ列挙子サブオブジェクトへのアクセスを提供します。 また、すべての接続ポイント サブオブジェクトへのアクセスも提供し、それぞれは <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> インターフェイスを実装します。  
  
2. すべての参照オブジェクトは、<xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink> イベントを実装する必要があります。 **[プロパティ]** ウィンドウは、 `IConnection`を通してイベントを設定することをお勧めします。  
  
3. 接続ポイントは、<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.Advise%2A> の実装で許容される接続数 (1 つまたは複数) を制御します。 インターフェイスを 1 つのみ許容する接続ポイントでは、<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.EnumConnections%2A> メソッドから <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> を返すことができます。  
  
4. クライアントは、`IConnection` インターフェイスを呼び出すことにより、<xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> インターフェイスを持つ列挙子サブオブジェクトへのアクセスを取得できます。 その後、<xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> インターフェイスを呼び出すと、各発信インターフェイス ID (IID) の接続ポイントを列挙することができます。  
  
5. また、`IConnection` を呼び出すことにより、各発信 IID への <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> インターフェイスを持つ接続ポイント サブオブジェクトへのアクセスを取得することもできます。 クライアントは、インターフェイスを介して、 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> 接続可能オブジェクトとクライアント独自の同期を使用して、アドバイザリループを開始または終了します。クライアントは、インターフェイスを呼び出して、 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnections> 認識している接続を列挙するためのインターフェイスを持つ列挙子オブジェクトを取得することもできます。  
  
## <a name="see-also"></a>参照  
 [プロパティウィンドウの選択の追跡の発表](../misc/announcing-property-window-selection-tracking.md)   
 [プロパティの拡張](../extensibility/internals/extending-properties.md)