---
title: 他のユーザーが配置できるように ClickOnce アプリケーションを作成する |Microsoft Docs
description: .NET Framework 3.5 と以前のバージョンの .NET Framework で開発された、お客様がホストする ClickOnce アプリケーションについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- preserved branding information
- useManifestForTrust element
- customer deployments [ClickOnce]
- multiple ClickOnce deployment and branding
- ClickOnce applications, previous .NET Framework versions
- application manifests [ClickOnce]
- <useManifestForTrust> element
- manifests [ClickOnce]
- trust applications, ClickOnce
- ClickOnce applications, deployed by others
- ClickOnce applications, previous .NET Framework
ms.assetid: d20766c7-4ef3-45ab-8aa0-3f15b61eccaa
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9554cad786669ae4aa3b9aa84ecd6b996ee196f3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99888473"
---
# <a name="create-clickonce-applications-for-others-to-deploy"></a>開発者以外が配置する ClickOnce アプリケーションを作成する
ClickOnce 配置を作成するすべての開発者が、アプリケーション自体を配置することを計画しているわけではありません。 多くの場合、ClickOnce を使用してアプリケーションをパッケージ化した後、大企業などの顧客にファイルを渡します。 顧客は、ネットワーク上でアプリケーションをホストする責任者になります。 このトピックでは、バージョン3.5 より前のバージョンの .NET Framework におけるこのような展開に固有の問題について説明します。 次に、.NET Framework 3.5 の新しい "信頼のマニフェストを使用する" 機能を使用して提供される新しいソリューションについて説明します。 最後に、以前のバージョンの .NET Framework をまだ使用しているお客様に対して、ClickOnce 配置を作成するための推奨される方法を示します。

## <a name="issues-involved-in-creating-deployments-for-customers"></a>顧客向けのデプロイの作成に関連する問題
 顧客にデプロイを提供する予定の場合、いくつかの問題が発生します。 最初の問題は、コードの署名に関するものです。 ネットワーク全体に配置するには、ClickOnce 配置の配置マニフェストとアプリケーションマニフェストの両方がデジタル証明書で署名されている必要があります。 これにより、マニフェストに署名するときに、開発者の証明書と顧客の証明書のどちらを使用するかについての質問が発生します。

 使用する証明書の質問は、ClickOnce アプリケーションの id が配置マニフェストのデジタル署名に基づいているため、重要です。 開発者が配置マニフェストに署名した場合、顧客が大規模な企業であり、企業の複数の部門がカスタマイズされたバージョンのアプリケーションをデプロイすると、競合が発生する可能性があります。

 たとえば、Adventure Works に財務部門と人事部があるとします。 どちらの部門も、SQL データベースに格納されているデータからレポートを生成する Microsoft Corporation の ClickOnce アプリケーションをライセンスします。 Microsoft では、各部門に、データ用にカスタマイズされたアプリケーションのバージョンを提供しています。 アプリケーションが同じ Authenticode 証明書で署名されている場合、両方のアプリケーションを使用しようとすると、2つ目のアプリケーションが最初のアプリケーションと同一であると見なされるため、エラーが発生します。 この場合、顧客は、アプリケーションによってローカルに保存されたデータの損失を含む、予測できない望ましくない副作用を発生させる可能性があります。

 コード署名に関連するその他の問題として、 `deploymentProvider` 配置マニフェストの要素があります。これは、アプリケーションの更新プログラムを検索する場所を ClickOnce に指示します。 この要素は、署名する前に配置マニフェストに追加する必要があります。 この要素を後で追加する場合は、配置マニフェストを再署名する必要があります。

### <a name="require-the-customer-to-sign-the-deployment-manifest"></a>顧客が配置マニフェストに署名することを要求する
 一意でない配置におけるこの問題の解決策の1つは、開発者がアプリケーションマニフェストに署名し、顧客が配置マニフェストに署名することです。 このアプローチは機能しますが、他の問題が発生します。 Authenticode 証明書は保護された資産のままである必要があるため、顧客はデプロイに署名するための証明書を開発者に提供するだけではありません。 .NET Framework SDK で自由に利用できるツールを使用してデプロイマニフェスト自体に署名することができますが、これにより、お客様が提供するよりも多くの技術的な知識が必要になる場合があります。 このような場合、開発者は通常、アプリケーション、Web サイト、またはその他のメカニズムを作成して、顧客が署名のためにバージョンのアプリケーションを送信できるようにします。

