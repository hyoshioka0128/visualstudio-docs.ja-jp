---
title: '[方法] 配置の更新の代替場所を指定する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: e0484e36bb857f5d08382f86f42b2e09dda21616
ms.sourcegitcommit: c1339f64fbeee6f17bf80fedea81afc8dac40dc0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "82037338"
---
# <a name="how-to-specify-an-alternate-location-for-deployment-updates"></a>方法: 配置の更新用に別の場所を指定する
アプリケーションは[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]CD またはファイル共有から最初にインストールできますが、アプリケーションは Web 上で定期的に更新を確認する必要があります。 配置マニフェストで更新の別の場所を指定すると、アプリケーションは、最初のインストール後に Web から自身を更新できます。

> [!NOTE]
> この機能を使用するには、ローカルにインストールするようにアプリケーションを構成する必要があります。 詳細については、「[チュートリアル : ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」を参照してください。 また、ネットワークからアプリケーションを[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]インストールする場合、別の場所を設定すると[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]、初期インストールとそれ以降のすべての更新の両方でその場所が使用されます。 アプリケーションをローカルにインストールする場合 (たとえば、CD から) は、最初のインストールは元のメディアを使用して実行され、以降のすべての更新では別の場所が使用されます。

### <a name="specify-an-alternate-location-for-updates-by-using-mageuiexe-windows-forms-based-utility"></a>MageUI.exe (Windows フォーム ベースのユーティリティ) を使用して、更新プログラムの別の場所を指定します。

1. .NET Framework コマンド プロンプトを開き、次のように入力します。

     **mageui.exe**

2. [**ファイル**] メニューの [**開く**] を選択して、アプリケーションの配置マニフェストを開きます。

3. **[配置オプション]** タブを選択します。

4. [**起動場所**] というテキスト ボックスに、アプリケーション更新の配置マニフェストを含むディレクトリの URL を入力します。

5. 配置マニフェストを保存します。

### <a name="specify-an-alternate-location-for-updates-by-using-mageexe"></a>Mage.exe を使用して更新プログラムの別の場所を指定する

1. .NET Framework コマンド プロンプトを開きます。

2. 次のコマンドを使用して、更新場所を設定します。 この例では、アプリケーション マニフェストへの[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]パスである*HelloWorld.exe.application*は、常に .application 拡張子`http://adatum.com/Update/Path`を持ち、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]アプリケーションの更新をチェックする URL です。

    **モージュ -更新ハローワールド.exe.アプリケーション - プロバイダ\/Url http: /adatum.com/Update/Path**

3. ファイルを保存します。

   > [!NOTE]
   > 次に *、Mage.exe*を使用してファイルに再署名する必要があります。 詳細については、「[チュートリアル : ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」を参照してください。

## <a name="net-framework-security"></a>.NET Framework のセキュリティ
 CD などのオフライン メディアからアプリケーションをインストールし、コンピュータがオンラインである場合は、まず[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]配置マニフェストの`<deploymentProvider>`タグで指定された URL をチェックして、更新場所にアプリケーションの最新バージョンが含まれているかどうかを確認します。 インストールされている場合は[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]、最初のインストール ディレクトリからではなくそこから直接アプリケーションをインストールし、共通言語ランタイム (CLR) は を使用して`<deploymentProvider>`アプリケーションの信頼レベルを決定します。 コンピュータがオフラインであるか、または`<deploymentProvider>`到達不能な場合は、CD[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]からインストールを行い、CLR はインストール ポイントに基づいて信頼を付与します。CD インストールの場合、アプリケーションは完全な信頼を受けます。 それ以降のすべての更新は、その信頼レベルを継承します。

 使用[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]`<deploymentProvider>`するすべてのアプリケーションは、アプリケーション マニフェストで必要なアクセス許可を明示的に宣言して、アプリケーションが異なるコンピューターで異なるレベルの信頼を受け取らないようにする必要があります。

## <a name="see-also"></a>関連項目
- [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
- [クリックOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)
- [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
- [ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)