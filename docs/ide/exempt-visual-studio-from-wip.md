---
title: Windows Information Protection からの除外
ms.date: 06/01/2018
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8b4eb454f641b5bef7273464d605fb194f650790
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75588565"
---
# <a name="configure-visual-studio-as-a-wip-exempt-app"></a>Visual Studio を WIP 除外アプリとして構成する

[Windows Information Protection](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP) は、企業が管理していない電子メールなどのアプリ、ソーシャル メディア、パブリック クラウドなどから、企業のデータが漏えいすることを防ぐために役立ちます。 WIP を使用すると、企業が所有するデバイスと個人用デバイスでも、偶発的なデータ漏えいから保護できます。既存の環境や他のアプリを変更する必要はありません。

WIP に*対応する*アプリは、保護されていないネットワークの場所に企業データが送信されないように防ぎ、個人データの暗号化が回避されることが期待されています。 Visual Studio は対応するアプリではないため、除外しない限り、WIP 対応環境では動作しません。 WIP 対応のマシンで Visual Studio を機能させるには、この記事の手順に従ってください。

## <a name="configure-vs-as-a-wip-exempt-app"></a>WIP 除外アプリとして VS を構成する

Visual Studio を WIP の制限から除外し、さらに企業データを使用できるようにすることができます。 WIP 除外アプリは、IP アドレスまたはホスト名を使用してエンタープライズ クラウド リソースに接続できます。 暗号化は適用されず、アプリはローカル ファイルにアクセスできます。

WIP から Visual Studio を除外するには、[デスクトップ アプリを除外する手順](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-intune-azure#exempt-apps-from-a-wip-policy)に従ってください。

## <a name="create-a-wip-exempt-applocker-policy-file"></a>WIP 除外 AppLocker ポリシー ファイルを作成する

Visual Studio には複数のバイナリが含まれているので、[WIP 除外 AppLocker ポリシー ファイルを作成します](/windows/security/threat-protection/windows-defender-application-control/applocker/run-the-automatically-generate-rules-wizard)。 AppLocker を使用すると、フォルダー内のすべてのファイルのルールを自動的に生成できます。

## <a name="add-appcompat-to-the-enterprise-cloud-resource-policy"></a>AppCompat をエンタープライズ クラウド リソース ポリシーに追加する

Visual Studio がネットワーク上の企業データにアクセスできる場所を指定するには、[保護されたアプリが企業データを検索および送信できる場所を定義する手順](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-intune-azure#choose-where-apps-can-access-enterprise-data)に従ってください。 Windows が IP アドレスを使用してクラウド リソースへの接続をブロックしないようにするには、/\*AppCompat\*/ 文字列を設定に追加してください。

## <a name="see-also"></a>関連項目

- [WIP を使っているときのアプリの動作](/windows/security/information-protection/windows-information-protection/app-behavior-with-wip)
