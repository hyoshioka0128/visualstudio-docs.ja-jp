---
title: 信頼されたアプリケーションの配置の概要 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, install without prompting
- ClickOnce deployment, security
- trusted application deployment
ms.assetid: b24a1702-8fbe-45b1-87a0-9618a0708f1d
caps.latest.revision: 33
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a95392525826fcfb2595e1bac7d45ebea20317fc
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74294699"
---
# <a name="trusted-application-deployment-overview"></a>信頼されたアプリケーションの配置の概要
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、信頼されたアプリケーションの配置テクノロジを使用して、昇格されたアクセス許可を持つ [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションを配置する方法の概要を示します。  
  
 信頼されたアプリケーションの配置テクノロジは、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 配置のテクノロジの一部です。このテクノロジを使用すると、どのような規模の組織でも、ユーザーに確認することなく、従来より安全な方法でマネージド アプリケーションにアクセス許可を付与できます。 信頼されたアプリケーションの配置の場合、組織に必要な処理は、信頼された発行元の一覧をクライアント コンピューターで構成することだけです。発行元は、Authenticode 証明書を使用して識別します。 その後は、信頼された発行元のいずれかによって署名されている [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションには、通常より高いレベルの信頼が与えられます。  
  
> [!NOTE]
> 信頼されたアプリケーションの配置では、ユーザー コンピューターの構成を一度だけ実行する必要があります。 管理されたデスクトップ環境では、グローバル ポリシーを使用してこの構成を実行できます。 この方法がアプリケーションに適さない場合は、代わりに、アクセス許可を昇格する機能を使用します。 詳細については、「[ClickOnce アプリケーションの発行](../deployment/securing-clickonce-applications.md)」を参照してください。  
  
## <a name="trusted-application-deployment-basics"></a>信頼されたアプリケーションの配置の基本  
 次の表は、信頼されたアプリケーションの配置に関連するオブジェクトおよびロールを示しています。  
  
|オブジェクトまたはロール|説明|  
|--------------------|-----------------|  
|管理者●かんりしゃ○|クライアント コンピューターの更新と保守を担当する組織エンティティです。|  
|信頼マネージャー|クライアント アプリケーションに対するセキュリティ処理を実施する、共通言語ランタイム (CLR) 内のサブシステムです。|  
|発行元|アプリケーションに関する記述と保守を実行するエンティティです。|  
|配置元|アプリケーションをパッケージ化し、ユーザーに配布するエンティティです。|  
|証明書|公開キーと秘密キーで構成される暗号化署名です。一般には、その信頼性を保証できる証明機関 (CA: Certification Authority) から発行されます。|  
|Authenticode 証明書|この証明書を使用できるユーザーの情報などを記述したメタデータを埋め込んだ証明書です。|  
|証明機関|発行元の ID を検査し、それらの発行元に、発行元のメタデータを埋め込んだ証明書を発行する組織です。|  
|root authority|他の証明機関が証明書を発行することを承認する証明機関です。|  
|キー コンテナー|証明書を格納するための Microsoft Windows の論理ストレージ領域です。|  
|信頼された発行元|クライアント コンピューターの証明書信頼リスト (CTL: Certificate Trust List) に Authenticode 証明書が追加された発行元です。|  
  
 大規模な組織では、発行元と配置元のエンティティが異なる場合が少なくありません。  
  
- 発行元は、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションを作成するグループです。  
  
- 配置元は、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションを企業のデスクトップ コンピューターに配布するグループ (通常は、情報技術 (IT) 部門) です。  
  
  信頼されたアプリケーションの配置を活用するには、次の手順に従う必要があります。  
  
1. 発行元の証明書を取得します。  
  
2. 発行元をすべてのクライアント コンピューターの信頼された発行元ストアに追加します。  
  
3. [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションを作成します。  
  
4. 発行元の証明書で配置マニフェストに署名します。  
  
5. アプリケーション配置をクライアント コンピューターに発行します。  
  
### <a name="obtain-a-certificate-for-the-publisher"></a>発行元の証明書を取得する  
 デジタル証明書は、Microsoft Authenticode 認証およびセキュリティ システムの主要なコンポーネントです。 Authenticode は、Windows オペレーティング システムの標準機能です。 すべての [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションには、信頼されたアプリケーションの配置の対象であるかどうかにかかわらず、デジタル証明書によって署名する必要があります。 Authenticode と [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]の連携の詳細については、「 [ClickOnce と authenticode](../deployment/clickonce-and-authenticode.md)」を参照してください。  
  
### <a name="add-the-publisher-to-the-trusted-publishers-store"></a>発行元を信頼された発行元ストアに追加する  
 開発した [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションに高いレベルの信頼を与えるには、そのアプリケーションを実行する各クライアント コンピューターに対して、発行元の証明書を信頼された発行元として追加する必要があります。 これは 1 回だけ実行する構成タスクです。 この構成が完了すると、同じ発行元の証明書で署名された [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションを必要なだけ配置し、そのすべてに高い信頼を与えて実行できます。  
  
 Windows オペレーティング システムを実行する会社のイントラネットなど、管理されたデスクトップ環境にアプリケーションを配置する場合には、グループ ポリシーと一緒に新しい証明書信頼リスト (CTL) を作成することによって、信頼された発行者元クライアント コンピューターの発行元ストアに追加できます。 詳細については、「 [グループ ポリシー オブジェクト用の証明書信頼リストを作成する](https://go.microsoft.com/fwlink/?LinkId=102576)」を参照してください。  
  
 管理されたデスクトップ環境にアプリケーションを配置しない場合には、次のような方法で信頼された発行元ストアに証明書を追加できます。  
  
- <xref:System.Security.Cryptography?displayProperty=fullName> 名前空間。  
  
- CertMgr.exe。これは、Internet Explorer のコンポーネントであるため、Windows 98 以降の全バージョンに含まれています。 詳細については、「 [certmgr.exe (証明書マネージャーツール)](https://msdn.microsoft.com/library/7e953b43-1374-4bbc-814f-53ca1b6b52bb)」を参照してください。  
  
### <a name="create-a-clickonce-application"></a>ClickOnce アプリケーションを作成する  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションは、マニフェスト ファイルと組み合わされた [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] クライアント アプリケーションです。マニフェスト ファイルでは、アプリケーションについての説明を記述し、インストール パラメーターを指定します。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] の **[発行]** コマンドを使用すると、開発したプログラムを [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]アプリケーションに変換できます。 または、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] に含まれているツールを使用して、 [!INCLUDE[winsdklong](../includes/winsdklong-md.md)]配置に必要なすべてのファイルを生成することもできます。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 配置の詳細な手順については、「[チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」を参照してください。  
  
 信頼されたアプリケーションの配置は [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]に特有の機能であり、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションに対してのみ使用できます。  
  
### <a name="sign-the-deployment"></a>配置に署名する  
 使用する証明書を取得したら、この証明書を使用して配置に署名する必要があります。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の発行ウィザードを使用してアプリケーションを配置する場合は、独自に証明書を指定しなければ、ウィザードが自動的にテスト証明書を生成します。 また、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の [プロジェクト デザイナー] ウィンドウを使用して、CA から取得した証明書を指定することもできます。  「 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](https://msdn.microsoft.com/library/31kztyey\(v=vs.110\)) 」または「 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](https://msdn.microsoft.com/library/31kztyey\(v=vs.110\))」も参照してください。  
  
> [!CAUTION]
> テスト証明書を使用してアプリケーションを配置することはお勧めできません。  
  
 また、SDK の Mage.exe ツールまたは MageUI.exe ツールを使用してアプリケーションに署名することもできます。 詳細については、「[チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」を参照してください。 配置の署名に関連するコマンドラインオプションの完全な一覧については、「 [mage.exe (マニフェスト生成および編集ツール)](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)」を参照してください。  
  
### <a name="publish-the-application"></a>アプリケーションを発行する  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] マニフェストに署名した後は、すぐにアプリケーションをインストール場所に発行できます。 インストール場所には、Web サーバー、ファイル共有、またはローカル ディスクを使用できます。 信頼マネージャーは、クライアントが配置マニフェストに初めてアクセスした時点で、インストール済みの信頼された発行元を参照して、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションの実行時に高いレベルの権限を与えるかどうかを判断する必要があります。 信頼マネージャーは、配置に署名する際に使用された証明書と、クライアントの信頼された発行元ストアに格納されている証明書とを比較することによって、この判断をします。 信頼マネージャーが一致する証明書を検出した場合は、アプリケーションの実行時に高い信頼が与えられます。  
  
## <a name="trusted-application-deployment-and-permission-elevation"></a>信頼されたアプリケーションの配置とアクセス許可の昇格  
 現在の発行元が信頼された発行元でない場合、信頼マネージャーは、アプリケーションのアクセス許可を昇格するためにアクセス許可の昇格機能を使用するかどうかをユーザーに確認します。 ただし、管理者がアクセス許可の昇格を無効にしている場合、アプリケーションは実行のためのアクセス許可を取得できません。 アプリケーションは実行されず、ユーザーに通知が表示されることもありません。 アクセス許可の昇格の詳細については、「 [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)」を参照してください。  
  
## <a name="limitations-of-trusted-application-deployment"></a>信頼されたアプリケーションの配置に関する制限事項  
 信頼されたアプリケーションの配置は、Web 経由または会社のファイル共有から配置される [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションに昇格された信頼を与えるために使用できます。 CD で配布される [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションには既定で完全信頼が付与されるため、信頼されたアプリケーションの配置を使用する必要はありません。  
  
## <a name="see-also"></a>関連項目  
 [Mage.exe (マニフェストの生成および編集ツール)](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)   
 [チュートリアル : ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
