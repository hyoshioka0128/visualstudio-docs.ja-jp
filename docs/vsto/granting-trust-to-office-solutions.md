---
title: Office ソリューションへの信頼の付与
description: Office ソリューションに信頼を付与するには、各ターゲットコンピューターのセキュリティポリシーを変更して、ソリューションアセンブリ、配置マニフェスト、およびドキュメントを信頼するようにします。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- security [Office development in Visual Studio], trust
- inclusion lists [Office development in Visual Studio], about inclusion lists
- trust [Office development in Visual Studio], 2007 Office system
- granting trust [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f0b81c034ed0f8934da378dc214191d3be1f4506
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96848327"
---
# <a name="grant-trust-to-office-solutions"></a>Office ソリューションへの信頼の付与
  Office ソリューションへの信頼の付与とは、ソリューションアセンブリ、アプリケーションマニフェスト、配置マニフェスト、およびドキュメントを信頼するように、各ターゲットコンピューターのセキュリティポリシーを変更することを意味します。 信頼は、ユーザーまたはエンドユーザーが Office ソリューションに付与できます。

 アプリケーションマニフェストと配置マニフェストに署名することによって、Office ソリューションに対する完全な信頼を付与することができます。

 エンドユーザーは、信頼プロンプトで信頼の決定を行うことによって、Office ソリューションに信頼を付与することができ [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] ます。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="trust-the-solution-by-signing-the-application-and-deployment-manifests"></a><a name="Signing"></a> アプリケーションマニフェストと配置マニフェストに署名することによってソリューションを信頼する
 Office ソリューションのすべてのアプリケーションマニフェストと配置マニフェストは、発行元を識別する証明書で署名されている必要があります。 証明書は、信頼の決定を行うための基礎となります。

 一時的な証明書が作成され、ビルド時に信頼が付与されるため、デバッグ中にソリューションが実行されます。 一時的な証明書で署名されたソリューションを発行すると、エンドユーザーに対して信頼の決定を求めるメッセージが表示されます。

 既知の信頼された証明書を使用してソリューションに署名すると、エンドユーザーに対して信頼の決定を求めることなく、ソリューションが自動的にインストールされます。 署名用の証明書を取得する方法の詳細については、「 [ClickOnce と Authenticode](../deployment/clickonce-and-authenticode.md)」を参照してください。 証明書を取得した後は、信頼された発行元の一覧に証明書を追加することで、証明書を明示的に信頼する必要があります。 詳細については、「 [方法: ClickOnce アプリケーション用の信頼された発行者をクライアントコンピューターに追加する](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)」を参照してください。

 開発者が一時的な証明書を使用してソリューションに署名する場合、管理者は、Microsoft .NET Framework ツールの1つであるマニフェスト生成および編集ツール (*mage.exe*) を使用して、既知の信頼された証明書でカスタマイズを再署名できます。 ソリューションの署名の詳細については、「 [方法: Office ソリューション](../vsto/how-to-sign-office-solutions.md) に署名する」および「 [方法: アプリケーションマニフェストと配置マニフェストに署名する](../ide/how-to-sign-application-and-deployment-manifests.md)」を参照してください。

## <a name="trust-the-solution-by-using-the-clickonce-trust-prompt"></a><a name="TrustPrompt"></a>ClickOnce 信頼プロンプトを使用してソリューションを信頼する
 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] ソリューションの証明書を信頼する組織全体のポリシーがない場合に、エンドユーザーに対して信頼の決定を求めるプロンプトを表示します。 エンドユーザーがソリューションに信頼を付与すると、信頼の決定を格納するための URL と公開キーを含む、包含リストエントリが作成されます。 信頼されたカスタマイズを後で実行すると、エンドユーザーに対して再度要求されることはありません。

 管理者は、信頼プロンプトを無効にし [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] たり、Authenticode 証明書で署名されたソリューションに対してのみプロンプトが表示されるようにすることができます。 MyComputer、LocalIntranet、インターネット、TrustedSites、および UntrustedSites ゾーンのこれらの設定を変更する方法の詳細については、「 [方法: ClickOnce 信頼プロンプトの動作を構成](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)する」を参照してください。

## <a name="see-also"></a>関連項目

- [セキュリティで保護された Office ソリューション](../vsto/securing-office-solutions.md)
- [ドキュメントへの信頼の付与](../vsto/granting-trust-to-documents.md)
- [Office ソリューションのセキュリティに関するトラブルシューティング](../vsto/troubleshooting-office-solution-security.md)
- [Office ソリューションに関する特定のセキュリティの考慮事項](../vsto/specific-security-considerations-for-office-solutions.md)