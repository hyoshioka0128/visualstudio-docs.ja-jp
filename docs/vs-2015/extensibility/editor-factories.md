---
title: エディターファクトリ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - editor factories
ms.assetid: cf4e8164-3546-441d-b465-e8a836ae7216
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2de1fc8440bd33a526da62dbb4c7937800484aaa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197758"
---
# <a name="editor-factories"></a>エディター ファクトリ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

エディターファクトリは、エディターオブジェクトを作成し、物理ビューと呼ばれるウィンドウフレームに配置します。 このメソッドは、エディターとデザイナーを作成するために必要なドキュメントデータとドキュメントビューオブジェクトを作成します。 Visual Studio のコアエディターと任意の標準エディターを作成するには、エディターファクトリが必要です。 また、必要に応じて、エディターファクトリを使用してカスタムエディターを作成することもできます。  
  
 エディターファクトリを作成するには、インターフェイスを実装し <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> ます。 次の例は、を実装してエディターファクトリを作成する方法を示してい <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> ます。  
  
 [!code-csharp[VSSDKEditorFactories#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkeditorfactories/cs/vssdkeditorfactoriespackage.cs#1)]
 [!code-vb[VSSDKEditorFactories#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkeditorfactories/vb/vssdkeditorfactoriespackage.vb#1)]  
  
 エディターは、そのエディターによって処理されるファイルの種類を初めて開いたときに読み込まれます。 特定のエディターまたは既定のエディターを開くことを選択できます。 既定のエディターを選択した場合は、統合開発環境 (IDE) によって適切なエディターが決定され、開いて開くことができます。 詳細については、「 [プロジェクト内でファイルを開くエディターの決定](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)」を参照してください。  
  
## <a name="registering-editor-factories"></a>登録 (エディターファクトリを)  
 作成したエディターを使用するには、まず、処理可能なファイル拡張子を含む、そのエディターに関する情報を登録しておく必要があります。  
  
 VSPackage がマネージコードで記述されている場合は、VSPackage が読み込まれた後に、Managed Package Framework (MPF) メソッドを使用して <xref:Microsoft.VisualStudio.Shell.Package.RegisterEditorFactory%2A> エディターファクトリを登録できます。 VSPackage がアンマネージコードで記述されている場合は、サービスを使用してエディターファクトリを登録する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterEditors> ます。  
  
### <a name="registering-an-editor-factory-by-using-managed-code"></a>マネージコードを使用したエディターファクトリの登録  
 VSPackage のメソッドにエディターファクトリを登録する必要があり `Initialize` ます。 最初に `base.Initialize` を呼び出し、次 <xref:Microsoft.VisualStudio.Shell.Package.RegisterEditorFactory%2A> に各エディターファクトリに対してを呼び出します。  
  
 マネージコードでは、VSPackage がこれを処理するため、エディターファクトリの登録を解除する必要はありません。 また、エディターファクトリがを実装している場合は、 <xref:System.IDisposable> 登録が解除されると自動的に破棄されます。  
  
### <a name="registering-an-editor-factory-by-using-unmanaged-code"></a>アンマネージコードを使用したエディターファクトリの登録  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>エディターパッケージの実装で、メソッドを使用してを `QueryService` 呼び出し `SVsRegisterEditors` ます。 この操作を行うと、へのポインターが返さ <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors> れます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A>インターフェイスの実装を渡すことによって、メソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> ます。 別のクラスで m する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> ます。  
  
## <a name="the-editor-factory-registration-process"></a>エディターファクトリの登録プロセス  
 エディターファクトリを使用して Visual Studio がエディターを読み込むと、次の処理が行われます。  
  
1. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]プロジェクトシステムがを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> ます。  
  
2. このメソッドは、エディターファクトリを返します。 ただし、Visual Studio では、プロジェクトシステムで実際にエディターが必要になるまで、エディターのパッケージの読み込みが遅れることがあります。  
  
3. プロジェクトシステムでエディターが必要な場合、Visual Studio は <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 、ドキュメントビューとドキュメントデータオブジェクトの両方を返す特殊なメソッドを呼び出します。  
  
4. ドキュメントデータオブジェクトとドキュメントビューオブジェクトの両方を返すを使用して、Visual Studio によってエディターファクトリに対して呼び出しが行われた場合、Visual Studio はドキュメントウィンドウを作成し、ドキュメント <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> ビューオブジェクトをその中に配置して、ドキュメントデータオブジェクトに対して実行中のドキュメントテーブル (RDT) にエントリを作成します。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>   
 [ドキュメント テーブルの実行](../extensibility/internals/running-document-table.md)
