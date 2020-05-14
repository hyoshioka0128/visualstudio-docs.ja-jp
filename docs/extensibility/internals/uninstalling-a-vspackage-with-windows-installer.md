---
title: Windows インストーラを使用して VS パッケージをアンインストールする |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- packages, uninstalling
- VSPackages, uninstalling
- uninstalling VSPackages
ms.assetid: c4575ac7-82da-4af8-a375-ea756a101fbf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fee88e895d40d42114eaf53422503524594b485f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704274"
---
# <a name="uninstalling-a-vspackage-with-windows-installer"></a>Windows インストーラーによる VSPackage のアンインストール
ほとんどの場合、Windows インストーラーは VSPackage をインストールするために行ったことを "元にする" だけで VSPackage をアンインストールできます。 [インストール後に実行する必要があるコマンド](../../extensibility/internals/commands-that-must-be-run-after-installation.md)で説明されているカスタムアクションは、アンインストール後も実行する必要があります。 devenv.exe への呼び出しは、インストールとアンインストールの両方の InstallFinalize 標準アクションの直前に発生するため、CustomAction テーブルエントリと InstallExecuteSequence テーブル エントリは両方のケースに対応します。

> [!NOTE]
> MSI パッケージをアンインストールした後に実行`devenv /setup`します。

 一般的な規則として、Windows インストーラ パッケージにカスタム動作を追加する場合は、アンインストールとロールバック中にこれらの操作を処理する必要があります。 たとえば、カスタム アクションを追加して VSPackage を自己登録する場合は、カスタム アクションを追加して登録を解除する必要があります。

> [!NOTE]
> ユーザーが VSPackage をインストールし、統合されているバージョンを[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]アンインストールすることが可能です。 に依存するコードを実行するカスタム アクションを削除することで、VSPackage のアンインストールがそのシナリオで動作することを確認できます[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

## <a name="handling-launch-conditions-at-uninstall-time"></a>アンインストール時の起動条件の処理
 標準アクションは、条件が満たされていない場合にエラー メッセージを表示するために、LaunchCondition テーブルの行を読み取ります。 起動条件は一般的にシステム要件を満たすようにするために使用されるため、一般に、LaunchCondition テーブルの LaunchConditions`NOT Installed`行に条件を追加することで、アンインストール中に起動条件をスキップできます。

 別の方法として、`OR Installed`アンインストール時に重要ではない起動条件を追加します。 これにより、アンインストール時に条件が常に真となるため、起動条件のエラー メッセージは表示されません。

> [!NOTE]
> `Installed`は、VSPackage が既にシステムにインストールされていることを検出したときに、Windows インストーラーが設定するプロパティです。

## <a name="see-also"></a>関連項目
- [インストーラ](https://msdn.microsoft.com/library/187d8965-c79d-4ecb-8689-10930fa8b3b5)
- [システム要件の検出](../../extensibility/internals/detecting-system-requirements.md)
