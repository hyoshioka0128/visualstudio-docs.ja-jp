---
title: VSPackage | のインストールディレクトリを選択するMicrosoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, installation directory
ms.assetid: 01fbbb5b-f747-446c-afe0-2a081626a945
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c4100c045181f32e51abcc59116a69cad6cc33b5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697246"
---
# <a name="choosing-the-installation-directory-for-a-vspackage"></a>VSPackage のインストール ディレクトリの選択
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

VSPackage とそのサポートファイルは、ユーザーのファイルシステム上にある必要があります。 場所は、VSPackage が管理されているかどうか、サイドバイサイドのバージョン管理スキーム、およびユーザーの選択によって異なります。  
  
## <a name="unmanaged-vspackages"></a>アンマネージド Vspackage  
 アンマネージ VSPackage は、任意の場所にインストールできる COM サーバーです。 その登録情報は、その場所を正確に反映している必要があります。 インストーラーのユーザーインターフェイス (UI) は、ProgramFilesFolder Windows インストーラープロパティのサブディレクトリとして既定の場所を提供する必要があります。 次に例を示します。  
  
 ProgramFilesFolderMyCompany\MyVSPackageProduct\V1.0\  
  
 ユーザーは、小さいブートパーティションを保持し、別のボリュームにアプリケーションやツールをインストールすることを希望するユーザーに対応するために、既定のディレクトリを変更できるようにする必要があります。  
  
 サイドバイサイドスキームでバージョン管理された VSPackage が使用されている場合は、サブディレクトリを使用して異なるバージョンを格納できます。 次に例を示します。  
  
 ProgramFilesFolderMyCompany\MyVSPackageProduct\V1.0\2002\  
  
 ProgramFilesFolderMyCompany\MyVSPackageProduct\V1.0\2003\  
  
 ProgramFilesFolderMyCompany\MyVSPackageProduct\V1.0\2005\  
  
## <a name="managed-vspackages"></a>マネージド VSPackage  
 マネージ Vspackage は、任意の場所にインストールすることもできます。 ただし、アセンブリの読み込み時間を短縮するには、グローバルアセンブリキャッシュ (GAC) にインストールすることを常に考慮する必要があります。 マネージ Vspackage は常に厳密な名前を持つアセンブリなので、GAC にインストールすると、厳密な名前の署名の検証はインストール時にのみ行われることになります。 ファイルシステム内の他の場所にインストールされている厳密な名前付きのアセンブリは、読み込まれるたびに署名を検証する必要があります。 マネージ Vspackage を GAC にインストールする場合は、regpkg ツールの **/assembly** スイッチを使用して、アセンブリの厳密な名前を指すレジストリエントリを書き込みます。  
  
 Managed Vspackage を GAC 以外の場所にインストールする場合は、「管理されていない Vspackage に対するディレクトリ階層の選択」に記載されている前述のアドバイスに従ってください。 Regpkg ツールの **/codebase** スイッチを使用して、VSPackage アセンブリのパスを指すレジストリエントリを書き込みます。  
  
 詳細については、「 [vspackage の登録と登録解除](../../extensibility/registering-and-unregistering-vspackages.md)」を参照してください。  
  
## <a name="satellite-dlls"></a>サテライト DLL  
 慣例により、特定のロケールのリソースを含む VSPackage サテライト Dll は、VSPackage ディレクトリのサブディレクトリにあります。 サブディレクトリはロケール ID (LCID) 値に対応します。  
  
 [Vspackage を管理](../../extensibility/managing-vspackages.md) することは、レジストリエントリが [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSPACKAGE のサテライト DLL を実際に検索する場所を制御することを示します。 ただし、では、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] LCID 値がという名前のサブディレクトリに、次の順序でサテライト DLL の読み込みが試行されます。  
  
1. 既定の LCID (たとえば、英語の場合は \ 1033)  
  
2. 既定のサブ言語を持つ既定の LCID。  
  
3. システムの既定の LCID。  
  
4. 既定のサブ言語を持つシステムの既定の LCID。  
  
5. 米国英語 (. \ 1033 または .\0x409)。  
  
   VSPackage DLL にリソースと SatelliteDll\DllName レジストリエントリが含まれている場合、はこれらの DLL を [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 上記の順序で読み込もうとします。  
  
## <a name="see-also"></a>参照  
 [共有バージョンとバージョン付き Vspackage の選択](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)   
 [Vspackage の管理](../../extensibility/managing-vspackages.md)   
 [マネージドパッケージの登録](https://msdn.microsoft.com/f69e0ea3-6a92-4639-8ca9-4c9c210e58a1)