### <a name="the-impact-of-customer-signing-on-clickonce-application-security"></a>ClickOnce アプリケーションセキュリティに対する顧客の署名の影響
 開発者と顧客がアプリケーションマニフェストに署名する必要があることに同意したとしても、アプリケーションの id を囲む他の問題が発生します (特に、信頼されたアプリケーションの展開に適用される場合)。 (この機能の詳細については、「 [信頼されたアプリケーションの展開の概要](../deployment/trusted-application-deployment-overview.md)」を参照してください)。たとえば、Adventure Works は、Microsoft Corporation によって提供されるすべてのアプリケーションが完全信頼で実行されるように、クライアントコンピューターを構成する必要があるとします。 Adventure Works が配置マニフェストに署名する場合、ClickOnce は Adventure Work のセキュリティ署名を使用して、アプリケーションの信頼レベルを決定します。

## <a name="create-customer-deployments-by-using-application-manifest-for-trust"></a>信頼のためにアプリケーションマニフェストを使用して顧客のデプロイを作成する
 .NET Framework 3.5 の ClickOnce には、開発者と顧客が、マニフェストに署名する方法のシナリオに対する新しいソリューションを提供する新しい機能が含まれています。 ClickOnce アプリケーションマニフェストは、という名前の新しい要素をサポートし `<useManifestForTrust>` ています。これにより、開発者は、アプリケーションマニフェストのデジタル署名が、信頼の決定に使用されるものであることを示すことができます。 開発者は、 *Mage.exe*、 *MageUI.exe*、Visual Studio などの ClickOnce パッケージ化ツールを使用して、アプリケーションマニフェストにこの要素を追加するだけでなく、発行元の名前とアプリケーションの名前の両方をマニフェストに埋め込むことができます。

 を使用する場合 `<useManifestForTrust>` 、配置マニフェストは、証明機関によって発行された Authenticode 証明書を使用して署名する必要はありません。 代わりに、自己署名証明書と呼ばれるものを使用して署名することができます。 自己署名証明書は、標準の .NET Framework SDK ツールを使用して顧客または開発者によって生成され、標準の ClickOnce 配置ツールを使用して配置マニフェストに適用されます。 詳細については、「 [MakeCert](/windows/desktop/SecCrypto/makecert)」を参照してください。

 自己署名証明書を配置マニフェストに使用すると、いくつかの利点があります。 顧客が独自の Authenticode 証明書を取得または作成する必要がなくなることで、は `<useManifestForTrust>` 顧客のデプロイを簡略化しながら、開発者はアプリケーションで独自のブランド id を維持することができます。 結果として、セキュリティが強化され、一意のアプリケーション id を持つ一連の署名済み展開が生成されます。 これにより、同じアプリケーションを複数の顧客にデプロイした場合に発生する可能性のある競合が回避されます。

 有効になっている ClickOnce 配置を作成する方法の詳細な手順については `<useManifestForTrust>` 、「 [チュートリアル: 再署名が不要で、ブランド情報を保持する clickonce アプリケーションを手動で配置](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)する」を参照してください。

### <a name="how-application-manifest-for-trust-works-at-run-time"></a>実行時に信頼のアプリケーションマニフェストが動作するしくみ
 実行時にアプリケーションマニフェストを信頼に使用する方法について理解を深めるには、次の例を検討してください。 .NET Framework 3.5 を対象とする ClickOnce アプリケーションは、Microsoft によって作成されます。 アプリケーションマニフェストは要素を使用 `<useManifestForTrust>` し、Microsoft によって署名されています。 Adventure Works は、自己署名証明書を使用して配置マニフェストに署名します。 Adventure Works クライアントは、Microsoft が署名したすべてのアプリケーションを信頼するように構成されています。

 ユーザーが配置マニフェストへのリンクをクリックすると、ClickOnce によってユーザーのコンピューターにアプリケーションがインストールされます。 証明書と配置情報は、クライアントコンピューター上の ClickOnce に対してアプリケーションを一意に識別します。 ユーザーが同じアプリケーションを別の場所から再度インストールしようとすると、ClickOnce はこの id を使用して、アプリケーションがクライアントに既に存在していることを確認できます。

 次に、ClickOnce は、アプリケーションマニフェストに署名するために使用される Authenticode 証明書を調べます。これにより、ClickOnce が付与する信頼のレベルが決まります。 Adventure Works は Microsoft が署名したすべてのアプリケーションを信頼するようにクライアントを構成しているため、この ClickOnce アプリケーションには完全な信頼が付与されます。 詳細については、「[信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)」を参照してください。

## <a name="create-customer-deployments-for-earlier-versions"></a>以前のバージョンの顧客のデプロイを作成する
 以前のバージョンの .NET Framework を使用している顧客に ClickOnce アプリケーションを配置する場合はどうすればよいですか。 以下のセクションでは、推奨されるいくつかのソリューションと、それぞれの長所と短所についてまとめています。

