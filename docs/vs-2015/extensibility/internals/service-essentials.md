---
title: サービスの要点 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- services, essentials
ms.assetid: fbe84ad9-efe1-48b1-aba3-b50b90424d47
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 407dda2f203b7be20b19c0e296caa9ce1c95b32c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65696081"
---
# <a name="service-essentials"></a>サービスの基本情報
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

サービスは、2つの Vspackage 間のコントラクトです。 VSPackage は、別の VSPackage が使用するインターフェイスの特定のセットを提供します。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] は、他の Vspackage にサービスを提供する Vspackage のコレクションです。  
  
 たとえば、SVsActivityLog サービスを使用して IVsActivityLog インターフェイスを取得することができます。このインターフェイスを使用して、アクティビティログに書き込むことができます。 詳細については、「 [方法: アクティビティログを使用する](../../extensibility/how-to-use-the-activity-log.md)」を参照してください。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] には、登録されていない組み込みのサービスも用意されています。 Vspackage は、サービスのオーバーライドを提供することによって、組み込みサービスやその他のサービスを置き換えることができます。 サービスに対して許可されるサービスオーバーライドは1つだけです。  
  
 サービスには探索できません。 そのため、使用するサービスのサービス識別子 (SID) を把握しておく必要があります。また、どのインターフェイスが提供するかを把握しておく必要があります。 この情報は、本サービスのリファレンスドキュメントに記載されています。  
  
- サービスを提供する Vspackage は、サービスプロバイダーと呼ばれます。  
  
- 他の Vspackage に提供されるサービスは、グローバルサービスと呼ばれます。  
  
- それらを実装する VSPackage、または作成した任意のオブジェクトにのみ使用できるサービスは、ローカルサービスと呼ばれます。  
  
- 他のパッケージによって提供される組み込みのサービスやサービスを置き換えるサービスは、サービスの上書きと呼ばれます。  
  
- サービス、またはサービスの上書きは、要求時に読み込まれます。つまり、サービスプロバイダーは、提供されたサービスが別の VSPackage によって要求されたときに読み込まれます。  
  
- オンデマンド読み込みをサポートするために、サービスプロバイダーはそのグローバルサービスをに登録 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] します。 詳細については、「 [サービスの登録](../../misc/registering-services.md)」を参照してください。  
  
- サービスを取得した後、必要なインターフェイスを取得するには、 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) (アンマネージコード) またはキャスト (マネージコード) を使用します。次に例を示します。  
  
    ```vb  
    TryCast(GetService(GetType(SVsActivityLog)), IVsActivityLog)  
    ```  
  
    ```csharp  
    GetService(typeof(SVsActivityLog)) as IVsActivityLog;  
  
    ```  
  
- マネージコードは、その型によってサービスを参照します。一方、アンマネージコードは GUID によってサービスを参照します。  
  
- で [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSPackage が読み込まれると、サービスプロバイダーが VSPackage に渡され、グローバルサービスにアクセスできるようになります。 これは、VSPackage の "サイト設定" と呼ばれます。  
  
- Vspackage は、作成するオブジェクトのサービスプロバイダーにすることができます。 たとえば、フォームは、カラーサービスの要求をそのフレームに送信する場合があります。これにより、要求がに渡される可能性があり [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
- 深い入れ子になっている、またはまったく配置されていないマネージオブジェクトは、 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> グローバルサービスに直接アクセスするためにを呼び出すことができます。 詳細については、「 [方法: GetGlobalService を使用する](../../misc/how-to-use-getglobalservice.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [利用可能なサービスの一覧](../../extensibility/internals/list-of-available-services.md)   
 [サービスの使用と提供](../../extensibility/using-and-providing-services.md)   
 [キャストと型変換](https://msdn.microsoft.com/library/568df58a-d292-4b55-93ba-601578722878)   
 [キャスト](https://msdn.microsoft.com/library/3dbeb06e-2f4b-4693-832d-624bc8ec95de)
