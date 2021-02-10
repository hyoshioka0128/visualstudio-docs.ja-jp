---
title: RegPkg パッケージ登録のトラブルシューティング |Microsoft Docs
description: この情報を使用して、Visual Studio での RegPkg パッケージ登録のトラブルシューティングを行います。 パッケージに適したバージョンの RegPkg を使用します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: troubleshooting
helpviewer_keywords:
- RegPkg
ms.assetid: f33f822f-697a-4bad-9c10-554b4c8f6246
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4b73f968d51cb15cde910a5bcbd7e541007f22fe
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99959468"
---
# <a name="troubleshooting-regpkg-package-registration"></a>RegPkg パッケージ登録のトラブルシューティング
> [!NOTE]
> Visual Studio でパッケージを登録するには、pkgdef ファイルを使用することをお勧めします。 これにより、システムレジストリにアクセスしなくても拡張機能を展開できます。 Pkgdef ファイルは、 [Createpkgdef ユーティリティ](../../extensibility/internals/createpkgdef-utility.md)を使用して作成されます。

 で RegPkg を使用してパッケージを登録するには [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、パッケージに適したバージョンの RegPkg を使用する必要があります。

## <a name="regpkg-versions-related-to-package-versions"></a>パッケージのバージョンに関連する RegPkg のバージョン
 RegPkg には2つのバージョンがあります。 には1つのバージョンが含まれてい [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 このバージョンを使用して、次のいずれかのアセンブリを使用して作成されたパッケージを登録します。

1. Microsoft.VisualStudioShell.9.0.dll

2. Microsoft.VisualStudioShell.10.0.dll

3. Microsoft.VisualStudioShell.11.0.dll

   以前の Microsoft.VisualStudio.Shell.dll アセンブリを使用してビルドされたパッケージを登録することはできません。

   以前のバージョンの RegPkg では、Microsoft.VisualStudio.Shell.dll アセンブリを使用してビルドされたパッケージを登録できます。 ただし、新しいバージョンのアセンブリを使用してビルドされたパッケージを登録することはできません。

## <a name="see-also"></a>関連項目
- [VSPackages](../../extensibility/internals/vspackages.md)
- [Visual Studio トラブルシューティング](/troubleshoot/visualstudio/welcome-visual-studio/)
