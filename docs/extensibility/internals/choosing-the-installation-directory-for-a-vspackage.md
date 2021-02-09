---
title: VSPackage | のインストールディレクトリを選択するMicrosoft Docs
description: VSPackage とそのサポートファイルのインストールディレクトリを、管理されているかどうかなどの要因を使用して選択する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, installation directory
ms.assetid: 01fbbb5b-f747-446c-afe0-2a081626a945
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ea697e6e445eeae117bb6bf1d1603220ec0c0675
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99874075"
---
# <a name="choose-the-installation-directory-for-a-vspackage"></a>VSPackage のインストールディレクトリを選択してください
VSPackage とそのサポートファイルは、ユーザーのファイルシステム上にある必要があります。 場所は、VSPackage が管理されているかどうか、サイドバイサイドのバージョン管理スキーム、およびユーザーの選択によって異なります。

## <a name="unmanaged-vspackages"></a>アンマネージド Vspackage
 アンマネージ VSPackage は、任意の場所にインストールできる COM サーバーです。 その登録情報は、その場所を正確に反映している必要があります。 インストーラーのユーザーインターフェイス (UI) は、Windows インストーラープロパティ値のサブディレクトリとして既定の場所を提供する必要があり `ProgramFilesFolder` ます。 次に例を示します。

*&lt;Programfilesfolder &gt; \\ &lt; &gt; \\ &lt; MyVSPackageProduct &gt;\\*

 ユーザーは、小さいブートパーティションを保持し、別のボリュームにアプリケーションやツールをインストールすることを希望するユーザーに対応するために、既定のディレクトリを変更できるようにする必要があります。

 サイドバイサイドスキームでバージョン管理された VSPackage が使用されている場合は、サブディレクトリを使用して異なるバージョンを格納できます。 次に例を示します。

 *&lt;Programfilesfolder &gt; \\ &lt; &gt; \\ &lt; MyVSPackageProduct v1.0 &gt; \\ \\ 2002\\*

 *&lt;Programfilesfolder &gt; \\ &lt; &gt; \\ &lt; MyVSPackageProduct v1.0 &gt; \\ \\ 2003\\*

 *&lt;Programfilesfolder &gt; \\ &lt; &gt; \\ &lt; MyVSPackageProduct v1.0 &gt; \\ \\ 2005\\*

## <a name="managed-vspackages"></a>マネージド VSPackage
 マネージ Vspackage は、任意の場所にインストールすることもできます。 ただし、アセンブリの読み込み時間を短縮するには、グローバルアセンブリキャッシュ (GAC) にインストールすることを常に考慮する必要があります。 マネージ Vspackage は常に厳密な名前を持つアセンブリなので、GAC にインストールすると、厳密な名前の署名の検証はインストール時にのみ行われることになります。 ファイルシステム内の他の場所にインストールされている厳密な名前付きのアセンブリは、読み込まれるたびに署名を検証する必要があります。 マネージ Vspackage を GAC にインストールする場合は、regpkg ツールの **/assembly** スイッチを使用して、アセンブリの厳密な名前を指すレジストリエントリを書き込みます。

 Managed Vspackage を GAC 以外の場所にインストールする場合は、「管理されていない Vspackage に対するディレクトリ階層の選択」に記載されている前述のアドバイスに従ってください。 Regpkg ツールの **/codebase** スイッチを使用して、VSPackage アセンブリのパスを指すレジストリエントリを書き込みます。

 詳細については、「 [Register And Register vspackage](../../extensibility/registering-and-unregistering-vspackages.md)」を参照してください。

## <a name="satellite-dlls"></a>サテライト DLL
 慣例により、特定のロケールのリソースを含む VSPackage サテライト Dll は、 *VSPackage* ディレクトリのサブディレクトリに配置されます。 サブディレクトリはロケール ID (LCID) 値に対応します。

 [Manage vspackage](../../extensibility/managing-vspackages.md)記事は、レジストリエントリが [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPACKAGE のサテライト DLL を実際に検索する場所を制御することを示します。 ただし、では、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] LCID 値がという名前のサブディレクトリに、次の順序でサテライト DLL の読み込みが試行されます。

1. 既定の LCID (たとえば、英語の場合は *\ 1033* )

2. 既定のサブ言語を持つ既定の LCID。

3. システムの既定の LCID。

4. 既定のサブ言語を持つシステムの既定の LCID。

5. 米国英語 (*. \ 1033* または *.\0x409*)。

VSPackage DLL にリソースと **SatelliteDll\DllName** レジストリエントリが含まれている場合、はこれらの DLL を [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 上記の順序で読み込もうとします。

## <a name="see-also"></a>関連項目
- [共有バージョンとバージョン付き Vspackage を選択する](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)
- [VSPackage を管理する](../../extensibility/managing-vspackages.md)
- [パッケージ登録の管理](/previous-versions/bb166783(v=vs.100))