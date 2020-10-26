---
title: レジストリ内のツールウィンドウ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- tool windows, registering
ms.assetid: c4bb8add-7148-49e4-a377-01d059fd5524
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8cedb95ccd98c3d5bd5e05086cfd1b53b0f97cd9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68186381"
---
# <a name="tool-windows-in-the-registry"></a>レジストリのツール ウィンドウ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ツールウィンドウを提供する Vspackage は、ツール [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ウィンドウプロバイダーとしてに登録する必要があります。 Visual Studio パッケージテンプレートを使用して作成されたツールウィンドウは、既定でこれを実行します。 ツールウィンドウプロバイダーには、表示属性を指定するシステムレジストリキーがあります。これには、既定のツールウィンドウのサイズと場所、ツールウィンドウペインとして機能するウィンドウの GUID、ドッキングスタイルなどが含まれます。  
  
 開発中、マネージツールウィンドウプロバイダーは、ソースコードに属性を追加し、結果のアセンブリで RegPkg.exe ユーティリティを実行することで、ツールウィンドウを登録します。 詳細については、「 [ツールウィンドウの登録](../extensibility/registering-a-tool-window.md)」を参照してください。  
  
## <a name="registering-unmanaged-tool-window-providers"></a>アンマネージツールウィンドウプロバイダーを登録しています  
 アンマネージツールウィンドウプロバイダーは、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] システムレジストリの ToolWindows セクションのに登録する必要があります。 次の .reg ファイルフラグメントは、動的ツールウィンドウがどのように登録されるかを示しています。  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\<version number>\ToolWindows\{f0e1e9a1-9860-484d-ad5d-367d79aabf55}]  
@="{01069cdd-95ce-4620-ac21-ddff6c57f012}"  
"Name"="Microsoft.Samples.VisualStudio.IDE.ToolWindow.DynamicWindowPane"  
"Float"="250, 250, 410, 430"  
"DontForceCreate"=dword:00000001  
  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\ToolWindows\{f0e1e9a1-9860-484d-ad5d-367d79aabf55}\Visibility]  
"{f1536ef8-92ec-443c-9ed7-fdadf150da82}"=dword:00000000  
```  
  
 上記の例の最初のキーでは、バージョン番号はのバージョン ( [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 7.1 や8.0 など)、サブキー {f0e1e9a1-9860-484d-ad5d-367d79aabf55} はツールウィンドウペインの guid (DynamicWindowPane)、既定値 {01069cdd-4620 95ce-ac21-ddff6c57f012} は、ツールウィンドウを提供している VSPackage の guid です。 Float サブキーと DontForceCreate サブキーの詳細については、「 [ツールウィンドウの表示構成](../extensibility/tool-window-display-configuration.md)」を参照してください。  
  
 2番目の省略可能なキー ToolWindows\Visibility は、ツールウィンドウを表示する必要があるコマンドの Guid を指定します。 この場合、コマンドは指定されていません。 詳細については、「 [ツールウィンドウの表示構成](../extensibility/tool-window-display-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [VSPackage の基本事項](../misc/vspackage-essentials.md)
