---
title: VSPackage のインストール ディレクトリを選択する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, installation directory
ms.assetid: 01fbbb5b-f747-446c-afe0-2a081626a945
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b8391cbdd3a857ea4ebaf3a36655520935f1a128
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709762"
---
# <a name="choose-the-installation-directory-for-a-vspackage"></a>VS パッケージのインストール ディレクトリを選択します。
VSPackage とそのサポート ファイルは、ユーザーのファイル システム上になければなりません。 場所は、VSPackage がマネージかアンマネージか、サイド バイ サイドのバージョン管理スキーム、およびユーザーの選択によって異なります。

## <a name="unmanaged-vspackages"></a>アンマネージ VS パッケージ
 アンマネージ VSPackage は、任意の場所にインストールできる COM サーバーです。 登録情報は、その場所を正確に反映する必要があります。 インストーラーのユーザー インターフェイス (UI) は、Windows インストーラーのプロパティ値`ProgramFilesFolder`のサブディレクトリとして既定の場所を提供する必要があります。 次に例を示します。

*&lt;\\&lt;&gt;マイカンパニー\\マイブス&lt;パッケージ製品 \V1.0&gt;&gt;\\*

 ユーザーは、小さなブート パーティションを保持し、別のボリュームにアプリケーションやツールをインストールすることを好むユーザーに対応するために、既定のディレクトリを変更できるようにする必要があります。

 サイド バイ サイド スキームでバージョン対応の VSPackage を使用する場合は、サブディレクトリを使用して異なるバージョンを格納できます。 次に例を示します。

 *&lt;プログラムファイルフォルダ&gt;\\&lt;マイカンパニー&gt;\\&lt;マイVSパッケージ製品&gt;\\V1.0\\2002\\*

 *&lt;\\&lt;&gt;マイカンパニー&lt;\\マイブスパッケージ製品 V1.0\\2003&gt;\\&gt;\\*

 *&lt;プログラムファイルフォルダ&gt;\\&lt;マイカンパニー&gt;\\&lt;マイVSパッケージ製品&gt;\\V1.0\\2005\\*

## <a name="managed-vspackages"></a>マネージド VSPackage
 管理 VSPackages は、任意の場所にインストールすることもできます。 ただし、アセンブリの読み込み時間を短縮するために、常にグローバル アセンブリ キャッシュ (GAC) にインストールすることを検討する必要があります。 マネージ VSPackages は常に厳密な名前を持つアセンブリであるため、GAC にアセンブリをインストールすると、厳密な名前の署名の検証はインストール時にのみ行われます。 ファイル システムの他の場所にインストールされている厳密な名前のアセンブリは、読み込まれるたびに署名を検証する必要があります。 GAC にマネージ VSPackages をインストールする場合は、regpkg ツールの **/assembly**スイッチを使用して、アセンブリの厳密な名前を指すレジストリ エントリを書き込みます。

 GAC 以外の場所に管理 VSPackages をインストールする場合は、ディレクトリ階層を選択するためのアンマネージ VSPackages に関する前述のアドバイスに従ってください。 regpkg ツールの **/codebase**スイッチを使用して、VSPackage アセンブリのパスを指すレジストリ エントリを書き込みます。

 詳細については、「 [VSPackages の登録と登録解除](../../extensibility/registering-and-unregistering-vspackages.md)」を参照してください。

## <a name="satellite-dlls"></a>サテライト DLL
 慣例により、特定のロケールのリソースを含む VSPackage サテライト DLL は *、VSPackage*ディレクトリのサブディレクトリに配置されます。 サブディレクトリはロケール ID (LCID) 値に対応します。

 [VSPackages](../../extensibility/managing-vspackages.md)の管理の記事は、レジストリ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]エントリが実際に VSPackage のサテライト DLL を検索する場所を制御することを示します。 ただし、LCID[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]値の名前が付けられたサブディレクトリに、次の順序でサテライト DLL を読み込もうとします。

1. 既定の LCID (Visual Studio LCID;英語の場合は*\1033*など)

2. 既定のサブ言語を使用する既定の LCID。

3. システムの既定の LCID。

4. システムの既定の LCID と既定のサブ言語。

5. 米国英語 (*.\1033*または *.\0x409*) 。

VSPackage DLL にリソースが含まれており **、SatelliteDll\DllName**レジストリ エントリ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]がリソースを指している場合は、上記の順序で読み込みを試みます。

## <a name="see-also"></a>関連項目
- [共有 VS パッケージとバージョン対応 VS パッケージの間で選択](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)
- [VSPackage を管理する](../../extensibility/managing-vspackages.md)
- [パッケージ登録の管理](https://msdn.microsoft.com/library/f69e0ea3-6a92-4639-8ca9-4c9c210e58a1)
