---
title: 再署名せずに ClickOnce アプリを展開する
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
ms.sourcegitcommit: d6828e7422c8d74ec1e99146fedf0a05f757245f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2020
ms.locfileid: "80395317"
---
# <a name="deploy-clickonce-applications-for-testing-and-production-servers-without-resigning"></a>辞任せずに、テストサーバーと運用サーバー用に ClickOnce アプリケーションを配置する
この資料では、再署名または ClickOnce マニフェストを変更せずに、複数のネットワークの場所から ClickOnce アプリケーションを配置できるようにする ClickOnce のバージョン 3.5 で導入された機能について説明します。

> [!NOTE]
> 新しいバージョンのアプリケーションを展開する場合は、辞職が望ましい方法です。 可能な場合は、再署名の方法を使用します。 詳細については、「 [ *Mage.exe* (マニフェスト生成および編集ツール)」](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)を参照してください。

 サードパーティの開発者や ISV は、この機能を使用できるため、顧客がアプリケーションを簡単に更新できるようになります。 この機能は、次の状況で使用できます。

- アプリケーションを更新する場合は、アプリケーションの初回インストール用ではありません。

- コンピュータ上にアプリケーションの構成が 1 つだけある場合。 たとえば、アプリケーションが 2 つの異なるデータベースを指す構成の場合、この機能は使用できません。

## <a name="exclude-deploymentprovider-from-deployment-manifests"></a>配置マニフェストから配置プロバイダーを除外する
 NET Framework 2.0 および .NET Framework 3.0 では、オフラインで使用できるようにシステムにインストールする ClickOnce アプリケーション`deploymentProvider`は、配置マニフェストに a を一覧表示する必要があります。 `deploymentProvider`は、更新場所と呼ばれることがよくあります。これは、ClickOnce がアプリケーションの更新をチェックする場所です。 この要件は、アプリケーションの発行元が展開に署名する必要がある場合と共に、企業がベンダーまたは他のサード パーティから ClickOnce アプリケーションを更新することが困難でした。 また、同じネットワーク上の複数の場所から同じアプリケーションを展開することも困難になります。

 .NET Framework 3.5 で ClickOnce に加えられた変更を加えた場合、サード パーティが ClickOnce アプリケーションを別の組織に提供し、その後、アプリケーションを独自のネットワークに配置できます。

 この機能を利用するには、ClickOnce アプリケーションの開発者が配置マニフェストから`deploymentProvider`除外する必要があります。 この要件は、Mage.exe`-providerUrl`を使用して配置マニフェストを作成するときに、引数を除外する必要があることを意味します。 または、MageUI.exe を使用して配置マニフェストを生成する場合は、[**アプリケーション マニフェスト**] タブの **[起動場所**] テキスト ボックスが空白になっていることを確認する必要があります。

## <a name="deploymentprovider-and-application-updates"></a>展開プロバイダおよびアプリケーションの更新
 NET Framework 3.5 以降では、オンラインとオフラインの両方の`deploymentProvider`使用のために ClickOnce アプリケーションを配置するために配置マニフェストで を指定する必要がなくなりました。 この変更は、自分で展開をパッケージ化して署名する必要があるが、他の企業がネットワーク上でアプリケーションを展開できるようにするシナリオをサポートします。

 注意が必要な重要な点は、 を`deploymentProvider`除外するアプリケーションは、タグを含む更新プログラムを再出荷するまで、`deploymentProvider`更新中にインストール場所を変更できないことです。

 この点を明確にする例を2つ紹介します。 最初の例では、タグのない`deploymentProvider`ClickOnce アプリケーションを発行し、ユーザーにから`http://www.adatum.com/MyApplication/`インストールするように求めます。 から`http://subdomain.adatum.com/MyApplication/`アプリケーションの次の更新を発行する場合は、 に存在する配置マニフェストでこれを示す方法はありません`http://www.adatum.com/MyApplication/`。 次の 2 つのうちいずれかを実行できます。

- 以前のバージョンをアンインストールし、新しいバージョンを新しい場所からインストールするようにユーザーに指示します。

- へのポイント`http://www.adatum.com/MyApplication/`を含む更新プログラム`deploymentProvider`を`http://www.adatum.com/MyApplication/`含めます。 次に、後でを指`deploymentProvider`す別`http://subdomain.adatum.com/MyApplication/`の更新プログラムをリリースします。

  2 番目の例では、 を指定`deploymentProvider`する ClickOnce アプリケーションを発行し、それを削除します。 新しいバージョンを`deploymentProvider`クライアントにダウンロードすると、`deploymentProvider`復元されたアプリケーションのバージョンをリリースするまで、更新に使用するパスをリダイレクトすることはできません。 最初の例と同様に`deploymentProvider`、最初は新しい場所ではなく、現在の更新場所をポイントする必要があります。 この場合、 を参照`deploymentProvider``http://subdomain.adatum.com/MyApplication/`する を挿入しようとすると、次の更新は失敗します。

## <a name="create-a-deployment"></a>デプロイの作成
 異なるネットワークの場所から配置できる配置を作成する手順については、「[チュートリアル: 再署名を必要とせず、ブランド情報を保持する ClickOnce アプリケーションを手動で展開する](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [*Mage.exe* (マニフェスト生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)
- [*MageUI.exe* (マニフェスト生成および編集ツール、グラフィカルクライアント)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)
