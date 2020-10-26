---
title: サービスの登録 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- services, registering
ms.assetid: c4ebac40-0374-4dda-948e-06fdda0e9c81
caps.latest.revision: 8
manager: jillfra
ms.openlocfilehash: 64f2afa6e853978e919e466f91475bed1e8d698c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62971291"
---
# <a name="registering-services"></a>サービスの登録
オンデマンド読み込みをサポートするには、サービス プロバイダーはグローバル サービスを [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]に登録する必要があります。  
  
 開発時にマネージド サービス プロバイダーはパッケージのソース コードに属性を追加し、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE でパッケージを構築して、サービスとサービスのオーバーライドを登録します。 これにより、生成されたアセンブリで RegPkg.exe ユーティリティが実行され、パッケージの登録と配置の準備が行われます。 詳細については、「 [方法: サービスを登録](../misc/how-to-register-a-service.md)する」を参照してください。  
  
 アンマネージ サービス プロバイダーは、提供するサービスをシステム レジストリのサービス セクションまたはサービス オーバーライド セクションで [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] に登録する必要があります。 次の .reg ファイル フラグメントは、SVsTextManager サービスを登録する方法を示しています。  
  
```  
[HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\<version number>\Services\{F5E7E71D-1401-11d1-883B-0000F87579D2}]  
@="{F5E7E720-1401-11d1-883B-0000F87579D2}"  
"Name"="SVsTextManager"  
```  
  
 上記の例で、バージョン番号は [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]のバージョン (7.1 や 8.0 など)、キー {F5E7E71D-1401-11d1-883B-0000F87579D2} は SVsTextManager サービスのサービス識別子 (SID)、既定値 {F5E7E720-1401-11d1-883B-0000F87579D2} はサービスを提供するテキスト マネージャー VSPackage のパッケージ GUID です。  
  
## <a name="remote-services-and-background-threads"></a>リモート サービスとバックグラウンド スレッド  
 提供するサービスは、リモートで、またはバックグラウンド スレッドに対して自動的に利用可能にはなりません。 使用できるようにするには、タイプ ライブラリを構築し、登録する必要があります。  
  
 Visual Studio ライブラリ (VSL) を使用するアンマネージ コードから、次のようにタイプ ライブラリを登録できます。  
  
```  
#define VSL_REGISTER_TYPE_LIB TRUE  
#include <VSLPackageDllEntryPoints.cpp>  
```  
  
 マネージド コードから、次のようにビルド後のステップを追加できます。  
  
```  
regasm /tlb MyAssembly.dll  
```  
  
## <a name="see-also"></a>参照  
 [サービスの使用と提供](../extensibility/using-and-providing-services.md)   
 [サービスの基本情報](../extensibility/internals/service-essentials.md)