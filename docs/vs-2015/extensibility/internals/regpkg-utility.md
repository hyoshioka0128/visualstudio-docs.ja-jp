---
title: RegPkg Utility |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- regpkg, registration utility
- registration, regpkg utility
ms.assetid: 1683ee18-59d1-4bab-a674-dd00dd960de3
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1895d3b57e5109f824728021cb1d64f0c527384b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842029"
---
# <a name="regpkg-utility"></a>RegPkg ユーティリティ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!NOTE]
> Visual Studio でパッケージを登録するには、pkgdef ファイルを使用することをお勧めします。 これにより、システムレジストリにアクセスしなくても拡張機能をデプロイできます。これは、VSIX 配置に必要です。 Pkgdef ファイルは、 [Createpkgdef ユーティリティ](../../extensibility/internals/createpkgdef-utility.md)を使用して作成されます。 Visual Studio パッケージの配置の詳細については、「 [Visual Studio 拡張機能の配布](../../extensibility/shipping-visual-studio-extensions.md)」を参照してください。  
  
 RegPkg.exe ユーティリティは、VSPackage をに登録 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] し、デプロイ用に準備します。 このユーティリティは、VSPackage の開発中にバックグラウンドで使用されます。 実験用 hive で VSPackage をビルドして実行できるように、ビルドプロセスの一部として実行されます。  
  
 RegPkg では、複数の形式でシステムレジストリスクリプトを生成できます。 これらのスクリプトは、.msi プロジェクトや Windows インストーラー XML ツールセットファイルなどの配置プロジェクトに組み込むことができます。  
  
 RegPkg.exe は通常、\VisualStudioIntegration\Tools\Bin\RegPkg.exe にあり \<*Visual Studio SDK installation path*> ます。 RegPkg は、次の構文に従います。  
  
```  
RegPkg [/root:<root>] [/regfile:<regfile>] [/rgsfile:<rgsfile> [/rgm]] [/vrgfile:<vrgfile>] [/codebase | /assembly] [/unregister] AssemblyPath  
```  
  
 /root: ルート  
 指定されたの下で登録を実行します  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ルート。  
  
 /regfile: ファイル名  
 レジストリを更新するのではなく、.reg ファイルを作成します。  /Vrgfile または/rgsfile または/wixfile. と共に使用することはできません。  
  
 /rgsfile: ファイル名  
 レジストリを更新するのではなく、.rgs ファイルを作成します。  /Vrgfile または/regfile または/wixfile. と共に使用することはできません。  
  
 /vrgfile: ファイル名  
 レジストリを更新するのではなく、vrg ファイルを作成します。  /Regfile または/rgsfile または/wixfile. と共に使用することはできません  
  
 /rgm  
 Rgs ファイルに加えて、rgm ファイルを作成します。  /Rgsfile. と組み合わせる必要があります。  
  
 /wixfile: ファイル名  
 レジストリを更新するのではなく、Windows インストーラー XML ツールセット互換ファイルを作成します。  /Regfile または/rgsfile または/vrgfileと共に使用することはできません。  
  
 /codebase  
 アセンブリではなく、コードベースで登録を強制します。  
  
 /assembly  
 コードベースではなく、アセンブリに強制的に登録します。  
  
 /unregister  
 このパッケージの登録を解除します。  使用できません  
  
 with/regfile または/vrgfile または/rgsfile または/wixfile.  
  
## <a name="see-also"></a>参照  
 [製品のリリース](../../misc/releasing-a-visual-studio-integration-product.md)   
 [RegPkg パッケージ登録のトラブルシューティング](../../extensibility/internals/troubleshooting-regpkg-package-registration.md)
