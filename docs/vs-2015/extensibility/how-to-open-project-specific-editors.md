---
title: '方法: プロジェクト固有のエディターを開く |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project types, opening a project-specific editor
- editors [Visual Studio SDK], opening project-specific editors
- projects [Visual Studio SDK], opening folders
ms.assetid: 83e56d39-c97b-4c6b-86d6-3ffbec97e8d1
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2439a07f63b8da854ca8dc331d26e30f49503257
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842177"
---
# <a name="how-to-open-project-specific-editors"></a>方法: プロジェクト固有のエディターを開く
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プロジェクトによって開かれている項目ファイルが、そのプロジェクトの特定のエディターに本質的にバインドされている場合、プロジェクトはプロジェクト固有のエディターを使用してファイルを開く必要があります。 エディターを選択するための IDE のメカニズムにファイルを委任することはできません。 たとえば、標準のビットマップエディターを使用する代わりに、このプロジェクト固有のエディターオプションを使用して、プロジェクトに固有のファイル内の情報を認識する特定のビットマップエディターを指定できます。  
  
 IDE は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> 特定のプロジェクトでファイルを開く必要があると判断したときに、メソッドを呼び出します。 詳細については、「[ [ファイルを開く] コマンドを使用したファイルの表示](../extensibility/internals/displaying-files-by-using-the-open-file-command.md)」を参照してください。 プロジェクト固有のエディターを使用して `OpenItem` ファイルを開くためのメソッドを実装するには、次のガイドラインに従います。  
  
### <a name="to-implement-the-openitem-method-with-a-project-specific-editor"></a>プロジェクト固有のエディターを使用して OpenItem メソッドを実装するには  
  
1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A>メソッド (RDT_EditLock) を呼び出して、ファイル (ドキュメントデータオブジェクト) が既に開いているかどうかを確認します。  
  
    > [!NOTE]
    > ドキュメントデータとドキュメントビューオブジェクトの詳細については、「 [カスタムエディターのドキュメントデータとドキュメントビュー](../extensibility/document-data-and-document-view-in-custom-editors.md)」を参照してください。  
  
2. ファイルが既に開いている場合は、メソッドを呼び出し、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> パラメーターに IDO_ActivateIfOpen の値を指定して、ファイルを resurface し `grfIDO` ます。  
  
     ファイルが開いていて、ドキュメントが呼び出し元のプロジェクト以外のプロジェクトによって所有されている場合は、開いているエディターが別のプロジェクトのものであることを示す警告がユーザーに表示されます。 次に、ファイルウィンドウが表示されます。  
  
3. テキストバッファー (ドキュメントデータオブジェクト) が既に開いていて、別のビューをアタッチする場合は、そのビューをフックする必要があります。 プロジェクトからビュー (ドキュメントビューオブジェクト) をインスタンス化するには、次の方法をお勧めします。  
  
    1. サービスでを呼び出して `QueryService` <xref:Microsoft.VisualStudio.Shell.Interop.SLocalRegistry> 、インターフェイスへのポインターを取得 <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2> します。  
  
    2. <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A>ドキュメントビュークラスのインスタンスを作成するには、メソッドを呼び出します。  
  
4. <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A>ドキュメントビューオブジェクトを指定して、メソッドを呼び出します。  
  
     このメソッドは、ドキュメントウィンドウ内のドキュメントビューオブジェクトをサイトにします。  
  
5. メソッドまたはメソッドへの適切な呼び出しを実行し <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.InitNew%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.Load%2A> ます。  
  
     この時点で、ビューは完全に初期化され、開く準備ができています。  
  
6. ビューを <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> 表示して開くには、メソッドを呼び出します。  
  
## <a name="see-also"></a>参照  
 [プロジェクト項目を開いて保存する](../extensibility/internals/opening-and-saving-project-items.md)   
 [方法: 標準エディターを開く](../extensibility/how-to-open-standard-editors.md)   
 [方法: 開いているドキュメントのエディターを開く](../extensibility/how-to-open-editors-for-open-documents.md)
