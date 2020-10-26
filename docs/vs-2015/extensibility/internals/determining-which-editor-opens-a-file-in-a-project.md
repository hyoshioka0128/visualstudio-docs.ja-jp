---
title: プロジェクト内のファイルを開くエディターを決定する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], determining which editor opens a file
- projects [Visual Studio SDK], determining which editor opens file
- project types, determining which editor opens a file
- persistence, determining which editor opens a file
ms.assetid: acbcf4d8-a53a-4727-9043-696a47369479
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1c79860f770a6b04a17786cfb281fc3c0e4dffda
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196768"
---
# <a name="determining-which-editor-opens-a-file-in-a-project"></a>プロジェクトでのファイルを開くエディターの決定
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ユーザーがプロジェクト内のファイルを開くと、環境はポーリングプロセスを実行し、最終的にそのファイルの適切なエディターまたはデザイナーを開きます。 環境で採用されている最初の手順は、標準エディターとカスタムエディターの両方で同じです。 この環境では、ファイルを開くために使用するエディターをポーリングするときに、さまざまな条件を使用します。 VSPackage は、この処理中に環境を調整する必要があります。  
  
 たとえば、ユーザーが [**ファイル**] メニューから [**開く**] コマンドを選択し、 `filename` .rtf (または .rtf 拡張子を持つその他のファイル) を選択すると、環境は <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> 各プロジェクトの実装を呼び出し、最終的にはソリューション内のすべてのプロジェクトインスタンスを循環します。 プロジェクトは、優先度によってドキュメントの要求を識別するフラグのセットを返します。 最も高い優先順位を使用すると、環境は適切なメソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> ます。 ポーリングプロセスの詳細については、「 [プロジェクトおよびプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)」を参照してください。  
  
 その他のファイルプロジェクトは、他のプロジェクトによって要求されていないすべてのファイルを要求します。 これにより、標準エディターがドキュメントを開く前に、カスタムエディターでドキュメントを開くことができます。 その他のファイルプロジェクトがファイルを要求する場合、環境はメソッドを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 標準のエディターでファイルを開きます。 環境では、.rtf ファイルを処理するエディターの登録済みエディターの内部リストを確認します。 この一覧は、レジストリの次のキーにあります。  
  
 [HKEY_LOCAL_MACHINE \Software\Microsoft\VisualStudio \\ < `version`> エディター \\ {<`editor factory guid`>} \ 拡張機能]  
  
 また、この環境では、HKEY_CLASSES_ROOT/CLSID キーのクラス識別子が、サブキー DocObject を持つすべてのオブジェクトについてもチェックされます。 ファイル拡張子が見つかった場合は、Microsoft Word などのアプリケーションの埋め込みバージョンが Visual Studio に埋め込まれて作成されます。 これらのドキュメントオブジェクトは、インターフェイスを実装する複合ファイルである <xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage> か、またはオブジェクトがインターフェイスを実装する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> ます。  
  
 レジストリに .rtf ファイルのエディターファクトリがない場合は、環境が HKEY_CLASSES_ROOT .rtf キーを検索し、 \\ そこに指定されているエディターを開きます。 ファイル拡張子が HKEY_CLASSES_ROOT に見つからない場合は、Visual Studio のコアテキストエディターを使用して、ファイルがテキストファイルである場合にファイルを開きます。  
  
 ファイルがテキストファイルでない場合に発生する、コアテキストエディターが失敗した場合、環境はファイルにバイナリエディターを使用します。  
  
 環境がそのレジストリで .rtf 拡張子のエディターを見つけると、このエディターファクトリを実装する VSPackage が読み込まれます。 環境は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> 新しい VSPackage に対してメソッドを呼び出します。 VSPackage は、 `QueryService` メソッドを使用してを呼び出し `SID_SVsRegistorEditor` 、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A> 環境にエディターファクトリを登録します。  
  
 この環境では、登録されているエディターの内部リストを再確認して、.rtf ファイル用に新しく登録されたエディターファクトリを見つけます。 環境は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 作成するファイル名とビューの種類を渡して、メソッドの実装を呼び出します。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>   
 <xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>
