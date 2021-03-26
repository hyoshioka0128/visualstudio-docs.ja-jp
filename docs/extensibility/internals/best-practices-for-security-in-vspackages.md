---
title: Vspackage のセキュリティに関するベストプラクティス |Microsoft Docs
description: VSPackage におけるセキュリティのベストプラクティスについて説明します。これは、Visual Studio アプリケーションのセキュリティとデプロイの基本単位です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- security [Visual Studio SDK]
- security best practices, VSPackages
- best practices, security
ms.assetid: 212a0504-cf6c-4e50-96b0-f2c1c575c0ff
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cca66d6c1fce0deb8103a7d626c16a4e81bc7b5f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086210"
---
# <a name="best-practices-for-security-in-vspackages"></a>Vspackage のセキュリティに関するベストプラクティス
コンピューターにをインストールするには、 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 管理者資格情報を持つコンテキストでを実行している必要があります。 アプリケーションのセキュリティと展開の基本単位 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、 [VSPackage](../../extensibility/internals/vspackages.md)です。 VSPackage は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、管理者の資格情報も必要とするを使用して登録する必要があります。

 管理者は、レジストリとファイルシステムに書き込み、任意のコードを実行するための完全なアクセス許可を持っています。 VSPackage を開発、展開、またはインストールするには、これらのアクセス許可を持っている必要があります。

 インストールが完了するとすぐに、VSPackage は完全に信頼されます。 この高いレベルのアクセス許可が VSPackage に関連付けられているため、悪意のある意図を持つ VSPackage を誤ってインストールする可能性があります。

 ユーザーは、信頼できるソースからのみ Vspackage をインストールする必要があります。 Vspackage を開発する企業は、ユーザーの改ざんを防止するために、厳密に名前を付けて署名する必要があります。 Vspackage を開発する企業は、web サービスやリモートインストールなどの外部の依存関係を調べて、セキュリティ上の問題を評価し、修正する必要があります。

 詳細については、「 [.NET Framework の安全なコーディングのガイドライン](/previous-versions/visualstudio/visual-studio-2008/d55zzx87(v=vs.90))」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [アドインのセキュリティ](/previous-versions/1326zbk3(v=vs.140))
- [DDEX のセキュリティ](/previous-versions/bb163703(v=vs.140))