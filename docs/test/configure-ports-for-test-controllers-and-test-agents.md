---
title: テスト コントローラーおよびテスト エージェント用のポートの構成
description: 他のソフトウェアとの競合を防ぐために、テスト コントローラー、テスト エージェント、およびクライアントが使用する既定の着信ポートを変更する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- firewalls, configuring for test agents
- firewalls, configuring for test controllers
- test agents, firewalls
- test controllers, firewalls
- agents, firewalls
- controllers, firewalls
ms.assetid: 211edbd7-9fe4-4251-ba85-8bec4363261b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2726d489c0c67bffb11bc59357f6ad107a6c94ba
ms.sourcegitcommit: 02f14db142dce68d084dcb0a19ca41a16f5bccff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "95441569"
---
# <a name="configure-ports-for-test-controllers-and-test-agents"></a>テスト コントローラーおよびテスト エージェント用のポートの構成

テスト コントローラー、テスト エージェント、およびクライアントが使用する既定の着信ポートを変更できます。 テスト コントローラー、テスト エージェント、またはクライアントを他のソフトウェアと共に使用する際、ポート設定が競合していると、着信ポートの変更が必要になることがあります。 ポートを変更するもう 1 つの理由として、テスト コントローラーとクライアント間のファイアウォールの制限があります。 この場合、ファイアウォールを通過してテスト コントローラーがクライアントに結果を送信できるように、手動でポートを設定することができます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

次の図は、テスト コントローラー、テスト エージェント、およびクライアント間のコネクション ポイントを示しています。 ここでは、着信および発信接続に使用されるポートに加え、これらのポートで使用されるセキュリティ要件の詳細についても説明します。

![テスト コントローラーおよびテスト エージェントのポートとセキュリティ](../test/media/test-controller-agent-firewall.png)

## <a name="incoming-connections"></a>着信接続

テスト コントローラーが使用する既定のポートは 6901 で、テスト エージェントの既定のポートは 6910 です。 クライアントは既定ではランダムなポートを使用して、テスト コントローラーからのテスト結果を受信します。 すべての着信接続に対して、テスト コントローラーは呼び出しを行っているパーティを認証し、そのパーティが特定のセキュリティ グループに所属しているかを検証します。

- **テスト コントローラー** 着信接続は TCP ポート 6901 で行われます。 必要に応じて着信ポートを設定することができます。 詳細については、「[着信ポートの構成](#configure-the-incoming-ports)」をご覧ください。

    テスト コントローラーは、テスト エージェントとクライアントに対して発信接続できる必要があります。

    > [!NOTE]
    > テスト コントローラーでは、着信である **[ファイルとプリンターの共有]** 接続が開いていることが必要です。

- **テスト エージェント** 着信接続は TCP ポート 6910 で行われます。 必要に応じて着信ポートを設定することができます。 詳細については、「[着信ポートの構成](#configure-the-incoming-ports)」をご覧ください。

   テスト エージェントは、テスト コントローラーに対して発信接続できる必要があります。

- **クライアント** 既定では、着信接続に対してランダム TCP ポートが使用されます。 必要に応じて着信ポートを設定することができます。 詳細については、「[着信ポートの構成](#configure-the-incoming-ports)」をご覧ください。

   テスト コントローラーがクライアントに初めて接続しようとするとき、ファイアウォールの通知を受け取る場合があります。

   Windows Server 2008 のファイアウォールの通知は既定で無効になっています。着信接続を受け取ることができるように、クライアント プログラム (*devenv.exe*、*mstest.exe*、*mlm.exe*) に対するファイアウォールの例外を手動で追加する必要があります。

## <a name="outgoing-connections"></a>発信接続

すべての発信接続に対してランダム TCP ポートが使用されます。

- **テスト コントローラー** テスト コントローラーはエージェントとクライアントに対して発信接続できる必要があります。

- **テスト エージェント** テスト エージェントはコントローラーに対して発信接続できる必要があります。

- **クライアント** クライアントはコントローラーに対して発信接続できる必要があります。

## <a name="configure-the-incoming-ports"></a>着信ポートの構成

テスト コントローラーおよびテスト エージェントのポートを設定するには、次の手順に従います。

- **コントローラー サービス***%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\QTCcontroller.exe.config* ファイルを編集してポートの値を変更します。

    ```xml
    <appSettings>
      <add key="ControllerServicePort" value="6901"/>
    </appSettings>
    ```

- **エージェント サービス***%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\QTAgentService.exe.config* ファイルを編集してポートを変更します。

    ```xml
    <appSettings>
      <add key="AgentServicePort" value="6910"/>
    </appSettings>
    ```

- **クライアント** レジストリ エディターを使用して次のレジストリ (**ダブルワード**) 値を追加します。 クライアントは指定した範囲のポートの 1 つを使用して、テスト コントローラーからのデータを受信します。

     **HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\VisualStudio\12.0\EnterpriseTools\QualityTools\ListenPortRange\PortRangeStart**

     **HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\VisualStudio\12.0\EnterpriseTools\QualityTools\ListenPortRange\PortRangeEnd**

## <a name="see-also"></a>関連項目

- [テスト エージェントをインストールして構成する](../test/lab-management/install-configure-test-agents.md)
