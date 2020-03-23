---
title: Office ソリューションに信頼を付与する
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
ms.openlocfilehash: cf7a68d5d3567305e4f70049d76a1c260ddecf25
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301657"
---
# <a name="grant-trust-to-office-solutions"></a>Office ソリューションに信頼を付与する
  Office ソリューションに信頼を付与するということは、ソリューション アセンブリ、アプリケーション マニフェスト、配置マニフェスト、およびドキュメントを信頼するように各対象コンピュータのセキュリティ ポリシーを変更することです。 信頼は、ユーザーまたはエンド ユーザーによって Office ソリューションに付与できます。

 アプリケーション マニフェストと配置マニフェストに署名することで、Office ソリューションに完全な信頼を付与できます。

 エンド ユーザーは、信頼プロンプトで信頼の決定を行うことによって、Office[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]ソリューションに信頼を付与できます。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="trust-the-solution-by-signing-the-application-and-deployment-manifests"></a><a name="Signing"></a>アプリケーション マニフェストと配置マニフェストに署名することでソリューションを信頼する
 Office ソリューションのすべてのアプリケーション マニフェストと配置マニフェストは、発行元を識別する証明書を使用して署名する必要があります。 証明書は、信頼の決定を行うための基礎となります。

 一時的な証明書が作成され、ビルド時に信頼が付与されるため、デバッグ中にソリューションが実行されます。 一時的な証明書で署名されたソリューションを発行する場合、エンド ユーザーは信頼の決定を行うよう求められます。

 既知の信頼された証明書を使用してソリューションに署名すると、エンド ユーザーに信頼の決定を求めることなく、ソリューションが自動的にインストールされます。 署名用の証明書を取得する方法の詳細については、「 [ClickOnce と Authenticode](../deployment/clickonce-and-authenticode.md)」を参照してください。 証明書を取得した後、証明書を信頼された発行元の一覧に追加して、証明書を明示的に信頼する必要があります。 詳細については、「[方法 : ClickOnce アプリケーションの信頼された発行元をクライアント コンピュータに追加する](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)」を参照してください。

 開発者が一時的な証明書を使用してソリューションに署名した場合、管理者は、Microsoft .NET Framework ツールの 1 つであるマニフェスト生成および編集ツール (*mage.exe*) を使用して、既知の信頼できる証明書を使用してカスタマイズに再署名できます。 ソリューションの署名の詳細については、「[方法 : Office ソリューションに署名する](../vsto/how-to-sign-office-solutions.md)」および「[方法 : アプリケーション マニフェストと配置マニフェストに署名する](../ide/how-to-sign-application-and-deployment-manifests.md)」を参照してください。

## <a name="trust-the-solution-by-using-the-clickonce-trust-prompt"></a><a name="TrustPrompt"></a>ClickOnce 信頼プロンプトを使用してソリューションを信頼する
 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]ソリューションの証明書を信頼する組織全体のポリシーがない場合は、エンド ユーザーに信頼の決定を求めるプロンプトが表示されます。 エンド ユーザーがソリューションに信頼を付与すると、この信頼の決定を格納する URL と公開キーを含む信頼リスト エントリが作成されます。 信頼されたカスタマイズを後で実行しても、エンド ユーザーに対して再びプロンプトが表示されません。

 管理者は、信頼プロンプト[!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]を無効にしたり、Authenticode 証明書で署名されたソリューションに対してのみプロンプトを表示するように要求することができます。 マイ コンピュータ、ローカル イントラネット、インターネット、信頼済みサイト、および信頼されていないサイトの各ゾーンの設定を変更する方法の詳細については、「[方法 : ClickOnce 信頼プロンプトの動作を構成する](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [セキュアなオフィスソリューション](../vsto/securing-office-solutions.md)
- [ドキュメントに信頼を付与する](../vsto/granting-trust-to-documents.md)
- [トラブルシューティング : Office ソリューションのセキュリティ](../vsto/troubleshooting-office-solution-security.md)
- [Office ソリューションのセキュリティに関する具体的な考慮事項](../vsto/specific-security-considerations-for-office-solutions.md)