---
title: カスタムユーザーインターフェイス (ソース管理 VSPackage) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- user interface, source control packages
- source control packages, user interface
ms.assetid: f35ddb24-53bf-461e-b34f-7414f657c082
caps.latest.revision: 29
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f03713213ec2e54ed8d82d7528dae12cefab7ebc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68154974"
---
# <a name="custom-user-interface-source-control-vspackage"></a>カスタム ユーザー インターフェイス (ソース管理 VSPackage)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

VSPackage は、Visual Studio のコマンドテーブル (vsct) ファイルを使用して、そのメニュー項目とその既定の状態を宣言します。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]統合開発環境 (IDE: integrated development environment) では、VSPackage が読み込まれるまで、既定の状態でメニュー項目が表示されます。 その後、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドを呼び出して、メニュー項目を有効または無効にします。  
  
 VSPackage は、コマンドのユーザーインターフェイス (UI) コンテキストに応じて VSPackage を自動的に読み込むようにレジストリキーを設定できます。ただし、通常は、ソース管理 VSPackage は特定の UI コンテキストに切り替えるだけではなく、必要に応じて読み込む必要があります。 AutoLoadPackages レジストリキーの詳細については、「 [vspackage の管理](../../extensibility/managing-vspackages.md)」を参照してください。  
  
## <a name="vspackage-ui"></a>VSPackage UI  
 ソース管理パッケージは VSPackage として実装され、の UI は使用しません [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 各ソース管理 VSPackage は、メニュー項目、メニューグループ、ツールウィンドウ、ツールバー、ソース管理 VSPackage に固有のオプションを設定するために必要な UI など、独自の UI 要素を指定する必要があります。 これらの UI 要素は、静的または動的に有効にすることができます。 静的 UI 要素は、vsct ファイルで定義され、VSPackage が読み込まれているかどうかにかかわらず表示されます。 動的 UI 要素は、などの特定のコマンド UI コンテキストによって <xref:EnvDTE.Constants.vsContextNoSolution> 、またはメソッドの呼び出しの結果として表示される場合があり <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> ます。 動的 UI 要素の可視性は、Vspackage の遅延読み込みの方法に準拠しています。  
  
## <a name="ui-constraints-on-source-control-vspackages"></a>ソース管理 Vspackage の UI 制約  
 ソース管理 VSPackage は、読み込まれた後に IDE から削除できないため、VSPackage は非アクティブ状態になる必要があります。 VSPackage がアクティブでなくなったという通知を受信すると、VSPackage はその UI を無効にし、外部の IDE との対話を無視します。 VSPackage のメソッドの実装では <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 、VSPackage がアクティブでない場合にコマンドを非表示にする必要があります。  
  
 すべてのソース管理 VSPackage は、インターフェイスを実装する必要があり `IVsSccProvider` ます。 インターフェイスの2つのメソッドであるとは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A> VSPackage によって実装される必要があります。  
  
 ソース管理 VSPackage は、、、などによって実装されるさまざまな IDE イベントをサブスクライブしている場合があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3> <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> ます。 また、VSPackage は、などのレジストリ対応のコールバックインターフェイスを実装している場合もあり <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> ます。 これらはすべて、非アクティブなときは無視する必要があります。  
  
 次の一覧は、ソース管理 VSPackage のアクティブ状態の影響を受けるインターフェイスを示しています。  
  
- プロジェクトドキュメントイベントを追跡します。  
  
- ソリューションイベント。  
  
- ソリューション永続化インターフェイス。 非アクティブの場合、パッケージは .sln ファイルと .suo ファイルに書き込むことはできません。  
  
- プロパティエクステンダー。  
  
  ソース <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> 管理 VSPackage が非アクティブになっている場合、必須のおよび、およびソース管理に関連付けられているオプションのインターフェイスは呼び出されません。  
  
  IDE が [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 起動すると、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] コマンド UI コンテキストが現在の既定のソース管理 VSPackage ID の id に設定されます。 これにより、アクティブなソースコントロール VSPackage の静的 UI が、実際には VSPackage を読み込まずに IDE に表示されます。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSPackage の呼び出しを行う前に、を介して VSPackage がに登録されるのを一時停止し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider> ます。  
  
  次の表は、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE がさまざまな UI 項目を非表示にする方法についての詳細を示しています。  
  
|UI 項目|説明|  
|-------------|-----------------|  
|メニューとツールバー|ソース管理パッケージでは、最初のメニューとツールバーの表示状態を、 [VisibilityConstraints](../../extensibility/visibilityconstraints-element.md) ファイルの [ソース管理パッケージ ID] に設定する必要があります。 これにより、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSPackage を読み込まずに、メソッドの実装を呼び出さなくても、IDE でメニュー項目の状態を適切に設定でき <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> ます。|  
|ツール ウィンドウ|ソース管理 VSPackage は、非アクティブになったときに所有しているすべてのツールウィンドウを非表示にします。|  
|ソース管理の VSPackage 固有のオプションページ|レジストリキー HKLM\SOFTWARE\Microsoft\VisualStudio\X.Y\ToolsOptionsPages\VisibilityCmdUIContexts を使用すると、オプションページを表示する必要があるコンテキストを VSPackage に設定できます。 このキーの下にあるレジストリエントリを作成するには、ソース管理サービスのサービス ID (SID) を使用して、それに DWORD 値1を割り当てる必要があります。 コンテキストで、ソース管理 VSPackage が登録されているコンテキストで UI イベントが発生すると、アクティブな場合は VSPackage が呼び出されます。|  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider>   
 <xref:EnvDTE.Constants.vsContextNoSolution>   
 [VSPackage の管理](../../extensibility/managing-vspackages.md)
