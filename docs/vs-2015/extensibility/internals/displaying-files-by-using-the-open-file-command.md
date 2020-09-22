---
title: '[ファイルを開く] コマンドを使用してファイルを表示する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project types, supporting Open File command
- Open File command
- persistence, supporting Open File command
ms.assetid: 4fff0576-b2f3-4f17-9769-930f926f273c
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: dd0018df4efb023357e10ab8050f6cf5e9eba1fb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842156"
---
# <a name="displaying-files-by-using-the-open-file-command"></a>ファイルを開くコマンドを使用したファイルの表示
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

次の手順では、IDE で [ **ファイルを開く** ] コマンドを処理する方法について説明します。これは、の [ **ファイル** ] メニューで使用でき [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 この手順では、このコマンドからの呼び出しにプロジェクトが応答する方法についても説明します。  
  
 ユーザーが **[ファイル] メニューの**[**ファイルを開く**] コマンドをクリックし、[ファイルを**開く**] ダイアログボックスでファイルを選択すると、次のプロセスが実行されます。  
  
1. IDE では、実行中のドキュメントテーブルを使用して、ファイルが既にプロジェクトで開かれているかどうかを判断します。  
  
    - ファイルが開いている場合は、IDE によってウィンドウが resurfaces されます。  
  
    - ファイルが開いていない場合、IDE は <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> を呼び出して各プロジェクトに対してクエリを実行し、ファイルを開くことができるプロジェクトを判別します。  
  
        > [!NOTE]
        > のプロジェクト実装で <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> 、プロジェクトがファイルを開くレベルを示す優先度値を指定します。 優先順位値は、列挙体で指定され <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> ます。  
  
2. 各プロジェクトは、ファイルを開くためにプロジェクトに必要な重要度を示す優先度レベルで応答します。  
  
3. IDE では、次の基準を使用して、ファイルを開くプロジェクトを決定します。  
  
    - 最高の優先度 (DP_Intrinsic) で応答するプロジェクトは、ファイルを開きます。 複数のプロジェクトがこの優先順位で応答する場合は、最初に応答するプロジェクトがファイルを開きます。  
  
    - 最も優先度の高い (DP_Intrinsic) プロジェクトが応答しなくても、すべてのプロジェクトが同じで優先度の低い優先順位で応答する場合、アクティブなプロジェクトはファイルを開きます。 アクティブなプロジェクトがない場合は、最初に応答するプロジェクトがファイルを開きます。  
  
    - ファイルの所有権を要求しているプロジェクトがない場合 (DP_Unsupported)、[その他のファイル] プロジェクトによってファイルが開きます。  
  
         その他のファイルプロジェクトのインスタンスが作成された場合、プロジェクトは常に DP_CanAddAsExternal 値を使用して応答します。 この値は、プロジェクトがファイルを開くことができることを示します。 このプロジェクトは、他のプロジェクトに含まれていない開いているファイルを格納するために使用されます。 このプロジェクト内の項目の一覧は保存されません。このプロジェクトは、ファイルを開くために使用された場合にのみ **ソリューションエクスプローラー** に表示されます。  
  
         その他のファイルプロジェクトでファイルを開くことができないことが示されていない場合は、プロジェクトのインスタンスが作成されていません。 この場合、IDE はその他のファイルプロジェクトのインスタンスを作成し、ファイルを開くようにプロジェクトに指示します。  
  
4. IDE によってファイルを開くプロジェクトが決定されるとすぐに、その <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> プロジェクトでメソッドが呼び出されます。  
  
5. プロジェクトには、プロジェクト固有のエディターまたは標準エディターを使用してファイルを開くオプションがあります。 詳細については、「 [方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md) 」および「 [方法: 標準エディターを開く](../../extensibility/how-to-open-standard-editors.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Open With コマンドを使用したファイルの表示](../../extensibility/internals/displaying-files-by-using-the-open-with-command.md)   
 [プロジェクト項目を開いて保存する](../../extensibility/internals/opening-and-saving-project-items.md)   
 [方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)   
 [方法: 標準のエディターを開く](../../extensibility/how-to-open-standard-editors.md)
