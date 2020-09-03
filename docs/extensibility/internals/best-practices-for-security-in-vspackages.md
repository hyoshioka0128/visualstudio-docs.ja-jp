---
title: Vspackage のセキュリティに関するベストプラクティス |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- security [Visual Studio SDK]
- security best practices, VSPackages
- best practices, security
ms.assetid: 212a0504-cf6c-4e50-96b0-f2c1c575c0ff
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d4309feeed3233d2149586afb1bf4efafacb21ec
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80709903"
---
# <a name="best-practices-for-security-in-vspackages"></a>Vspackage のセキュリティに関するベストプラクティス
コンピューターにをインストールするには、 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 管理者資格情報を持つコンテキストでを実行している必要があります。 アプリケーションのセキュリティと展開の基本単位 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、 [VSPackage](../../extensibility/internals/vspackages.md)です。 VSPackage は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、管理者の資格情報も必要とするを使用して登録する必要があります。

 管理者は、レジストリとファイルシステムに書き込み、任意のコードを実行するための完全なアクセス許可を持っています。 VSPackage を開発、展開、またはインストールするには、これらのアクセス許可を持っている必要があります。

 インストールが完了するとすぐに、VSPackage は完全に信頼されます。 この高いレベルのアクセス許可が VSPackage に関連付けられているため、悪意のある意図を持つ VSPackage を誤ってインストールする可能性があります。

 ユーザーは、信頼できるソースからのみ Vspackage をインストールする必要があります。 Vspackage を開発する企業は、ユーザーの改ざんを防止するために、厳密に名前を付けて署名する必要があります。 Vspackage を開発する企業は、web サービスやリモートインストールなどの外部の依存関係を調べて、セキュリティ上の問題を評価し、修正する必要があります。

 詳細については、「 [.NET Framework の安全なコーディングのガイドライン](/previous-versions/visualstudio/visual-studio-2008/d55zzx87(v=vs.90))」を参照してください。

## <a name="see-also"></a>関連項目
- [アドインのセキュリティ](https://msdn.microsoft.com/Library/44a5c651-6246-4310-b371-65378917c799)
- [DDEX のセキュリティ](https://msdn.microsoft.com/library/44a52a70-5c98-450e-993d-4a3b32f69ba8)
