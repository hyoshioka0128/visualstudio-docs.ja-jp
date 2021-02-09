---
title: Windows インストーラー | を使用した VSPackage のアンインストールMicrosoft Docs
description: VSPackage をアンインストールするには、インストールを逆にします。 Windows インストーラー Windows インストーラーパッケージでカスタムアクションを処理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- packages, uninstalling
- VSPackages, uninstalling
- uninstalling VSPackages
ms.assetid: c4575ac7-82da-4af8-a375-ea756a101fbf
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 89a3ed681f51b392e076cff0fcb06b2f868c0aa5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99888993"
---
# <a name="uninstalling-a-vspackage-with-windows-installer"></a>Windows インストーラーによる VSPackage のアンインストール
ほとんどの場合 Windows インストーラー、VSPackage をアンインストールするには、VSPackage をインストールしたことを "元に戻す" だけで済みます。 「 [インストール後に実行する必要](../../extensibility/internals/commands-that-must-be-run-after-installation.md) のあるコマンド」で説明されているカスタムアクションもアンインストール後に実行する必要があります。 devenv.exe の呼び出しは、インストールとアンインストールの両方について InstallFinalize 標準アクションの直前に発生するため、CustomAction と InstallExecuteSequence テーブルエントリは両方のケースに対応します。

> [!NOTE]
> `devenv /setup`MSI パッケージをアンインストールした後で、を実行します。

 一般的なルールとして、Windows インストーラーパッケージにカスタムアクションを追加する場合は、アンインストール時およびロールバック時にそれらのアクションを処理する必要があります。 たとえば、VSPackage を自己登録するカスタムアクションを追加する場合は、カスタムアクションを追加して、登録を解除する必要があります。

> [!NOTE]
> ユーザーは、VSPackage をインストールしてから、統合されているのバージョンをアンインストールすることができ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 の依存関係があるコードを実行するカスタムアクションを排除することで、そのシナリオで VSPackage のアンインストールが確実に機能するようにすることができ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

## <a name="handling-launch-conditions-at-uninstall-time"></a>アンインストール時に起動条件を処理する
 Launchconditions 標準アクションは、条件が満たされていない場合にエラーメッセージを表示するために、Launchconditions テーブルの行を読み取ります。 システム要件が満たされていることを確認するために一般的に使用される起動条件では、通常、 `NOT Installed` launchconditions テーブルの launchconditions 行に条件を追加することによって、アンインストール中に起動条件をスキップできます。

 別の方法とし `OR Installed` て、アンインストール中に重要でない起動条件を追加することもできます。 これにより、アンインストール中に条件が常に true になるため、起動条件エラーメッセージは表示されません。

> [!NOTE]
> `Installed` は、VSPackage が既にシステムにインストールされていることを検出したときに設定 Windows インストーラープロパティです。

## <a name="see-also"></a>関連項目
- [Windows インストーラー](/previous-versions/ee231230(v=vs.100))
- [システム要件の検出](../../extensibility/internals/detecting-system-requirements.md)