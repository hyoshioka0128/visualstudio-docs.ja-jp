---
title: Visual Studio サブスクリプションでの運用前環境のインベントリ | Visual Studio Marketplace
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 7d74e113-8fb2-490e-8502-48cce7b1327a
ms.date: 01/14/2021
ms.topic: conceptual
description: 運用前環境のインベントリを実施する管理者の責任について説明します
ms.openlocfilehash: da8146b9f7d2b758ac2d249534d43bd98beae385
ms.sourcegitcommit: d124123528776993eb5e7461dae8da3975d11d0d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/03/2021
ms.locfileid: "99511307"
---
# <a name="inventory-of-pre-production-environment"></a>運用前環境のインベントリ
Visual Studio サブスクリプションは、デバイスではなくユーザーをカウントすることで、資産管理を簡略化します。

Visual Studio の管理者は、Visual Studio サブスクリプションを **特定の指定した個人** に割り当てる必要があります。 Dev1 や Dev2 などの名前付け規則、または "FeatureTeam" のようなチーム名の使用は、**許可されていません**。

実稼働前環境のインベントリを簡略化するいくつかの方法を次に示します。
- ユーザーの割り当てを確認します。 Microsoft が提供する [Visual Studio 管理ポータル](https://manage.visualstudio.com/)と呼ばれる Web サイトで、Visual Studio サブスクリプションの割り当てを追跡できます。
- オンプレミスまたはクラウド ベースの Active Directory を使用してユーザーを一覧表示します。 Active Directory を使用してユーザー アクセスを管理する場合は、開発ユーザーとテスト ユーザーをそのディレクトリ メンバーシップで識別することができます。
- インベントリ システムに自動化ツールを使用します。 また、ソフトウェア資産を管理し、実稼働前環境と運用環境を区別するには、ソフトウェア インベントリ ツールを使用する必要があります。 Microsoft System Center を使用する多くのお客様が、インベントリ プロセスのこの部分を自動化するために名前付け規則を作成しています。
- 手動による調整に関するヘルプを入手します。 開発およびテスト環境で、開発ユーザーおよびテスト ユーザーの調整を支援するため、スタッフを登録します。

> [!NOTE]
> Visual Studio サブスクリプションのソフトウェアは、運用環境にはライセンス付与されません。運用環境には、受け入れテストやフィードバック以外にエンド ユーザーによってアクセスされる環境、実稼働データベースに接続している環境、ディザスター リカバリーまたは実稼働バックアップをサポートしている環境、またはアクティビティのピーク時に運用に使用される環境が含まれます。 この例外には、[Visual Studio ライセンスのホワイト ペーパー](https://aka.ms/vslicensing)に記載されている特定のサブスクリプション レベルの特定の特典が含まれます。  

## <a name="resources"></a>リソース
- [Visual Studio ライセンスのホワイト ペーパー](https://visualstudio.microsoft.com/wp-content/uploads/2019/06/Visual-Studio-Licensing-Whitepaper-May-2019.pdf)
- [Visual Studio サブスクリプションのサポート](https://my.visualstudio.com/gethelp)
- [ボリューム ライセンスの契約条件](https://www.microsoft.com/licensing/product-licensing/products.aspx)

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](/visualstudio/)
- [Azure DevOps ドキュメント](/azure/devops/)
- [Azure ドキュメント](/azure/)
- [Microsoft 365 ドキュメント](/microsoft-365/)

## <a name="next-steps"></a>次のステップ
管理者の責任について詳しくは、以下をご覧ください。
- [管理者の責任](admin-responsibilities.md)
- [大規模なチームと外部請負業者を管理する](manage-teams.md)
- [ユーザーの割り当てを追跡し、注文を処理する](assignments-orders.md)
- [最大使用量](maximum-usage.md)を使用して購入コミットメントを追跡する