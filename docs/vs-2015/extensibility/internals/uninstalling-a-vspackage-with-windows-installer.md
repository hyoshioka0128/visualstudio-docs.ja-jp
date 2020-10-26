---
title: Windows インストーラー | を使用した VSPackage のアンインストールMicrosoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- packages, uninstalling
- VSPackages, uninstalling
- uninstalling VSPackages
ms.assetid: c4575ac7-82da-4af8-a375-ea756a101fbf
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9a309779850dd33b77b426beb5627f61c40c2c4f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65675240"
---
# <a name="uninstalling-a-vspackage-with-windows-installer"></a>Windows インストーラーによる VSPackage のアンインストール
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ほとんどの場合 Windows インストーラー、VSPackage をアンインストールするには、VSPackage をインストールしたことを "元に戻す" だけで済みます。 「 [インストール後に実行する必要](../../extensibility/internals/commands-that-must-be-run-after-installation.md) のあるコマンド」で説明されているカスタムアクションもアンインストール後に実行する必要があります。 devenv.exe の呼び出しは、インストールとアンインストールの両方について InstallFinalize 標準アクションの直前に発生するため、CustomAction と InstallExecuteSequence テーブルエントリは両方のケースに対応します。  
  
> [!NOTE]
> `devenv /setup`MSI パッケージをアンインストールした後で、を実行します。  
  
 一般的なルールとして、Windows インストーラーパッケージにカスタムアクションを追加する場合は、アンインストール時およびロールバック時にそれらのアクションを処理する必要があります。 たとえば、VSPackage を自己登録するカスタムアクションを追加する場合は、カスタムアクションを追加して、登録を解除する必要があります。  
  
> [!NOTE]
> ユーザーは、VSPackage をインストールしてから、統合されているのバージョンをアンインストールすることができ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 の依存関係があるコードを実行するカスタムアクションを排除することで、そのシナリオで VSPackage のアンインストールが確実に機能するようにすることができ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
## <a name="handling-launch-conditions-at-uninstall-time"></a>アンインストール時に起動条件を処理する  
 Launchconditions 標準アクションは、条件が満たされていない場合にエラーメッセージを表示するために、Launchconditions テーブルの行を読み取ります。 システム要件が満たされていることを確認するために一般的に使用される起動条件では、通常、 `NOT Installed` launchconditions テーブルの launchconditions 行に条件を追加することによって、アンインストール中に起動条件をスキップできます。  
  
 別の方法とし `OR Installed` て、アンインストール中に重要でない起動条件を追加することもできます。 これにより、アンインストール中に条件が常に true になるため、起動条件エラーメッセージは表示されません。  
  
> [!NOTE]
> `Installed` は、VSPackage が既にシステムにインストールされていることを検出したときに設定 Windows インストーラープロパティです。  
  
## <a name="see-also"></a>参照  
 [Windows インストーラー](https://msdn.microsoft.com/187d8965-c79d-4ecb-8689-10930fa8b3b5)   
 [システム要件の検出](../../extensibility/internals/detecting-system-requirements.md)
