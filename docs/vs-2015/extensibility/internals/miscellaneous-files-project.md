---
title: その他のファイルプロジェクト |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- files, adding existing files to solutions
- Miscellaneous Files project
- Solution Items folder
- files, opening with Miscellaneous Files project
ms.assetid: 93a278a8-d4f4-400b-8945-4f1b0a2b5bac
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9c128475ad9f5cb71b98325bbece4e524507a08b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68179780"
---
# <a name="miscellaneous-files-project"></a>その他のファイル プロジェクト
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ユーザーがプロジェクト項目を開くと、IDE はその他のファイルプロジェクトに、ソリューション内のプロジェクトのメンバーではないすべての項目を割り当てます。  
  
 プロジェクトは、ユーザーがプロジェクト項目を開いたときにどのエディターが使用されるかを決定するうえで重要な役割を果たします。 プロジェクトは、プロジェクト固有のエディターまたは標準エディターを使用して、特定のファイルを開くように設計できます。  
  
 プロジェクト固有のエディターでは、通常、ユーザーが特別な知識を持っているか、またはプロジェクトから特殊なインターフェイスを使用している必要があります。 詳細については、「 [方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)」を参照してください。  
  
 標準エディターでは、任意のプロジェクトで特定の拡張機能の任意のファイルを開くことができます。 ユーザーは、プロジェクトのために、テキストエディターなどの一部の標準エディターをカスタマイズでき [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ますが、パブリック文字は引き続き保持できます。 標準エディターは、メソッドを使用して作成され <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> ます。  
  
 ソリューション内のプロジェクトがプロジェクト項目を開くことができない場合、IDE には、任意のファイルを開く "その他のファイル" プロジェクトと呼ばれる特別なプロジェクトが用意されています。  
  
 この特別なプロジェクトでは、プロジェクトのコンテキストの外部でファイルを開くことができます。 メソッドの処理中 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenDocumentViaProject%2A> 、その他のファイルプロジェクトは常に低優先度で応答します。 そのため、その他のファイルプロジェクトは常に、ファイルを開くことができる優先度の高いプロジェクトに対して生成されます。  
  
 その他のファイルプロジェクトでは、ユーザーが [ **新しいプロジェクト** ] ダイアログボックスを使用して明示的に作成する必要はありません。 また、その他のファイルプロジェクトでは、プロジェクトメンバーの一覧は永続的には管理されません。 また、オプションの機能を使用して、各ユーザーが最近使用したファイルの一覧を記録します。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument>   
 <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>   
 [方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)   
 [方法: 標準エディターを開く](../../extensibility/how-to-open-standard-editors.md)   
 [プロジェクトおよびプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)   
 [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
