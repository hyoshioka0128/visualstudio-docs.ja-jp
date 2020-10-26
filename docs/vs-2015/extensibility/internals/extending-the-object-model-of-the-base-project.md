---
title: 基本プロジェクト | のオブジェクトモデルの拡張Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- automation object model, extending
- project subtypes, extending automation object model
- automation object model
ms.assetid: 2f95cc53-dff6-476c-bacd-500fb0ff7725
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7723881bce81824b66a936793175077a0ec67666
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68187163"
---
# <a name="extending-the-object-model-of-the-base-project"></a>ベース プロジェクトのオブジェクト モデルの拡張
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

プロジェクトのサブタイプは、基本プロジェクトのオートメーションオブジェクトモデルを次の場所で拡張することができます。  
  
- プロジェクトの Extender (" \<ProjectSubtypeName> ") –プロジェクトのサブタイプが、からのカスタムメソッドを持つオブジェクトを提供できるようにします <xref:EnvDTE.Project> 。 プロジェクトのサブタイプは、オートメーションエクステンダーを使用してオブジェクトを公開でき `Project` ます。 <xref:EnvDTE80.IInternalExtenderProvider>メインプロジェクトのサブタイプアグリゲーターに実装されたインターフェイスは、からのオブジェクト `VSHPROPID_ExtObjectCATID` <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2> (VSITEMID_ROOT の値に対応する) を提供する必要があり `itemid` `VSITEMID` ます。  
  
- ProjectItem (" \<ProjectSubtypeName> ") –プロジェクトのサブタイプが、プロジェクト内の特定のオブジェクトからのカスタムメソッドを持つオブジェクトを提供できるようにします <xref:EnvDTE.ProjectItem> 。 プロジェクトのサブタイプは、オートメーションエクステンダーを使用してこのオブジェクトを公開できます。 <xref:EnvDTE80.IInternalExtenderProvider>メインプロジェクトのサブタイプアグリゲーターに実装されているインターフェイスは、の `VSHPROPID_ExtObjectCATID` オブジェクト <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> (必要な CATID に対応する) を提供する必要があり `VSITEMID` ます。  
  
- プロジェクト. プロパティ–このコレクションは、オブジェクトの構成に依存しないプロパティを公開します。 `Project` プロジェクトのプロパティの詳細については、「」を参照してください <xref:EnvDTE.Project.Properties%2A> 。 プロジェクトのサブタイプは、オートメーションエクステンダーを使用して、そのプロパティをこのコレクションに追加できます。 <xref:EnvDTE80.IInternalExtenderProvider>メインプロジェクトのサブタイプアグリゲーターに実装されているインターフェイスは、 `VSHPROPID_BrowseObjectCATID` VSHPROPID2 から (VSITEMID_ROOT の値に対応する) CATID のオブジェクトを提供する必要があり `itemid` <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> ます。  
  
- [構成]: このコレクションは、特定の構成 (デバッグなど) のプロジェクトの構成依存プロパティを公開します。 詳細については、「<xref:EnvDTE.Configuration>」を参照してください。 プロジェクトのサブタイプは、オートメーションエクステンダーを使用して、そのプロパティをこのコレクションに追加できます。 <xref:EnvDTE80.IInternalExtenderProvider>メインプロジェクトのサブタイプアグリゲーターに実装されたインターフェイスは、CATID `VSHPROPID_CfgBrowseObjectCATID` (の値に対応する) のオブジェクトを提供し `itemid` <xref:Microsoft.VisualStudio.VSConstants.VSITEMID> ます。 インターフェイスは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject> 1 つの構成参照オブジェクトを別の構成と区別するために使用されます。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>
