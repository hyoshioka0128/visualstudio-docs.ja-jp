---
title: MPSA での Visual Studio サブスクリプション | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: b331c837-3524-42b7-820e-b4fdd5e12793
ms.date: 09/03/2020
ms.topic: conceptual
description: マイクロソフト製品とサービス契約 (MPSA) での Visual Studio サブスクリプションの管理について説明します
ms.openlocfilehash: 9d26bccebb11a59933c37ec0f29a9b6e30e86c5b
ms.sourcegitcommit: f8d14fab194fcb30658f23f700da07d35ffc9d4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89561391"
---
# <a name="visual-studio-subscriptions-in-a-microsoft-products-and-services-agreement-mpsa"></a>マイクロソフト製品/サービス契約 (MPSA) の Visual Studio サブスクリプション
MPSA プログラムを使用して Visual Studio サブスクリプションを購入した場合、Visual Studio サブスクリプション管理者になってサブスクリプションをユーザーに割り当てる前に、いくつか注意が必要な点があります。 管理者として既に設定されている場合は、Visual Studio サブスクリプション[管理ポータル](https://manage.visualstudio.com/)に直接進むことができます。

MPSA のお客様は、MPSA を通じて購入した資産を、ボリューム ライセンス サービス センター (VLSC) と同様の機能をサポートする[ビジネス センター](https://businessaccount.microsoft.com/Customer)と呼ばれるポータルで管理します。 たとえば、ライセンスの概要、注文、ダウンロード、キー、ユーザーなどが表示されます。ただし、MPSA の Visual Studio サブスクリプションの機能は、クラウド サービスとよく似ています。 ビジネス センターでは、Microsoft アカウント (MSA) の代わりに職場アカウントを使用してサインインすることもできます。 組織で Office 365 や Azure Active Directory などのクラウド サービスを使用していて、これら 2 つのサービスのいずれかにメール アドレスが使用されている場合、そのメール アドレスは職場アカウントです。 そのため、既存のパスワードを使用してビジネス センターに登録することができます。 組織がクラウド サービスを使用しておらず、メール アドレスが職場アカウントではない場合でも、そのメール アドレスで問題なくビジネス センターに登録できます。

また、Visual Studio サブスクリプション管理者になると、Visual Studio サブスクリプション[管理ポータル](https://manage.visualstudio.com/)でサブスクリプションを割り当てることができます。 MPSA では、Visual Studio サブスクリプションをそれぞれの管理ポータル (Visual Studio サブスクリプション管理ポータル) にプロビジョニングする必要があります。 この場合、購入アカウントをテナント (つまり contoso.onmicrosoft.com) に関連付ける必要があります。

2 種類のテナント (マネージド テナントとアンマネージド テナント) があることに注意してください。 管理対象のテナントとは、既に組織内の管理者によって管理されているテナントを指します。

アンマネージド テナントとは、管理者が割り当てられていないテナントであり、Office 365 などのオンライン サービスには使用できません。 アンマネージド テナントは、職場アカウントではないメール アドレスを使用してビジネス センターに登録するときにも作成されます。 ビジネス センターに登録するときにパスワードを作成するように求められた場合、そのメール アドレスは職場アカウント内にはなく、アンマネージド テナントが作成されたことを示します。

テナントの関連付けを完了する前に、Visual Studio サブスクリプション管理者になるための要件と手順がいくつかあります。

## <a name="pre-tenant-association-managed-tenant"></a>テナントの関連付け前 (管理対象のテナント)
- ビジネス センターの登録ユーザーである必要があります。
- 属しているテナント内の (少なくとも) ユーザー管理者またはグローバル管理者である必要があります (この要件は、会社が既に Cloud Services を使用している場合に適用されます)。 いずれのロールも Visual Studio サブスクリプション管理者である必要があります。
- 購入アカウントをテナントに関連付けるには、属しているテナントのグローバル管理者である必要があります。
- ビジネス センターのアカウント管理者またはアカウント マネージャーである必要があります。
- [Azure](https://portal.azure.com/) のユーザー プロファイル (および他のユーザー) の [国または地域] フィールドは、リージョン (米国、CA など) に応じて適切に設定する必要があります。 

> [!NOTE]
> Visual Studio サブスクリプション管理者にするすべてのユーザーは、2 と 5 の条件を満たす必要があるだけなので、ビジネス センターのユーザーである必要はありません。

上記の条件を満たしたら、以下の手順に従って購入アカウントをテナントに関連付けることができます。
1. [ビジネス センター](https://businessaccount.microsoft.com/Customer)にログインします。
2. **[アカウント]** タブをクリックし、 **[Associate Domains]\(ドメインの関連付け\)** を選択します。
3. (購入アカウントを複数持っている場合は) **[Purchasing Account]\(購入アカウント\)** を選択します。
4. **テナント** (つまり contoso.onmicrosoft.com) を選択します。
5. **[Associate Domain]\(ドメインの関連付け\)** をクリックします。

関連付けが行われると、条件を満たすすべてのユーザーは、通常は数分で Visual Studio のサブスクリプション管理者としてプロビジョニングされます。 ただし、最大 24 時間かかることもあります。 テナントがプロビジョニングされると、Visual Studio サブスクリプション管理ポータルにアクセスできるようになります。 24 時間よりも長くかかる場合は、次の手順に従って MPSA サポートにお問い合わせください。
1. <https://www.microsoft.com/licensing/mpsa/default> に接続します。
2. ページの上部にある **[詳細]** メニューをクリックします。 
3. **[サポート]** を選択します。
4. **[Licensing support]\(ライセンス サポート\)** を選択します。
5. 自分のニーズに最適なサポート オプションを選択します。 

> [!NOTE]
> 手順 2 と 5 (関連付け後) の条件を満たした新規ユーザーがいる場合は、MPSA サポートに連絡する必要があります。 MPSA サポートは、新しい Visual Studio サブスクリプション管理者のプロビジョニングを支援します。

## <a name="tenant-association-unmanaged"></a>テナントの関連付け (管理対象外)
前述したように、職場アカウントではない (Azure Active Directory "Azure AD" に登録されていない) メール アドレスでビジネス センターに登録した場合、テナントの関連付け方法の一部が異なります。 "ドメインの引き継ぎ" と呼ばれるプロセスを実行する必要があります。 このプロセスでは、自分をグローバル管理者にして、テナントをアンマネージドからマネージドに変更します。

このプロセスの詳細については、「[クイック スタート ガイド](https://www.microsoft.com/Licensing/existing-customer/business-center-training-and-resources.aspx)」を参照してください。 ドメインの引き継ぎ手順が説明されている「*オンライン サービスを設定し使用する*」というガイドをダウンロードしてください。 このプロセスを完了すると、購入アカウントもテナントに関連付けられます。

> [!NOTE]
> ドメインの引き継ぎプロセスを完了したら、「テナントの関連付け前 (管理対象のテナント)」セクションの 5 つの手順の条件を満たす必要があります。 条件を満たした後に必要な手順は、MPSA サポートに連絡して追加の Visual Studio サブスクリプション管理者をプロビジョニングすることのみです。

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps ドキュメント](https://docs.microsoft.com/azure/devops/)
- [Azure ドキュメント](https://docs.microsoft.com/azure/)
- [Microsoft 365 ドキュメント](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>次の手順
Visual Studio サブスクリプションの管理に関する詳細情報をご覧ください。
- [個別のサブスクリプションの割り当て](assign-license.md)
- [複数のサブスクリプションを管理する](assign-license-bulk.md)
- [サブスクリプションの編集](edit-license.md)
- [サブスクリプションの削除](delete-license.md)
- [最大使用量の確認](maximum-usage.md)
