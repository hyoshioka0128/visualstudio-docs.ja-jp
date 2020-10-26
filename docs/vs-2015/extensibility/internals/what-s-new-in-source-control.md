---
title: ソース管理の新機能
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- what's new [Visual Studio SDK], source control
- source control [Visual Studio SDK], what's new
ms.assetid: bcf85418-18fb-4824-9dae-d14bf3d56a77
caps.latest.revision: 28
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 31b55c57f47f25814eff24f13bcf91408468d0f4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200950"
---
# <a name="what39s-new-in-source-control-in-visual-studio-2015"></a>Visual Studio 2015 でのソース管理の新機能&#39;

[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

で [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] は、ソース管理 VSPackage を実装することで、緊密に統合されたソース管理ソリューションを提供できます。 ここでは、ソース管理 Vspackage の機能について説明し、実装手順の概要を示します。  
  
## <a name="the-source-control-vspackage"></a>ソース管理 VSPackage  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] では、2種類のソース管理ソリューションがサポートされています。 すべてのバージョンのでは [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 、ソース管理プラグイン API ベースのプラグインを統合することもできます。 また、高度な機能を [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] 必要とするソース管理ソリューションに適した高度な統合パスを提供するソース管理の VSPackage を作成することもできます。  
  
 VSPackage は、ほぼすべての種類の機能をに追加でき [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 ソース管理 VSPackage は [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 、ユーザーに提示された UI からソース管理システムとのバックエンド通信まで、の完全なソース管理機能を提供します。  
  
 ソース管理 VSPackage を実装するには、"すべて" または "なし" の戦略が必要です。 ソース管理 VSPackage の作成者は、ソース管理インターフェイスと新しい UI 要素 (ダイアログボックス、メニュー、およびツールバー) を実装するために多くの労力を費やす必要があります。また、すべてのパッケージで正常に統合するために必要なインターフェイスについても説明し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
 次の手順では、ソース管理パッケージを実装するために必要な作業の概要を説明します。 詳細については、「 [ソース管理の作成 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)」を参照してください。  
  
1. プライベートソース管理サービスを作成する VSPackage を作成します。  
  
2. によって proffered されるソース管理関連サービス [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] (やインターフェイスなど) にインターフェイスを実装し <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider> ます。  
  
3. ソース管理 VSPackage を登録します。  
  
4. メニュー項目、ダイアログボックス、ツールバー、およびコンテキストメニューを含む、すべてのソース管理 UI を実装します。  
  
5. ソース管理に関連するすべてのイベントは、アクティブであり、VSPackage によって処理される必要がある場合に、ソース管理 VSackage に渡されます。  
  
6. ソース管理 VSPackage は、インターフェイスを実装するイベント <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3> や、(インターフェイスによって実装される) プロジェクトドキュメント (TPD) イベントを追跡し、必要なアクションを実行するなどのイベントをリッスンする必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> ます。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>   
 [概要](../../extensibility/internals/source-control-integration-overview.md)   
 [ソース管理 VSPackage の作成](../../extensibility/internals/creating-a-source-control-vspackage.md)
