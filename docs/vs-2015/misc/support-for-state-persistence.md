---
title: 状態の永続化のサポート |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- state persistence, managed package framework support
- managed package framework, state persistence support
- state, persistence
ms.assetid: d25866f2-8d1f-477f-8aa5-3af3fbbf6e97
caps.latest.revision: 15
manager: jillfra
ms.openlocfilehash: 6dc542d2e410b79a21e436a1881c06bd3cc4eef8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62434320"
---
# <a name="support-for-state-persistence"></a>状態の永続性のサポート
[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 共通オブジェクトの状態を維持できます。 たとえば、ソリューションとプロジェクトのプロパティは、ソリューションファイルとプロジェクトファイルに保存され、復元されます。 ユーザー設定をエクスポートしたり、設定ファイルからインポートしたりできます。  
  
 Vspackage は、通常、システムレジストリ、または現在のユーザーまたはコンピューターの application data フォルダーにあるローカルストレージに依存しています。 通常、整数や文字列など、ストレージ用に少量の領域を必要とする値は、システムレジストリに格納されます。 ビットマップなど、ストレージに多くの領域を必要とする値は、ファイルに保存されます。 ファイルのパスは、システムレジストリに保存することができます。 永続化メカニズムには、ローカルストレージにアクセスするためのアクセス許可が必要です。  
  
## <a name="support-for-locating-local-storage"></a>ローカルストレージの検索のサポート  
 クラスは、 <xref:Microsoft.VisualStudio.Shell.Package> 現在のユーザーまたはコンピューターのシステムレジストリまたはアプリケーションデータフォルダー内の状態情報を検索するためのサポートを提供します。  
  
 <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>  
 ローカルコンピューターのレジストリルートのパスを返します。たとえば [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 、HKEY_LOCAL_MACHINE \software\microsoft\visualstudio\8.0exp. のようになります。  
  
 ローカルレジストリルートは、サービスから取得され <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell> ます。 使用できない場合は、VSPackage の属性から取得され <xref:Microsoft.VisualStudio.Shell.DefaultRegistryRootAttribute> ます。  
  
 <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A>  
 現在のユーザーの (コンピューターごとの) レジストリルートのパスを返します ( [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 例 HKEY_CURRENT_USER \software\microsoft\visualstudio\8.0exp.)。  
  
 ローカルレジストリルートは、サービスから取得され <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell> ます。 使用できない場合は、VSPackage の DefaultLocalRegistryRoot 属性から取得されます。  
  
 <xref:Microsoft.VisualStudio.Shell.Package.UserDataPath%2A>  
 現在のローミングユーザーのデータの共通リポジトリとして機能するディレクトリのパスを返します。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] たとえば、c:\documents and、 \\ *accountname*\Application Data\Microsoft\VisualStudio\8.0Exp. のように設定します。  
  
 <xref:Microsoft.VisualStudio.Shell.Package.UserLocalDataPath%2A>  
 現在の非ローミングユーザーのデータの共通リポジトリとして機能するディレクトリのパスを返します。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] たとえば、c:\documents and と Settings を \\ *accountname*\Local Settings\Application Data\Microsoft\VisualStudio\8.0Exp. として指定します。  
  
## <a name="see-also"></a>参照  
 [Visual Studio の状態](../misc/vspackage-state.md)