---
title: 再署名せずに ClickOnce アプリをデプロイする
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce applications, deploying without resigning
- ClickOnce deployment, without resigning
- application updates, ClickOnce
- update location [ClickOnce]
- deploymentProvider tag
- manifests [ClickOnce]
ms.assetid: 1218a98d-1ad5-4eef-95dd-0e0b3c44168c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 89e1d7970b26d5ba9bd49090362a6a4e8c09f78d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80395317"
---
# <a name="deploy-clickonce-applications-for-testing-and-production-servers-without-resigning"></a>テストサーバーおよび運用サーバー用の ClickOnce アプリケーションを、署名せずに配置する
この記事では、.NET Framework バージョン3.5 で導入された ClickOnce の機能について説明します。 clickonce マニフェストを再署名または変更することなく、複数のネットワークの場所から ClickOnce アプリケーションを配置できます。

> [!NOTE]
> 新しいバージョンのアプリケーションを展開する場合も、再度署名することをお勧めします。 可能な限り、署名の方法を使用してください。 詳細については、「 [ *Mage.exe* (マニフェスト生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)」を参照してください。

 サードパーティの開発者や Isv はこの機能を選択して、お客様がアプリケーションを簡単に更新できるようにします。 この機能は、次の状況で使用できます。

- アプリケーションの最初のインストールではなく、アプリケーションを更新する場合。

- コンピューターにアプリケーションの構成が1つしかない場合。 たとえば、アプリケーションが2つの異なるデータベースを指すように構成されている場合、この機能を使用することはできません。

## <a name="exclude-deploymentprovider-from-deployment-manifests"></a>配置マニフェストから deploymentProvider を除外する
 .NET Framework 2.0 および .NET Framework 3.0 では、オフラインで使用できるようにシステムにインストールされている ClickOnce アプリケーションは、配置マニフェストにを一覧表示する必要があり `deploymentProvider` ます。 は、 `deploymentProvider` 通常、更新プログラムの場所と呼ばれます。 ClickOnce がアプリケーションの更新プログラムをチェックする場所です。 この要件は、アプリケーション発行者が配置に署名する必要があると共に、企業がベンダーや他のサードパーティから ClickOnce アプリケーションを更新することが困難になっています。 また、同じネットワーク上の複数の場所から同じアプリケーションを展開することが難しくなります。

 .NET Framework 3.5 で ClickOnce に加えられた変更により、サードパーティが ClickOnce アプリケーションを別の組織に提供し、それによってアプリケーションを独自のネットワークにデプロイできるようになります。

 この機能を利用するために、ClickOnce アプリケーションの開発者は、配置マニフェストからを除外する必要があり `deploymentProvider` ます。 この要件は、 `-providerUrl` Mage.exe で配置マニフェストを作成するときに引数を除外する必要があることを意味します。 または、MageUI.exe で配置マニフェストを生成している場合は、[**アプリケーションマニフェスト**] タブの [**起動場所**] テキストボックスが空白のままになっていることを確認する必要があります。

## <a name="deploymentprovider-and-application-updates"></a>deploymentProvider とアプリケーションの更新プログラム
 .NET Framework 3.5 以降では、 `deploymentProvider` オンラインとオフラインの両方の使用のために ClickOnce アプリケーションを配置するために、配置マニフェストでを指定する必要がなくなりました。 この変更により、展開を自分でパッケージ化して署名する必要がありますが、他の企業がネットワーク経由でアプリケーションを展開できるようになります。

 注意すべき重要な点は、を除外するアプリケーションは、 `deploymentProvider` タグを含む更新プログラムを再配布するまで、更新中にインストール場所を変更できないことです `deploymentProvider` 。

 この点を明確にする2つの例を次に示します。 最初の例では、タグのない ClickOnce アプリケーションを発行 `deploymentProvider` し、からインストールするようにユーザーに依頼し `http://www.adatum.com/MyApplication/` ます。 からアプリケーションの次の更新プログラムを発行する場合は `http://subdomain.adatum.com/MyApplication/` 、に存在する配置マニフェストでこれを示すことはできません `http://www.adatum.com/MyApplication/` 。 次の2つの操作のいずれかを実行できます。

- 以前のバージョンをアンインストールするようにユーザーに通知し、新しい場所から新しいバージョンをインストールします。

- をポイントするを含む更新プログラムをに含め `http://www.adatum.com/MyApplication/` `deploymentProvider` `http://www.adatum.com/MyApplication/` ます。 次に、をポイントして、後で別の更新プログラムをリリースし `deploymentProvider` `http://subdomain.adatum.com/MyApplication/` ます。

  2番目の例では、を指定する ClickOnce アプリケーションを発行し、 `deploymentProvider` それを削除するかどうかを決定します。 を使用せずに新しいバージョン `deploymentProvider` がクライアントにダウンロードされると、復元されたアプリケーションのバージョンがリリースされるまで、更新に使用されるパスをリダイレクトすることはできません `deploymentProvider` 。 最初の例と同様に、は `deploymentProvider` 最初に新しい場所ではなく、現在の更新プログラムの場所を指す必要があります。 この場合、を参照するを挿入しようとすると、 `deploymentProvider` `http://subdomain.adatum.com/MyApplication/` 次の更新は失敗します。

## <a name="create-a-deployment"></a>デプロイの作成
 さまざまなネットワークの場所からデプロイできるデプロイを作成するための詳細な手順については、「 [チュートリアル: 再署名が不要で、ブランド情報を保持する ClickOnce アプリケーションを手動で配置](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)する」を参照してください。

## <a name="see-also"></a>関連項目
- [*Mage.exe* (マニフェスト生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)
- [*MageUI.exe* (マニフェスト生成および編集ツール、グラフィカルクライアント)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)
