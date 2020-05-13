---
title: RegPkg パッケージ登録のトラブルシューティング |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- RegPkg
ms.assetid: f33f822f-697a-4bad-9c10-554b4c8f6246
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ebae9f7c5b4d1a6dcfee20c3b36c02f8ead2e0bc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704329"
---
# <a name="troubleshooting-regpkg-package-registration"></a>RegPkg パッケージ登録のトラブルシューティング
> [!NOTE]
> Visual Studio でパッケージを登録する場合は、.pkgdef ファイルを使用する方法が推奨されます。 これにより、システム レジストリにアクセスしなくても拡張機能の展開が可能になります。 Pkgdef ファイルは[、CreatePkgDef ユーティリティ](../../extensibility/internals/createpkgdef-utility.md)を使用して作成されます。

 で RegPkg[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を使用してパッケージを登録するには、パッケージに適したバージョンの RegPkg を使用する必要があります。

## <a name="regpkg-versions-related-to-package-versions"></a>パッケージバージョンに関連する RegPkg バージョン
 RegPkg には 2 つのバージョンがあります。 1 つのバージョンが[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]に含まれています。 このバージョンを使用して、次のいずれかのアセンブリを使用してビルドされたパッケージを登録します。

1. Microsoft.VisualStudioShell.9.0.dll

2. Microsoft.VisualStudioShell.10.0.dll

3. Microsoft.VisualStudioShell.11.0.dll

   以前のアセンブリを使用してビルドされたパッケージを登録することはできません。

   RegPkg の以前のバージョンでは、アセンブリを使用してビルドされたパッケージを登録できます。 ただし、そのアセンブリの新しいバージョンを使用してビルドされたパッケージを登録することはできません。

## <a name="see-also"></a>関連項目
- [VSPackages](../../extensibility/internals/vspackages.md)
