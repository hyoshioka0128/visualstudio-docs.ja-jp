---
title: VS パッケージのセキュリティに関するベスト プラクティス |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709903"
---
# <a name="best-practices-for-security-in-vspackages"></a>VS パッケージのセキュリティに関するベスト プラクティス
をコンピューター[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]にインストールするには、管理者資格情報を使用してコンテキストで実行する必要があります。 アプリケーションのセキュリティと配置の基本単位は[、 VSPackage です。](../../extensibility/internals/vspackages.md) [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage は、 を使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]して登録する必要があります。

 管理者は、レジストリとファイル システムに書き込み、コードを実行するための完全なアクセス許可を持っています。 VSPackage を開発、展開、またはインストールするには、これらのアクセス許可が必要です。

 インストールされるとすぐに VSPackage は完全に信頼されます。 VSPackage に関連付けられているアクセス許可のこの高レベルのため、悪意のある VSPackage を誤ってインストールする可能性があります。

 ユーザーは、信頼できるソースからのみ VSPackages をインストールするようにする必要があります。 VSPackage を開発する企業は、改ざんが防止されることをユーザーに保証するために、厳密に名前を付け、署名する必要があります。 VSPackage を開発する企業は、Web サービスやリモート インストールなどの外部依存関係を調査して、セキュリティ問題を評価および修正する必要があります。

 詳細については、「 [.NET Framework のセキュリティで保護されたコーディングのガイドライン](/previous-versions/visualstudio/visual-studio-2008/d55zzx87(v=vs.90))」を参照してください。

## <a name="see-also"></a>関連項目
- [アドインのセキュリティ](https://msdn.microsoft.com/Library/44a5c651-6246-4310-b371-65378917c799)
- [DDEX セキュリティ](https://msdn.microsoft.com/library/44a52a70-5c98-450e-993d-4a3b32f69ba8)