### <a name="sign-deployments-on-behalf-of-customer"></a>顧客に代わってデプロイに署名する
 考えられるデプロイ方法の1つは、顧客独自の秘密キーを使用して、開発者が顧客に代わってデプロイに署名するメカニズムを作成することです。 これにより、開発者は秘密キーまたは複数の展開パッケージを管理する必要がなくなります。 開発者は、各顧客に同じデプロイを提供するだけです。 署名サービスを使用して、環境に合わせてカスタマイズすることはお客様が行う必要があります。

 この方法の欠点の1つは、実装に必要な時間と費用です。 このようなサービスは、.NET Framework SDK に用意されているツールを使用して作成できますが、製品のライフサイクルに追加される開発時間が増えます。

 このトピックで既に説明したように、お客様のアプリケーションのバージョンごとに同じアプリケーション id が使用されるため、競合が発生する可能性があります。 この問題が発生した場合、開発者は、配置マニフェストを生成するときに使用する名前フィールドを変更して、各アプリケーションに一意の名前を付けることができます。 これにより、アプリケーションのバージョンごとに個別の id が作成され、潜在的な id の競合がなくなります。 このフィールドは `-Name` 、Mage.exe の引数と、MageUI.exe の [**名前**] タブの [**名前**] フィールドに対応しています。

 たとえば、開発者がアプリケーション1という名前のアプリケーションを作成したとします。 開発者は、Name フィールドをアプリケーション1に設定して単一のデプロイを作成するのではなく、この名前に対して顧客固有のバリエーション (アプリケーション1、アプリケーション1など) を使用して複数のデプロイを作成できます。

### <a name="deploy-using-a-setup-package"></a>セットアップパッケージを使用して展開する
 もう1つの方法として、Microsoft セットアッププロジェクトを生成して、ClickOnce アプリケーションの初期配置を実行する方法があります。 これは、MSI の展開としてのセットアップ実行可能ファイル () のいずれかの形式で指定できます。EXE) を使用するか、キャビネット (.cab) ファイルとしてバッチスクリプトと共に使用します。

 この手法を使用すると、開発者は、アプリケーションファイル、アプリケーションマニフェスト、およびテンプレートとして機能する配置マニフェストを含む配置を顧客に提供します。 顧客はセットアッププログラムを実行します。これにより、デプロイ URL (ユーザーが ClickOnce アプリケーションをインストールするサーバーまたはファイル共有の場所) とデジタル証明書の入力を求められます。 セットアップアプリケーションでは、更新チェック間隔などの追加の ClickOnce 構成オプションの入力も選択できます。 この情報が収集されると、セットアッププログラムによって実際の配置マニフェストが生成され、署名されて、指定されたサーバーの場所に ClickOnce アプリケーションが発行されます。

 このような状況では、顧客が配置マニフェストに署名する方法は3つあります。

1. 顧客は、証明機関 (CA) によって発行された有効な証明書を使用できます。

2. このアプローチのバリエーションとして、お客様は自己署名証明書を使用して配置マニフェストに署名することを選択できます。 欠点は、インストールするかどうかを確認するメッセージが表示されたときに、アプリケーションで "不明な発行元" という単語が表示されることです。 ただし、これにより、証明機関によって発行された証明書に必要な時間とコストを削減することができなくなります。

3. 最後に、開発者は、独自の自己署名証明書をセットアップパッケージに含めることができます。 これにより、このトピックで既に説明したアプリケーション id に問題が生じる可能性があります。

   セットアップ配置プロジェクトの方法の欠点は、カスタム展開アプリケーションを構築するために必要な時間と費用です。

### <a name="have-customer-generate-deployment-manifest"></a>顧客が配置マニフェストを生成する
 3番目に考えられる展開方法は、アプリケーションファイルとアプリケーションマニフェストのみを顧客に渡すことです。 このシナリオでは、お客様は .NET Framework SDK を使用して配置マニフェストを生成し、署名する責任があります。

 この方法の欠点は、お客様が .NET Framework SDK ツールをインストールする必要があることと、開発者またはシステム管理者がその使用についてのスキルを持っていることです。 一部のお客様は、技術的な労力をほとんどまたはまったく必要としないソリューションを要求する場合があります。

## <a name="see-also"></a>関連項目
- [テストサーバーおよび運用サーバー用の ClickOnce アプリケーションを、署名せずに配置する](../deployment/deploying-clickonce-applications-for-testing-and-production-without-resigning.md)
- [チュートリアル: ClickOnce アプリケーションの手動配置](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
- [チュートリアル: 再署名が不要で商標を保持する ClickOnce アプリケーションの手動配置](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)