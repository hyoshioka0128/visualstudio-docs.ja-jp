---
title: Visual Studio サブスクリプションでの Microsoft Windows Virtual Desktop | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 872c5746-5357-4764-949b-aa525a0adf1a
ms.date: 09/08/2020
ms.topic: conceptual
description: Visual Studio サブスクリプションを使用して Microsoft Windows Virtual Desktop を活用する方法について説明します
ms.openlocfilehash: f598aca8d277ca443b10dac289fae756ccd95432
ms.sourcegitcommit: f8d14fab194fcb30658f23f700da07d35ffc9d4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89561365"
---
# <a name="access-windows-virtual-desktop-in-subscriptions"></a>サブスクリプション内で Windows Virtual Desktop にアクセスする 
Visual Studio のサブスクライバーは、Microsoft Windows Virtual Desktop サービスで Azure Dev/Test の個人クレジットを使用できるようになりました。  
Windows Virtual Desktop は、クラウド上で実行される包括的なデスクトップおよびアプリの仮想化サービスです。 これは、簡素化された管理、マルチセッション Windows 10、Microsoft 365 Apps for enterprise 向けの最適化、リモート デスクトップ サービス (RDS) 環境のサポートを提供する、唯一の仮想デスクトップ インフラストラクチャ (VDI) です。 Windows デスクトップとアプリを数分で Azure にデプロイして拡張し、組み込みのセキュリティとコンプライアンスの機能を利用できます。
Azure 上の Windows Virtual Desktop でできることは次のとおりです。
- マルチセッションの Windows 10 デプロイを設定し、スケーラビリティを備えた完全版の Windows 10 を提供
- Microsoft 365 Apps for enterprise を仮想化および最適化し、マルチユーザーの仮想シナリオで運用
- Windows 7 仮想デスクトップに無料の延長セキュリティ更新プログラムを提供
- 既存のリモート デスクトップ サービス (RDS) と Windows Server のデスクトップやアプリをあらゆるコンピューターで利用
- デスクトップとアプリの両方を仮想化
- 統合された管理エクスペリエンスで Windows 10、Windows Server、Windows 7 のデスクトップとアプリを管理 Windows Virtual Desktop でできることの詳細については、[紹介ビデオ](https://docs.microsoft.com/azure/virtual-desktop/overview)をご覧ください。

## <a name="use-windows-virtual-desktop-with-azure"></a>Azure で Windows Virtual Desktop を使用する 
Visual Studio のサブスクライバーは、いくつかの方法で Azure サブスクリプションを使用して Windows Virtual Desktop サービスの支払いを行えるようになりました。
- [Azure DevTest の個人クレジット](vs-azure.md)。  サブスクリプションの一部として Azure DevTest の個人クレジットを受け取るサブスクライバーは、そのクレジットで Windows Virtual Desktop サービスの支払いを行うことができます。  月単位のクレジットの金額は、サブスクリプション レベルによって異なります。
- [Azure DevTest の従量課金制のサブスクリプション](vs-azure-payg.md)。  Azure サブスクリプションを作成し、支払い方法をアタッチして、Windows Virtual Desktop の使用に合わせてシームレスに料金を支払うことができます。 
- [Azure Enterprise Agreement DevTest オファー](azure-ea-devtest.md)。  このオファーでは、Enterprise Agreement によるサブスクライバーは、Azure での Windows Virtual Desktop の料金を割引価格で支払うことができます。 

## <a name="requirements"></a>必要条件
Windows Virtual Desktop では、VM が参加する Azure Active Directory (Azure AD) が必要です。  ユーザーは、この Azure AD のメンバーである必要があります。  Azure AD を実装するには、次の 2 つのオプションがあります。
- Azure AD ディレクトリ サービス。  ほとんどのユーザーにとっては、こちらの実装方法が簡単です。
- ドメイン コントローラー キャンペーンを実行している仮想マシン。  このオプションでは、セットアップに多くの作業が必要ですが、ほとんどのユーザーの運用コストが低くなります。
Windows Virtual Desktop を使用するための前提条件の完全な一覧については、Windows Virtual Desktop の [概要ページ](https://docs.microsoft.com/azure/virtual-desktop/overview#requirements)を参照してください。 

## <a name="get-started"></a>作業開始 
すべての前提条件が満たされたら、いくつかのアクションを実行して、実装を適切な場所に配置します。  使用を開始するには、次のチュートリアルをご覧ください。
- [Windows Virtual Desktop テナントを作成する](https://docs.microsoft.com/azure/virtual-desktop/virtual-desktop-fall-2019/tenant-setup-azure-active-directory)
- Azure portal を使用して[ホスト プールを作成する](https://docs.microsoft.com/azure/virtual-desktop/create-host-pools-azure-marketplace)
- Windows Virtual Desktop の[アプリ グループを管理する](https://docs.microsoft.com/azure/virtual-desktop/manage-app-groups)

## <a name="eligibility"></a>特典を受ける条件
| サブスクリプション レベル                                                 |     チャネル                                            | 特長                                                          | 更新可能かどうか    |
|--------------------------------------------------------------------|---------------------------------------------------------|------------------------------------------------------------------|---------------|
| Visual Studio Enterprise (Standard)   | VL、Azure、リテール、 | 使用可能|  はい          |
| Visual Studio Enterprise with GitHub Enterprise  | VL | 使用可能|  はい          |
| Visual Studio Professional (Standard) | VL、Azure、リテール                                       | 使用可能                                                             |  はい             |
| Visual Studio Professional with GitHub Enterprise | VL                                       | 使用可能                                        |  はい           |
| Visual Studio Test Professional (標準)                         | VL、リテール                                              | 使用可能|  はい          |
| MSDN Platforms (標準)                                          | VL、リテール                                              | 使用可能                                         |  はい          |
| Visual Studio Enterprise (Standard)  | NFR<sup>1</sup> |使用できません  | N/A |
| Visual Studio Enterprise、Visual Studio Professional (月間クラウド) | Azure | 使用できません | N/A |

<sup>1</sup>  *以下が含まれます:Not for Resale (NFR)、FTE、Most Valuable Professional (MVP)、Regional Director (RD)、Microsoft Partner Network (MPN)、Visual Studio Industry Partner (VSIP)、Microsoft Certified Trainer、BizSpark、Imagine が含まれます。*

> [!NOTE]
> Microsoft では、クラウド サブスクリプションの Visual Studio Professional 年間サブスクリプションおよび Visual Studio Enterprise 年間サブスクリプションが提供されなくなりました。 サブスクリプションの更新、増減、キャンセルに関する既存のお客様のエクスペリエンスと機能については変更はありません。 新規のお客様は、[https://visualstudio.microsoft.com/vs/pricing/](https://visualstudio.microsoft.com/vs/pricing/) に移動し、Visual Studio のさまざまな購入オプションを調べることをお勧めします。

どのサブスクリプション使用しているかわからない場合は次の手順を実行してください。  [https://my.visualstudio.com/subscriptions](https://my.visualstudio.com/subscriptions?wt.mc_id=o~msft~docs) に接続し、お使いのメール アドレスに割り当てられているすべてのサブスクリプションを確認します。 すべてのサブスクリプションが表示されない場合は、1 つ以上のサブスクリプションが別のメール アドレスに割り当てられている可能性があります。  それらのサブスクリプションを表示するには、そのメール アドレスを使用してサインインする必要があります。

## <a name="see-also"></a>関連項目
- [Azure ドキュメント](https://docs.microsoft.com/azure/)
- [Windows Virtual Desktop のドキュメント](https://docs.microsoft.com/azure/virtual-desktop/)

## <a name="next-steps"></a>次の手順
-   Visual Studio サブスクリプションを購入する必要がある場合は、次のことを確認してください。
     - Microsoft Store での[小売価格](https://visualstudio.microsoft.com/vs/pricing/)
     - [ボリューム ライセンスのプログラム](https://www.microsoft.com/licensing/default)
-   [Windows Virtual Desktop](https://docs.microsoft.com/azure/virtual-desktop/overview) について 
