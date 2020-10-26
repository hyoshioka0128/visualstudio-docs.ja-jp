---
title: テストおよび運用サーバー用の ClickOnce アプリケーションを、再度署名せずに配置する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
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
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a8e41e67d5e2800acc41e1220fe632001420a274
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80395369"
---
# <a name="deploying-clickonce-applications-for-testing-and-production-servers-without-resigning"></a>再署名を行わない ClickOnce アプリケーションの配置 (テスト サーバーおよび運用サーバー)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、.NET Framework バージョン3.5 で導入された ClickOnce の新機能について説明します。この機能を使用すると、clickonce マニフェストを再署名したり変更したりすることなく、複数のネットワークの場所から ClickOnce アプリケーションを配置できます。  
  
> [!NOTE]
> 新しいバージョンのアプリケーションを展開する場合も、再度署名することをお勧めします。 可能な限り、署名の方法を使用してください。 詳しくは、「[Mage.exe (マニフェストの生成および編集ツール)](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)」をご覧ください。  
  
 サードパーティの開発者や Isv はこの機能をオプトインできるため、お客様がアプリケーションを簡単に更新できます。 この機能は、次の状況で使用できます。  
  
- アプリケーションの最初のインストールではなく、アプリケーションを更新する場合。  
  
- コンピューターにアプリケーションの構成が1つしかない場合。 たとえば、アプリケーションが2つの異なるデータベースを指すように構成されている場合、この機能を使用することはできません。  
  
## <a name="excluding-deploymentprovider-from-deployment-manifests"></a>配置マニフェストからの deploymentProvider の除外  
 .NET Framework 2.0 および .NET Framework 3.0 では、オフラインで使用できるようにシステムにインストールされる ClickOnce アプリケーションは、配置マニフェストでを指定する必要があり `deploymentProvider` ます。 は、 `deploymentProvider` 通常、更新プログラムの場所と呼ばれます。 ClickOnce がアプリケーションの更新プログラムをチェックする場所です。 この要件は、アプリケーション発行者が配置に署名する必要があるため、企業がベンダーや他のサードパーティから ClickOnce アプリケーションを更新することが困難になっています。 また、同じネットワーク上の複数の場所から同じアプリケーションを展開することが難しくなります。  
  
 .NET Framework 3.5 で ClickOnce に加えられた変更により、サードパーティが ClickOnce アプリケーションを別の組織に提供できるようになります。これにより、アプリケーションを独自のネットワークに配置できます。  
  
 この機能を利用するために、ClickOnce アプリケーションの開発者は、配置マニフェストからを除外する必要があり `deploymentProvider` ます。 これは、 `-providerUrl` Mage.exe で配置マニフェストを作成する場合は引数を除外すること、MageUI.exe で配置マニフェストを生成する場合は [**アプリケーションマニフェスト**] タブの [**起動場所**] テキストボックスが空白のままになることを意味します。  
  
## <a name="deploymentprovider-and-application-updates"></a>deploymentProvider とアプリケーションの更新プログラム  
 .NET Framework 3.5 以降では、 `deploymentProvider` オンラインとオフラインの両方の使用のために ClickOnce アプリケーションを配置するために、配置マニフェストでを指定する必要がなくなりました。 これにより、展開を自分でパッケージ化して署名する必要がありますが、他の企業がネットワーク経由でアプリケーションを展開することを許可するシナリオがサポートされます。  
  
 注意すべき重要な点は、を除外するアプリケーションは、 `deploymentProvider` タグを含む更新プログラムを再配布するまで、更新中にインストール場所を変更できないことです `deploymentProvider` 。  
  
 この点を明確にする2つの例を次に示します。 最初の例では、タグのない ClickOnce アプリケーションを発行 `deploymentProvider` し、からインストールするようにユーザーに依頼し `http://www.adatum.com/MyApplication/` ます。 からアプリケーションの次の更新プログラムを発行する場合 `http://subdomain.adatum.com/MyApplication/` 、に存在する配置マニフェストでこれを示す方法はありません `http://www.adatum.com/MyApplication/` 。 次の2つの操作のいずれかを実行できます。  
  
- 以前のバージョンをアンインストールするようにユーザーに通知し、新しい場所から新しいバージョンをインストールします。  
  
- をポイントするを含む更新プログラムをに含め `http://www.adatum.com/MyApplication/` `deploymentProvider` `http://www.adatum.com/MyApplication/` ます。 次に、をポイントして、後で別の更新プログラムをリリースし `deploymentProvider` `http://subdomain.adatum.com/MyApplication/` ます。  
  
  2番目の例では、を指定する ClickOnce アプリケーションを発行し、 `deploymentProvider` それを削除するかどうかを決定します。 を使用せずに新しいバージョンを `deploymentProvider` クライアントにダウンロードすると、復元されたアプリケーションのバージョンがリリースされるまで、更新に使用されるパスをリダイレクトすることはできません `deploymentProvider` 。 最初の例と同様に、は `deploymentProvider` 最初に新しい場所ではなく、現在の更新プログラムの場所を指す必要があります。 この場合、を参照するを挿入しようとすると、 `deploymentProvider` `http://subdomain.adatum.com/MyApplication/` 次の更新は失敗します。  
  
## <a name="creating-a-deployment"></a>デプロイの作成  
 さまざまなネットワークの場所からデプロイできるデプロイを作成するための詳細な手順については、「 [チュートリアル: 再署名が不要で、ブランド情報を保持する ClickOnce アプリケーションを手動で配置](/visualstudio/deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required?view=vs-2015)する」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Mage.exe (マニフェスト生成および編集ツール)](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)   
 [MageUI.exe (マニフェスト生成および編集ツールのグラフィカル クライアント)](https://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14)
