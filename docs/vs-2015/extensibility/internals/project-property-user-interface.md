---
title: プロジェクトプロパティのユーザーインターフェイス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project properties [Visual Studio], user interface
- projects [Visual Studio SDK], properties UI
- project properties UI
ms.assetid: b6aec634-8533-476c-9ebd-36536a2288e2
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 31840c40f2a494ffd32f5241e2770938138877e9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704099"
---
# <a name="project-property-user-interface"></a>プロジェクト プロパティのユーザー インターフェイス
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

プロジェクトのサブタイプは、プロジェクトの [ **プロパティページ** ] ダイアログボックスで、基本プロジェクトによって指定されている項目を使用することができます。また、指定どおりに読み取り専用コントロールやページ全体を表示または非表示にしたり、[ **プロパティページ** ] ダイアログボックスにプロジェクトのサブタイプ固有のページを追加したりできます。  
  
## <a name="extending-the-project-property-dialog-box"></a>[プロジェクトプロパティ] ダイアログボックスの拡張  
 プロジェクトのサブタイプは、オートメーションエクステンダーとプロジェクト構成の参照オブジェクトを実装します。 これらのエクステンダー <xref:EnvDTE.IFilterProperties> は、特定のプロパティを非表示または読み取り専用にするためのインターフェイスを実装しています。 基本プロジェクトの [ **プロパティページ** ] ダイアログボックスでは、基本プロジェクトによって実装され、オートメーションエクステンダーによって実行されるフィルター処理が優先されます。  
  
 **プロジェクトプロパティ**ダイアログボックスを拡張するプロセスを次に示します。  
  
- 基本プロジェクトは、インターフェイスを実装することで、プロジェクトのサブタイプからエクステンダーを取得し <xref:EnvDTE80.IInternalExtenderProvider> ます。 基本プロジェクトの [参照]、[プロジェクトオートメーション]、[プロジェクト構成] の各オブジェクトは、このインターフェイスを実装します。  
  
- プロジェクト参照オブジェクトとプロジェクトオートメーションオブジェクトのの実装は、プロジェクトの <xref:EnvDTE80.IInternalExtenderProvider> <xref:EnvDTE80.IInternalExtenderProvider> サブタイプアグリゲーター (つまり、 `QueryInterface` プロジェクトオブジェクトに対する) の実装に対するを実装し <xref:EnvDTE80.IInternalExtenderProvider> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> ます。  
  
- 基本プロジェクト構成の参照オブジェクトは、 <xref:EnvDTE80.IInternalExtenderProvider> プロジェクトのサブタイプ構成オブジェクトからオートメーションエクステンダーに直接接続するためにも実装します。 その実装 <xref:EnvDTE80.IInternalExtenderProvider> は、プロジェクトのサブタイプアグリゲーターによって実装されるインターフェイスに委任されます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject.GetProjectItem%2A>は、プロジェクト構成参照オブジェクトによって実装され、オブジェクトを返し <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> ます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject.GetCfg%2A>は、プロジェクト構成参照オブジェクトによっても実装され、オブジェクトを返し <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg> ます。  
  
- プロジェクトのサブタイプは、次の値を取得することによって、実行時に基本プロジェクトのさまざまな拡張可能なオブジェクトの適切な Catid を特定でき <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> ます。  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>  
  
  - <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>  
  
  プロジェクトスコープの Catid を決定するために、プロジェクトのサブタイプは、の上のプロパティをから取得し <xref:Microsoft.VisualStudio.VSConstants.VSITEMID> `VSITEMID``typedef` ます。 プロジェクトのサブタイプでは、プロジェクトに対して表示される [ **プロパティページ** ] ダイアログボックスのページを制御する必要がある場合もあります。構成依存と構成に依存しません。 一部のプロジェクトのサブタイプでは、組み込みページを削除し、プロジェクトのサブタイプに固有のページを追加する必要がある場合があります。 これを有効にするために、マネージクライアントプロジェクトは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> 次のプロパティのメソッドを呼び出します。  
  
- `VSHPROPID_PropertyPagesCLSIDList` —構成に依存しないプロパティページの Clsid をセミコロンで区切った一覧。  
  
- `VSHPROPID_CfgPropertyPagesCLSIDList —` 構成に依存するプロパティページの Clsid をセミコロンで区切った一覧。  
  
  プロジェクトのサブタイプによってオブジェクトが集約されるため <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 、これらのプロパティの定義をオーバーライドして、どの **プロパティページ** のダイアログボックスを表示するかを制御できます。 プロジェクトのサブタイプは、これらのプロパティを内部基本プロジェクトから取得し、必要に応じて Clsid を追加または削除できます。  
  
  プロジェクトのサブタイプによって追加された新しいプロパティページには、プロジェクト構成の参照オブジェクトが基本プロジェクトの実装から渡されます。 このプロジェクト構成の参照オブジェクトは、オートメーションエクステンダーをサポートしています。 AutomationExtenders の詳細については、「 [オートメーションエクステンダーの実装と使用](https://msdn.microsoft.com/library/0d5c218c-f412-4b28-ab0c-33a611f62356)」を参照してください。 プロジェクトのサブタイプの呼び出しによって実装されるプロパティページでは、 <xref:EnvDTE.Project.Extender%2A> 基本プロジェクトの構成参照オブジェクトを拡張する独自のプロジェクトサブタイプの構成参照オブジェクトを取得します。  
  
## <a name="see-also"></a>参照  
 <xref:EnvDTE.IFilterProperties>   
 [[プロパティページ] ダイアログボックス](https://msdn.microsoft.com/4a3d34ac-ed03-45e8-ae60-a0e1aad300e4)
