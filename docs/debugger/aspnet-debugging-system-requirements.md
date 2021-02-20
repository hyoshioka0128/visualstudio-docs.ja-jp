---
title: 'ASP.NET のデバッグ: システム要件 | Microsoft Docs'
description: Visual Studio と Web アプリが同じコンピューター上で実行される ASP.NET ローカル デバッグとリモート デバッグのためのソフトウェアおよびセキュリティの要件について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging ASP.NET Web applications, system requirements
- debugging ASP.NET Web applications, security requirements
ms.assetid: 7810b9b2-debf-4271-8fc7-1df031123255
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- aspnet
ms.openlocfilehash: 8ab32e855ee93ceb328bc33340597ce65e3ee871
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866100"
---
# <a name="aspnet-debugging-system-requirements"></a>ASP.NET のデバッグ: システム要件
ここでは、 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] のデバッグ シナリオに必要なソフトウェアとセキュリティの要件について説明します。

- ローカル デバッグ。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] と Web アプリケーションが同じコンピューターで実行されている場合のデバッグです。 このシナリオには、2 つのバージョンがあります。

  - [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] コードがファイル システムに存在する場合

  - [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] コードが IIS の Web サイトに存在する場合

- リモート デバッグ。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] はクライアント コンピューターで実行され、リモート サーバー コンピューターで実行されている Web アプリケーションをデバッグします。

## <a name="security-requirements"></a>セキュリティ要件
 リモート デバッグでは、ローカル コンピューターとリモート コンピューターが同じドメイン内または同じワークグループ内にセットアップされている必要があります。

 (アプリケーション プールによってホストされている) [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセス をデバッグするには、そのプロセスをデバッグするアクセス許可が必要です。 既定では、IIS 6.0 より前の [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] アプリケーションは、**ASPNET** ユーザーとして実行されます。 IIS 6.0 および IIS 7.0 では、**NETWORK SERVICE** アカウントが既定値です。 ワーカー プロセスが **ASPNET**(既定) または **NETWORK SERVICE** として実行されている場合、そのプロセスをデバッグするには管理者特権が必要です。

 > [!IMPORTANT]
 > Windows Server 2008 R2 以降、各アプリケーション プールの ID として [ApplicationPoolIdentity](/iis/manage/configuring-security/application-pool-identities) を使用することが推奨されます。

 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスの名前は、デバッグ シナリオや IIS のバージョンによって異なります。 詳細については、[ASP.NET プロセスの名前を見つける](../debugger/how-to-find-the-name-of-the-aspnet-process.md)」を参照してください。

 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスを実行しているユーザー アカウントは、IIS を実行しているサーバーの machine.config ファイルを編集することによって変更できます。 これを行うには、 **インターネット インフォメーション サービス (IIS) マネージャー** を使用するのが最善です。 詳細については、[ユーザー アカウントでワーカー プロセスを実行する](../debugger/how-to-run-the-worker-process-under-a-user-account.md)」を参照してください。

 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスを自分のユーザー アカウントで実行するように変更する場合、IIS を実行しているサーバーの管理者である必要はありません。

> [!CAUTION]
> [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスを別のアカウントで実行するように変更する場合は、 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスがそのアカウントで実行中にハックされた場合の影響を考慮する必要があります。 ASPNET および NETWORK SERVICE の各ユーザー アカウントは最小限のアクセス許可で実行されるので、プロセスがハックされた場合の損害が少なくなります。 高い権限のアクセス許可を持つアカウントで [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスを実行する必要がある場合、損害が大きくなる可能性があります。

## <a name="see-also"></a>関連項目

- [ASP.NET アプリケーションをデバッグする](../debugger/how-to-enable-debugging-for-aspnet-applications.md)
- [方法: ユーザー アカウントでワーカー プロセスを実行する](../debugger/how-to-run-the-worker-process-under-a-user-account.md)