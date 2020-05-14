---
title: 再署名せずにテストサーバーおよび実稼働サーバー用に ClickOnce アプリケーションを配置する |マイクロソフトドキュメント
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
ms.sourcegitcommit: d6828e7422c8d74ec1e99146fedf0a05f757245f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2020
ms.locfileid: "80395369"
---
# <a name="deploying-clickonce-applications-for-testing-and-production-servers-without-resigning"></a>再署名を行わない ClickOnce アプリケーションの配置 (テスト サーバーおよび運用サーバー)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、.NET Framework バージョン 3.5 で導入された ClickOnce の新機能について説明します。  
  
> [!NOTE]
> 新しいバージョンのアプリケーションを展開する場合は、辞職が望ましい方法です。 可能な場合は、再署名の方法を使用します。 詳細については、「 [Mage.exe (マニフェスト生成および編集ツール)」](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)を参照してください。  
  
 サードパーティの開発者や ISV は、この機能を使用して、顧客がアプリケーションを更新しやすくすることができます。 この機能は、次の状況で使用できます。  
  
- アプリケーションを更新する場合は、アプリケーションの最初のインストールではありません。  
  
- コンピュータ上にアプリケーションの構成が 1 つだけある場合。 たとえば、アプリケーションが 2 つの異なるデータベースを指す構成の場合、この機能は使用できません。  
  
## <a name="excluding-deploymentprovider-from-deployment-manifests"></a>配置マニフェストから展開プロバイダーを除外する  
 NET Framework 2.0 および .NET Framework 3.0 では、オフラインで使用できるようにシステムにインストールする ClickOnce アプリケーション`deploymentProvider`は、配置マニフェストで を指定する必要があります。 `deploymentProvider`は、更新場所と呼ばれることがよくあります。これは、ClickOnce がアプリケーションの更新をチェックする場所です。 この要件は、アプリケーション発行元が展開に署名する必要がある場合と相まって、企業がベンダーまたは他のサードパーティから ClickOnce アプリケーションを更新することが困難になりました。 また、同じネットワーク上の複数の場所から同じアプリケーションを展開することも困難になります。  
  
 .NET Framework 3.5 で ClickOnce に加えられた変更を加えた場合、サードパーティが ClickOnce アプリケーションを別の組織に提供し、その後、アプリケーションを独自のネットワークに配置できます。  
  
 この機能を利用するには、ClickOnce アプリケーションの開発者が配置マニフェストから`deploymentProvider`除外する必要があります。 つまり、Mage.exe を使用して配置マニフェストを作成するときに`-providerUrl`引数を除外するか、MageUI.exe を使用して配置マニフェストを生成する場合は、[アプリケーション**マニフェスト**] タブの **[起動場所**] テキスト ボックスが空白のままであることを確認します。  
  
## <a name="deploymentprovider-and-application-updates"></a>展開プロバイダとアプリケーションの更新  
 NET Framework 3.5 以降では、オンラインとオフラインの両方の`deploymentProvider`使用のために ClickOnce アプリケーションを配置するために配置マニフェストで を指定する必要がなくなりました。 これは、自分で展開をパッケージ化して署名する必要があるが、他の企業がネットワーク上でアプリケーションを展開できるようにするシナリオをサポートします。  
  
 注意が必要な重要な点は、 を`deploymentProvider`除外するアプリケーションは、タグを含む更新プログラムを再出荷するまで、`deploymentProvider`更新中にインストール場所を変更できないことです。  
  
 この点を明確にする例を2つ紹介します。 最初の例では、タグのない`deploymentProvider`ClickOnce アプリケーションを発行し、ユーザーにから`http://www.adatum.com/MyApplication/`インストールするように求めます。 から`http://subdomain.adatum.com/MyApplication/`アプリケーションの次の更新を発行する場合は、 に存在する配置マニフェストでこれを示す方法はありません`http://www.adatum.com/MyApplication/`。 次の 2 つのうちいずれかを実行できます。  
  
- 以前のバージョンをアンインストールし、新しいバージョンを新しい場所からインストールするようにユーザーに指示します。  
  
- へのポイント`http://www.adatum.com/MyApplication/`を含む更新プログラム`deploymentProvider`を`http://www.adatum.com/MyApplication/`含めます。 次に、後でを指`deploymentProvider`す別`http://subdomain.adatum.com/MyApplication/`の更新プログラムをリリースします。  
  
  2 番目の例では、 を指定`deploymentProvider`する ClickOnce アプリケーションを発行し、それを削除します。 クライアントにダウンロードされていない新`deploymentProvider`しいバージョンは、`deploymentProvider`復元されたアプリケーションのバージョンをリリースするまで、更新に使用するパスをリダイレクトできません。 最初の例と同様に`deploymentProvider`、最初は新しい場所ではなく、現在の更新場所をポイントする必要があります。 この場合、`deploymentProvider``http://subdomain.adatum.com/MyApplication/`を参照する を挿入しようとすると、次の更新は失敗します。  
  
## <a name="creating-a-deployment"></a>配置の作成  
 異なるネットワークの場所から配置できる配置を作成する手順の詳細については、「[チュートリアル: 再署名を必要としない ClickOnce アプリケーションを手動で展開する」および「ブランド情報を保持する](/visualstudio/deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required?view=vs-2015)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [Mage.exe (マニフェスト生成および編集ツール)](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)   
 [MageUI.exe (マニフェスト生成および編集ツール、グラフィカルクライアント)](https://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14)
