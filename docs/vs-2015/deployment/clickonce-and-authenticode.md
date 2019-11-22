---
title: ClickOnce and Authenticode | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- .pfx files
- ClickOnce deployment, Authenticode
- Authenticode, ClickOnce
- ClickOnce deployment, certificates
- ClickOnce deployment, security
ms.assetid: ab5b6712-f32a-4e33-842f-e88ab4818ccf
caps.latest.revision: 20
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 06edf9954134a6110f9285fc744c87c2696b19d5
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298274"
---
# <a name="clickonce-and-authenticode"></a>ClickOnce と Authenticode
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Authenticode* is a Microsoft technology that uses industry-standard cryptography to sign application code with digital certificates that verify the authenticity of the application's publisher. アプリケーションの配置に Authenticode を使用し、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] はトロイの木馬のリスクを軽減します。 トロイの木馬は、悪意のある第三者が、確立された信頼できるソースからの正規のプログラムと偽って示すウイルスやその他の有害なプログラムです。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 配置のデジタル証明書による署名は、アセンブリとファイルが改ざんされていないことを確認するためのオプションの手順です。  
  
 以下のセクションでは、Authenticode で使用するさまざまな種類のデジタル証明書、証明機関 (CA) を使用して証明書を検証するしくみ、証明書におけるタイムスタンプの役割、および証明書で使用できるストレージの方法について説明します。  
  
## <a name="authenticode-and-code-signing"></a>Authenticode とコード署名  
 *デジタル証明書* は、証明書の発行先であるアプリケーション発行者と証明書を発行した機関を示すメタデータと共に、暗号化公開キー/秘密キーのペアが格納されたファイルです。  
  
 Authenticode 証明書にはさまざまな種類があります。 それぞれの証明書は、異なる種類の署名用に構成されています。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションの場合、コード署名で有効な Authenticode 証明書が必要です。 電子メールのデジタル証明書など、別の種類の証明書によって [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションへの署名を試みた場合、アプリケーションは動作しません。 詳細については、「 [Introduction to Code Signing](https://go.microsoft.com/fwlink/?LinkId=179452)」 (コード署名の概要) を参照してください。  
  
 コード署名の証明書は、次の 3 つの方法のいずれかで取得することができます。  
  
- 証明書の販売元から購入する。  
  
- デジタル証明書の作成を担当する組織内のグループから受け取る。  
  
- [!INCLUDE[winsdklong](../includes/winsdklong-md.md)]に含まれている MakeCert.exe で独自の証明書を生成する。  
  
### <a name="how-using-certificate-authorities-helps-users"></a>証明機関を使用してユーザーを支援する方法  
 A certificate generated using the MakeCert.exe utility is commonly called a *self-cert* or a *test cert*. This kind of certificate works much the same way that a .snk file works in the .NET Framework. この証明書は、秘密/公開暗号化キーのペアのみで構成され、発行者に関する検証可能な情報を含んでいません。 自己証明書を使用すると、イントラネット上に信頼性の高い [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションを配置できます。 ただし、これらのアプリケーションをクライアント コンピューターで実行した場合は、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] が、不明な発行元からのものとしてアプリケーションを識別します。 既定では、自己証明書によって署名され、インターネットを介して配置された [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションは、信頼されたアプリケーションの配置を利用できません。  
  
 これに対し、証明書販売元や企業内の部門などの CA から証明書を受け取る場合は、証明書によってユーザーのセキュリティが強化されます。 証明書によって、署名済みソフトウェアの発行者が識別されるだけでなく、署名を行った CA に問い合わせてその ID が検査されます。 CA がルート証明機関でない場合、Authenticode はルート証明機関まで "信頼チェーン" をたどって、その CA が証明書の発行を承認されているかどうかを検査します。 セキュリティを強化するために、可能であれば常に CA によって発行された証明書を使用することをお勧めします。  
  
 For more information about generating self-certs, see [Makecert.exe (Certificate Creation Tool)](https://msdn.microsoft.com/library/b0343f8e-9c41-4852-a85c-f8a0c408cf0d).  
  
### <a name="timestamps"></a>タイムスタンプ  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションの署名に使用する証明書は、一定の期間 (通常は 12 か月) で期限切れになります。 新しい証明書を持つアプリケーションに再署名を繰り返さずに済むように、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ではタイムスタンプがサポートされています。 アプリケーションがタイムスタンプ付きで署名されると、タイムスタンプが有効な場合は、有効期限が過ぎていても、その証明書が受け付けられます。 これにより、期限切れの証明書と有効なタイムスタンプを持つ [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションをダウンロードして実行できます。 また、期限切れの証明書を持つインストール済みのアプリケーションでは、引き続き、更新プログラムをダウンロードしてインストールできます。  
  
 アプリケーション サーバーにタイムスタンプを含めるには、タイムスタンプ サーバーが必要です。 タイムスタンプ サーバーを選択する方法については、「 [How to: Sign Application and Deployment Manifests](../ide/how-to-sign-application-and-deployment-manifests.md)」を参照してください。  
  
### <a name="updating-expired-certificates"></a>期限切れの証明書の更新  
 以前のバージョンの .NET Framework では、証明書の期限が切れているアプリケーションを更新すると、そのアプリケーションが機能しなくなる可能性がありました。 この問題を解決するには、次のいずれかの方法を使用します。  
  
- .NET Framework のバージョンを 2.0 SP1 以降 (Windows XP の場合) または 3.5 以降 (Windows Vista の場合) に更新します。  
  
- アプリケーションをアンインストールし、有効な証明書を含む新しいバージョンを再インストールします。  
  
- 証明書を更新するコマンド ライン アセンブリを作成します。 このプロセスの詳細な手順については、 [Microsoft サポートの記事 925521](https://go.microsoft.com/fwlink/?LinkId=179454)を参照してください。  
  
### <a name="storing-certificates"></a>証明書の格納  
  
- 証明書は .pfx ファイルとしてファイル システムに格納できます。また、キー コンテナーの内部に格納することもできます。 Windows ドメインのユーザーは、多数のキー コンテナーを持つことができます。 .pfx に保存するよう指定しない限り、既定では、MakeCert.exe が個人のキー コンテナーに証明書を格納します。 [!INCLUDE[winsdkshort](../includes/winsdkshort-md.md)] 配置の作成に使用する [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ツールである Mage.exe と MageUI.exe を使用すると、このどちらの方法で格納された証明書も使用できます。  
  
## <a name="see-also"></a>参照  
 [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)   
 [ClickOnce アプリケーションのセキュリティ](../deployment/securing-clickonce-applications.md)   
 [信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)   
 [Mage.exe (マニフェストの生成および編集ツール)](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)
