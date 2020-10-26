---
title: FIPS 140-2 承認の操作モードを Visual Studio でサポート
ms.date: 04/14/2020
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4d06204fd1ef6ee2deb5eadc514af1ede8ae9bb6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "84180494"
---
# <a name="visual-studio-support-for-the-fips-140-2-approved-mode-of-operation"></a>FIPS 140-2 承認の操作モードを Visual Studio でサポート

[バージョン 16.4](/visualstudio/releases/2019/release-notes-v16.4/) 以降の Visual Studio 2019 では、Federal Information Processing Standard (FIPS) Publication 140-2 で承認されている Windows、Azure、.NET の操作モードがサポートされています。 また、[バージョン 16.5](/visualstudio/releases/2019/release-notes-archive-v16.5) の Visual Studio では、[リモート Linux システムを対象とする C++ アプリケーション](/cpp/linux/set-up-fips-compliant-secure-remote-linux-development/)を開発するとき、FIPS 140-2 承認の操作モードがサポートされるようになりました。

Visual Studio のために FIPS 140-2 承認の操作モードを構成するには、[.NET Framework 4.8 をインストールし](https://dotnet.microsoft.com/download/dotnet-framework/net48)、 **[システム暗号化: 暗号化、ハッシュ、署名のための FIPS 準拠アルゴリズムを使う]** というグループ ポリシー設定を有効にします。

FIPS 140-2 承認の操作モードとそれを有効化する方法については、「[FIPS 140-2 の検証](/windows/security/threat-protection/fips-140-validation/)」を参照してください。

> [!NOTE]
> iOS や Android など、Microsoft 以外のプラットフォームのためにアプリを開発する目的で使用するツールでは、FIPS 準拠のアルゴリズムが使われないことがあります。 Visual Studio に含まれているサードパーティ製ソフトウェアまたはユーザーがインストールする拡張機能でも、FIPS 140-2 準拠のアルゴリズムが使われない場合があります。 また、[SharePoint](/sharepoint/security-for-sharepoint-server/federal-information-processing-standard-security-standards/) ソリューションの開発は FIPS 140-2 承認の操作モードに対応していません。

## <a name="next-steps"></a>次の手順

Visual Studio や Microsoft のその他の製品やサービスのための FIPS 140-2 承認の操作モードに関する詳細については、次のリンクをご覧ください。

- [Visual Studio:FIPS 準拠の安全なリモートの C++ による Linux 開発の設定](/cpp/linux/set-up-fips-compliant-secure-remote-linux-development/)
- [Windows:システム暗号化と、暗号化、ハッシュ、署名のための FIPS 準拠アルゴリズムの使用](/windows/security/threat-protection/security-policy-settings/system-cryptography-use-fips-compliant-algorithms-for-encryption-hashing-and-signing)
- [.NET Core:FIPS 準拠](/dotnet/standard/security/fips-compliance/)

## <a name="see-also"></a>関連項目

[セキュリティで保護されたアプリケーション](securing-applications.md)
