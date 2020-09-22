---
title: '方法: サービスを登録する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- services, registering
ms.assetid: d086be78-ec3c-43cc-b799-5180a71e19f1
caps.latest.revision: 16
manager: jillfra
ms.openlocfilehash: f41578f2522487f746a469933a2269a621390f3c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841436"
---
# <a name="how-to-register-a-service"></a>方法: サービスを登録する
Managed Package Framework (MPF) は、管理するサービスの登録を制御する属性を提供します。 RegPkg ユーティリティでは、これらの属性を使用して、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]にサービスを登録します。  
  
## <a name="example"></a>例  
 次のコードは、 [Vssdk サンプル](../misc/vssdk-samples.md)からのものです。  
  
 [!code-csharp[VSSDKRegisterService#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkregisterservice/cs/vssdkregisterservicepackage.cs#1)]
 [!code-vb[VSSDKRegisterService#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkregisterservice/vb/vssdkregisterservicepackage.vb#1)]  
  
 <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> によって、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] に SMyGlobalService サービスが登録されます。 およびの詳細について <xref:Microsoft.VisualStudio.Shell.DefaultRegistryRootAttribute> <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> は、「 [vspackage の登録と登録解除](../extensibility/registering-and-unregistering-vspackages.md)」を参照してください。  
  
 名前が同じ別のサービスを置き換えるサービスを登録するには、<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> ではなく <xref:Microsoft.VisualStudio.Shell.ProvideServiceOverrideAttribute> を使用します。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 サービス クライアントを変更せずに、サービス プロバイダーの再コンパイルを容易にできるようにするか、またはその逆を実行するには、別のアセンブリ モジュールでサービスとそのインターフェイスを定義することができます。 次のコードは Reference.Services (C#) サンプルの IMyGlobalService.cs ファイルのものです。  
  
 [!code-csharp[VSSDKRegisterService#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkregisterservice/cs/vssdkregisterservicepackage.cs#2)]
 [!code-vb[VSSDKRegisterService#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkregisterservice/vb/vssdkregisterservicepackage.vb#2)]  
  
 アンマネージ コードからインターフェイスを取得するには、<xref:System.Runtime.InteropServices.ComVisibleAttribute> が必要です。  
  
> [!NOTE]
> サービスとインターフェイスの両方に同じ型または GUID を使用できますが、サービスが異なるインターフェイスを公開できるようにするために、2 つを分離することをお勧めします。  
  
## <a name="see-also"></a>参照  
 [Vspackage を登録しています](../extensibility/internals/registering-vspackages.md)   
 [サービスの基本情報](../extensibility/internals/service-essentials.md)