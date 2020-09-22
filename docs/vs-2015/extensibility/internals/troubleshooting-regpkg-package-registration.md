---
title: RegPkg パッケージ登録のトラブルシューティング |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: troubleshooting
helpviewer_keywords:
- RegPkg
ms.assetid: f33f822f-697a-4bad-9c10-554b4c8f6246
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 241975e475252a18d5e5a91c6e8c4fb40c067a95
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841812"
---
# <a name="troubleshooting-regpkg-package-registration"></a>RegPkg パッケージ登録のトラブルシューティング
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!NOTE]
> Visual Studio でパッケージを登録するには、pkgdef ファイルを使用することをお勧めします。 これにより、システムレジストリにアクセスしなくても拡張機能を展開できます。 Pkgdef ファイルは、 [Createpkgdef ユーティリティ](../../extensibility/internals/createpkgdef-utility.md)を使用して作成されます。  
  
 で RegPkg を使用してパッケージを登録するには [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 、パッケージに適したバージョンの RegPkg を使用する必要があります。  
  
## <a name="regpkg-versions-related-to-package-versions"></a>パッケージのバージョンに関連する RegPkg のバージョン  
 RegPkg には2つのバージョンがあります。 には1つのバージョンが含まれてい [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 このバージョンを使用して、次のいずれかのアセンブリを使用して作成されたパッケージを登録します。  
  
1. Microsoft.VisualStudioShell.9.0.dll  
  
2. Microsoft.VisualStudioShell.10.0.dll  
  
3. Microsoft.VisualStudioShell.11.0.dll  
  
   以前の Microsoft.VisualStudio.Shell.dll アセンブリを使用してビルドされたパッケージを登録することはできません。  
  
   以前のバージョンの RegPkg では、Microsoft.VisualStudio.Shell.dll アセンブリを使用してビルドされたパッケージを登録できます。 ただし、新しいバージョンのアセンブリを使用してビルドされたパッケージを登録することはできません。  
  
## <a name="see-also"></a>参照  
 [製品のリリース](../../misc/releasing-a-visual-studio-integration-product.md)
