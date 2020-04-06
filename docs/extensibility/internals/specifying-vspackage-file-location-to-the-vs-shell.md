---
title: VS シェルに VSPackage ファイルの場所を指定する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, file location
- VSPackages, managed package file location
ms.assetid: beb8607a-4183-4ed2-9ac8-7527f11513b1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f112da4e79bff06d12472f0af7a3fe47b2f25da4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704978"
---
# <a name="specifying-vspackage-file-location-to-the-vs-shell"></a>VSPackage ファイルの場所を VS Shell に指定する
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]VSPackage を読み込むアセンブリ DLL を見つける必要があります。 次の表に示すように、さまざまな方法で検索できます。

| Method | 説明 |
| - | - |
| CodeBase レジストリ キーを使用します。 | CodeBase キーを使用して、VSPackage[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]アセンブリを任意の完全修飾ファイル パスから読み込むことができます。 キーの値は、DLL へのファイル パスである必要があります。 これは、パッケージ アセンブリを読[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]み込むには、最適な方法です。 この手法は、"CodeBase/プライベート インストール ディレクトリ技法" と呼ばれることもあります。 登録時に、コードベースの値は、その型のインスタンスを通じて登録属性クラス<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.RegistrationContext>に渡されます。 |
| DLL をプライベート**アセンブリ**ディレクトリに配置します。 | アセンブリをディレクトリの**PrivateAssemblyies**サブディレクトリに[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]配置します。 **Private アセンブリ**内にあるアセンブリは自動的に検出されますが、[**参照の追加**] ダイアログ ボックスには表示されません。 **プライベート アセンブリ**とパブリック**アセンブリ**の違いは、**パブリック アセンブリ**内のアセンブリが **[参照の追加**] ダイアログ ボックスで列挙される点です。 "CodeBase/プライベート インストール ディレクトリ" の手法を使用しない場合は **、PrivateAssemblyies**ディレクトリにインストールする必要があります。 |
| 厳密な名前付きアセンブリとアセンブリレジストリ キーを使用します。 | アセンブリ キーを使用すると、厳密な名前[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]付き VSPackage アセンブリを読み込む際に明示的に指示できます。 キーの値はアセンブリの厳密な名前にする必要があります。 |
| DLL をパブリック**アセンブリ**ディレクトリに配置します。 | 最後に、アセンブリを**PublicAssemblyies**サブディレクトリに配置することもできます。 **Public アセンブリ**内のアセンブリは自動的に検出され、 の [**参照の追加**] ダイアログ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ボックスにも表示されます。<br /><br /> VSPackage アセンブリは、他の VSPackage 開発者によって再利用されるマネージ コンポーネントが含まれている場合にのみ **、PublicAssemblyies**ディレクトリに配置する必要があります。 アセンブリの大半は、この基準を満たしていません。 |

> [!NOTE]
> 厳密な名前を持つ署名付きアセンブリを、すべての依存アセンブリに使用します。 これらのアセンブリは、独自のディレクトリまたはグローバル アセンブリ キャッシュ (GAC) にもインストールする必要があります。 これにより、同じベース ファイル名を持つアセンブリとの競合 (弱い名前のバインド) を防ぐことができます。
