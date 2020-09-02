---
title: '方法: GetGlobalService を使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- services, GetGlobalService
ms.assetid: 4cdf5ab5-9f09-4caf-9011-2dcb2c62f1b7
caps.latest.revision: 14
manager: jillfra
ms.openlocfilehash: 1c1fb48e4bb354ef403b39b0f1320ead92f43967
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62948183"
---
# <a name="how-to-use-getglobalservice"></a>方法: GetGlobalService を使用する
場合によっては、配置されていないツールウィンドウまたはコントロールコンテナーからサービスを取得する必要があります。そうしないと、必要なサービスがわからないサービスプロバイダーが配置されていることがあります。 たとえば、コントロール内からアクティビティログに書き込むことができます。 これらのシナリオとその他のシナリオの詳細については、「 [方法: サービスのトラブルシューティング](../extensibility/how-to-troubleshoot-services.md)」を参照してください。  
  
 ほとんど [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のサービスは、静的メソッドを呼び出すことによって取得でき <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> ます。  
  
 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> は、から派生したすべての VSPackage が配置されるときに初期化される、キャッシュされたサービスプロバイダーに依存 <xref:Microsoft.VisualStudio.Shell.Package> します。 この条件が満たされていることを保証するか、null サービス用に準備する必要があります。  
  
 幸いにも、 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> ほとんどの場合、正常に動作します。  
  
- VSPackage が別の VSPackage だけを認識するサービスを提供する場合、サービスを要求する VSPackage は、サービスを提供する VSPackage が読み込まれる前に配置されます。  
  
- ツールウィンドウが VSPackage によって作成された場合、ツールウィンドウが作成される前に VSPackage が配置されます。  
  
- コントロールコンテナーが、VSPackage によって作成されたツールウィンドウによってホストされている場合、VSPackage はコントロールコンテナーが作成される前に配置されます。  
  
### <a name="to-get-a-service-from-within-a-tool-window-or-control-container"></a>ツールウィンドウまたはコントロールコンテナー内からサービスを取得するには  
  
- コンストラクター、ツールウィンドウ、またはコントロールコンテナーに次のコードを挿入します。  
  
     [!code-csharp[UseGetGlobalService#1](../snippets/csharp/VS_Snippets_VSSDK/usegetglobalservice/cs/getglobalservicepackage.cs#1)]
     [!code-vb[UseGetGlobalService#1](../snippets/visualbasic/VS_Snippets_VSSDK/usegetglobalservice/vb/getglobalservicepackage.vb#1)]  
  
     このコードは、SVsActivityLog サービスを取得し、それをインターフェイスにキャストします。これを使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> アクティビティログに書き込むことができます。 例については、「 [方法: アクティビティログを使用する](../extensibility/how-to-use-the-activity-log.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [方法: サービスのトラブルシューティング](../extensibility/how-to-troubleshoot-services.md)   
 [サービスの使用と提供](../extensibility/using-and-providing-services.md)   
 [サービスの基本情報](../extensibility/internals/service-essentials.md)