---
title: '方法: ソース管理プラグインの互換性に関する警告をオフにする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, turning off compatibility warnings
- compatibility warnings, turning off
ms.assetid: ba318e12-921b-4b7a-a8c2-12c712be1dbf
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a4397b2710a7de4addd97bfcbdb4f8e80e2b9c70
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204050"
---
# <a name="how-to-turn-off-compatibility-warnings-for-source-control-plug-ins"></a>方法: ソース管理プラグインの互換性に関する警告をオフにする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

でソース管理を採用している場合、ユーザーにはいくつかの互換性の警告が表示されることがあり [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。 表示される警告は、ソース管理プラグインの機能によって異なります。詳細については、こちらを参照してください。  
  
### <a name="to-disable-the-warning-to-ensure-optimal-source-control-integration-with-visual-studio"></a>"Visual Studio との最適なソース管理の統合を保証するには..." という警告を無効にするには  
  
- 次のレジストリエントリを設定します (必要に応じて値を追加します)。  
  
     HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\8.0\SourceControl\DontDisplayCheckDotNETCompatible = dword: 00000001  
  
     この警告は、すべての非プラグインに対して表示され [!INCLUDE[vsvss](../includes/vsvss-md.md)] ます。  
  
### <a name="to-disable-the-warning-the-installed-source-control-provider-does-not-support-all-the-capabilities"></a>警告を無効にするには、「インストールされているソース管理プロバイダーは、すべての機能をサポートしていません...」  
  
- 次の2つのレジストリ値を設定します (必要に応じて値を追加します)。  
  
     HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\8.0\SourceControl\WarnedOldMSSCCIProvider = dword: 00000000  
  
     HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\8.0\SourceControl\UseOldSCC = dword: 00000001  
  
     この警告は、ソース管理プラグインが複数のプロジェクトの再入を明示的にサポートしていない場合 (つまり、一度に1つのファイルとプロジェクトだけをチェックインできる場合) に表示されます。  
  
     再入 (機能) をサポートすることをお勧めします。そう `SCC_CAP_REENTRANT` しないと、この警告は削除されます。 ただし、このサポートが不可能な場合は、これらのレジストリエントリを設定できます。  
  
## <a name="see-also"></a>参照  
 [機能フラグ](../extensibility/capability-flags.md)
