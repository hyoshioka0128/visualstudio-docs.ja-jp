---
title: 展開の更新の代替の場所を指定する
description: 配置マニフェストで ClickOnce アプリケーションの更新プログラムの別の場所を指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, updates
- deployment update, alternative locations
ms.assetid: 7faacd35-2638-492d-80f6-6b57e5f820de
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 698ca2c97bcc4699d2c836eff9fefa371481c9cc
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2020
ms.locfileid: "94349647"
---
# <a name="how-to-specify-an-alternate-location-for-deployment-updates"></a>方法: 配置の更新用に別の場所を指定する
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]最初に CD またはファイル共有からアプリケーションをインストールできますが、アプリケーションでは Web 上の定期的な更新プログラムを確認する必要があります。 配置マニフェストで更新プログラムの別の場所を指定して、アプリケーションが最初のインストール後に Web から自身を更新できるようにすることができます。

> [!NOTE]
> この機能を使用するには、アプリケーションをローカルにインストールするように構成する必要があります。 詳細については、「 [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」を参照してください。 さらに、ネットワークからアプリケーションをインストールする場合 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 、別の場所を設定すると、では、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 初期インストールとそれ以降のすべての更新で、その場所が使用されます。 アプリケーションをローカルに (たとえば CD から) インストールする場合、最初のインストールは元のメディアを使用して実行され、それ以降のすべての更新では代替の場所が使用されます。

### <a name="specify-an-alternate-location-for-updates-by-using-mageuiexe-windows-forms-based-utility"></a>MageUI.exe (Windows フォームベースのユーティリティ) を使用して、更新プログラムの別の場所を指定する

1. .NET Framework コマンドプロンプトを開き、次のように入力します。

     **mageui.exe**

2. [ **ファイル** ] メニューの [ **開く** ] をクリックして、アプリケーションの配置マニフェストを開きます。

3. **[配置オプション]** タブを選択します。

4. [ **Launch Location** ] という名前のテキストボックスに、アプリケーションの更新の配置マニフェストが格納されるディレクトリの URL を入力します。

5. 配置マニフェストを保存します。

### <a name="specify-an-alternate-location-for-updates-by-using-mageexe"></a>Mage.exe を使用して、更新プログラムの別の場所を指定します

1. .NET Framework コマンドプロンプトを開きます。

2. 次のコマンドを使用して、更新プログラムの場所を設定します。 この例では、 *HelloWorld.exe* アプリケーションマニフェストへのパスを指定します。このパスは [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 常にアプリケーションの拡張子を持ち、 `http://adatum.com/Update/Path` は [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの更新プログラムをチェックする URL です。

    **Mage.exe-ProviderUrl http:/adatum.com/Update/Path を HelloWorld.exe 更新します。 \/**

3. ファイルを保存します。

   > [!NOTE]
   > 次に、 *Mage.exe* を使用してファイルに再署名する必要があります。 詳細については、「 [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」を参照してください。

## <a name="net-framework-security"></a>.NET Framework セキュリティ
 CD などのオフラインメディアからアプリケーションをインストールし、コンピューターがオンラインの場合、はまず、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置マニフェストのタグで指定された URL を確認して、 `<deploymentProvider>` 更新プログラムの場所により新しいバージョンのアプリケーションが含まれているかどうかを確認します。 存在する場合は、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 最初のインストールディレクトリからではなく、そこからアプリケーションを直接インストールします。また、を使用して、共通言語ランタイム (CLR) によってアプリケーションの信頼レベルが決定され `<deploymentProvider>` ます。 コンピューターがオフラインである場合、また `<deploymentProvider>` はアクセスできない場合は、が cd からインストールされます。また、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] この CLR は、インストールポイントに基づいて信頼を付与します。 CD のインストールの場合は、アプリケーションが完全な信頼を受け取ることを意味します。 それ以降のすべての更新は、その信頼レベルを継承します。

 を使用するすべてのアプリケーションは、アプリケーション [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `<deploymentProvider>` マニフェストで必要なアクセス許可を明示的に宣言する必要があります。これにより、アプリケーションが異なるコンピューター上で異なる信頼レベルを受け取ることはありません。

## <a name="see-also"></a>関連項目
- [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)
- [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
- [ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)