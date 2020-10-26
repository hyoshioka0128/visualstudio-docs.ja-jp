---
title: プロジェクトシステムへの Web サービスの追加 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- project systems, adding Web services
- Web services, adding to VSPackage project systems
ms.assetid: 8efa078b-68b2-45a2-9be2-44f807bc0d7f
caps.latest.revision: 8
manager: jillfra
ms.openlocfilehash: f5b192be8e5f68ad9314fe08fff963c032013cb0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "63002658"
---
# <a name="adding-web-services-to-project-systems"></a>プロジェクト システムへの Web サービスの追加
XML Web サービスは、一般に、SOAP (Simple Object Access Protocol) プロトコルを使用してプログラム情報をプロジェクトシステムに返す、URL でアドレス指定可能なリソースです。 インターフェイスを使用して、Web サービスを VSPackage プロジェクトシステムに統合でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddProjectItemDlg2> ます。  
  
### <a name="to-add-a-web-service-to-your-project-system"></a>プロジェクトシステムに Web サービスを追加するには  
  
1. `QueryService`サービスを <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddProjectItemDlg2> 使用してインターフェイスを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.SVsAddWebReferenceDlg> ます。  
  
2. <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg2.AddWebReferenceDlg%2A> メソッドを呼び出します。 `pDiscoverySession`パラメーターをとして渡すと `NULL` 、検出セッションが作成され、そのセッションがキャッシュされて、インターフェイスでの後続の使用に使用できるようになり <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg2> ます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg2.AddWebReferenceDlg%2A> メソッドは、へのポインターを返し <xref:Microsoft.VisualStudio.Shell.Interop.IDiscoveryResult2> ます。  
  
3. <xref:Microsoft.VisualStudio.Shell.Interop.IDiscoveryResult.AddWebReference%2A> メソッドを呼び出します。 Web サービス参照フォルダーのオートメーションオブジェクトをパラメーターとして渡し `pUnkWebReferenceFolder` ます。 その後、Visual Studio 環境によって、Web サービスが既に存在するかどうかが確認されます。 Web サービスが存在しない場合は、環境によって Web サービスがダウンロードされ、フォルダーおよび追加ファイル (.wsdl ファイルなど) にフォルダーの子ノードに追加されます。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg2>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IDiscoveryResult>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IDiscoverySession>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDiscoveryService>