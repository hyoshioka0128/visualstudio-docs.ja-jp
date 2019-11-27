---
title: Visual Studio 管理者ガイド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-install
ms.topic: conceptual
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
ms.assetid: 4af353f5-6cfd-4ebe-bcfb-f42306e451a0
caps.latest.revision: 76
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: a59f9f2cb2548d6d40670832e66d4df5c83680df
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295916"
---
# <a name="visual-studio-administrator-guide"></a>Visual Studio Administrator Guide
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の最新のドキュメントについては、「 [Visual studio 管理者ガイド](/visualstudio/install/visual-studio-administrator-guide)」を参照してください。

各対象コンピューターが[最小インストール要件](https://visualstudio.microsoft.com/vs/older-downloads/)を満たしている限り、Visual Studio 2015 をネットワークに配置できます。 /layout スイッチを指定してインストール ファイルを実行し (「[Visual Studio のオフライン インストールを作成する](../install/create-an-offline-installation-of-visual-studio.md)」ページの説明を参照)、そのファイルをローカル コンピューターからネットワーク共有にコピーすることで、ネットワーク共有を作成できます。 ISO を使用している場合は、ISO をマウントして共有するか、ISO をネットワーク共有にコピーすることができます。  
  
 ネットワーク共有からのインストールは、出所のソースの場所を記憶します。 これは、クライアント マシンの修復に、クライアントのインストール元のネットワーク共有に戻る必要があることを意味します。 ネットワークの場所は、Visual Studio 2015 クライアントが組織で実行されると予想される有効期間に合わせて配置されるよう慎重に選択してください。  
  
## <a name="detection-and-servicing-keys"></a>検出キーおよびサービス キー  
 レジストリの検出サブキーを使用して、Visual Studio 製品がコンピューターに既にインストールされているかどうかを確認できます。 自動化された展開で検出キーを使用して、インストールを続行するために必要かどうかを確認します。  「[システム要件の検出](../extensibility/internals/detecting-system-requirements.md)[システム要件の検出]」を参照してください。  
  
## <a name="avoiding-reboots"></a>再起動の回避  
 Visual Studio を配置する前に Visual Studio の適切な前提条件を確認することによって、再起動を減らすことができます。 .NET Framework では、最初に .NET Framework 4.6 をインストールせずに Visual Studio 2015 を展開する場合は、Windows 8 を実行しているコンピューターの再起動が必要になることがあります。  
  
 Windows および Android デバイスのエミュレーションでは、Windows 機能の HYPER-V がオンになっていないと、コンピューターの再起動が必要になる場合があります。 Web 開発では、Windows 機能の Web サーバーがオンになっていないと、コンピューターの再起動が必要になる場合があります。 Office の開発では、Windows 機能の Windows Identify Foundation がオンになっていないと、コンピューターの再起動が必要になる場合があります。 Web 開発では、Windows 機能の Web Server がオンになっていないと、コンピューターの再起動が必要になる場合があります。 Office の開発では、Windows 機能の Windows Identify Foundation がオンになっていないと、コンピューターの再起動が必要になる場合があります。 Windows 機能の検出とインストールを自動化する方法の詳細については、「 [Windows Server 2008 R2 の Server Core インストールを実行しているサーバーにサーバー ロールをインストールする](https://technet.microsoft.com/library/ee441260(v=ws.10).aspx)」を参照してください。  
  
## <a name="error-return-codes"></a>エラー リターン コード  
 次の表に重要なエラー コードを示します。 これらのエラー コードは、再起動が必要かどうか、インストールが成功したかどうかを判断するために自動化で使用できます。 エラーコードが表示された場合は、「 [Visual Studio のインストール](../install/install-visual-studio-2015.md)」ページのトラブルシューティングの手順を検討してください。  
  
|セットアップの状態|再起動は不要|再起動が必要|説明|  
|------------------|--------------------------|----------------------|-----------------|  
|成功|0x00000000 [0]|0x00000bc2 [3010]|インストールは成功しました。|  
|[ブロック]|0x80044000 [-2147205120]|0x8004C000 [-2147172352]|報告するブロックが "再起動の保留中" だけの場合、戻り値は "不完全-再起動が必要" の値 (0x80048bc7) です。|  
|キャンセル|0x00000642 [1602]|0x80048642 [-2147187134]|再起動値が返されると、結果コードは 1602 です。|  
|不完全-再起動が必要|N/A|0x80048bc7 [-2147185721]|インストールを続行するには再起動が必要です。|  
|失敗|0x00000643 [1603]|0x80048643 [-2147187133]|再起動値が返されると、結果コードは 1603 です。|  
  
## <a name="interactive-administrator-installer"></a>対話型の管理者のインストーラー  
 Visual Studio のインストールに対話型のインストーラーを作成する場合、Visual Studio インストーラーから進行状況を表示できます。 Visual Studio 2015 インストーラーは、オープン ソースの Windows インストーラー XML (WiX) チェーン元テクノロジ ("書き込み" とも呼ばれる) に基づいて構築されます。 書き込みテクノロジは、burn と netfx4 の 2 つの通信プロトコルをサポートします。 簡単なリファレンスについては、 [wixtoolset.org](https://wixtoolset.org/)にある exepackage 要素のドキュメントで、プロトコル属性の説明を参照してください。このプロトコル属性の WiX オープンソースの実装の確認は、統合に必要な場合があります。  
  
## <a name="controlling-what-is-installed"></a>インストール内容の制御  
 エンド ユーザーによるインストール内容を制御する場合、管理者ファイルのインストールとコマンド ラインの 2 つのオプションがあります。 エンド ユーザーが Visual Studio インストーラー エクスペリエンスから選択できる内容を制限することが目的の場合は、管理者ファイルのインストールを選択できます、 初期構成を作成しつつ、エンド ユーザーが独自の Visual Studio インストーラー エクスペリエンスから選択できるようにする場合、コマンド ラインのパラメーターを選択します。  
  
 管理者ファイル エクスペリエンスの詳細については、「 [How to: Create and Run an Unattended Installation of Visual Studio](../install/how-to-create-and-run-an-unattended-installation-of-visual-studio.md) 」および「 [How to: Automatically apply product keys when deploying Visual Studio](../install/how-to-automatically-apply-product-keys-when-deploying-visual-studio.md)」を参照してください。  コマンドラインコントロールの詳細については、「[コマンドラインパラメーターを使用して Visual Studio をインストールする](../install/use-command-line-parameters-to-install-visual-studio.md)」を参照してください。  
  
## <a name="specifying-customer-feedback-settings"></a>顧客フィードバック設定の指定  

既定では、Visual Studio をインストールすると、カスタマー フィードバックが有効になります。 次のレジストリ キーの値を文字列 "0" に変更することで、個々のコンピューターで顧客からのカスタマー フィードバックを無効にするように Visual Studio を構成できます。  
  
**HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\VisualStudio\SQM**  
**OptIn**  
  
(たとえば、HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\VisualStudio\SQM OptIn="0" に変更します)  
  
## <a name="related-topics"></a>関連トピック  
  
|トピック|説明|  
|-----------|-----------------|  
|[方法: Visual Studio の特定のリリースをインストールする](../install/how-to-install-a-specific-release-of-visual-studio.md)|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]の現在のバージョンの特定の構成をインストールする方法について説明します。|  
|[方法: Visual Studio の無人インストールを作成して実行する](../install/how-to-create-and-run-an-unattended-installation-of-visual-studio.md)|無人モードで [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] をインストールする方法について説明します。|  
|[方法: Visual Studio の展開時にプロダクト キーを自動的に適用する](../install/how-to-automatically-apply-product-keys-when-deploying-visual-studio.md)|複数のコンピューターに展開するときにプロダクトキーを適用する方法について説明します。|  
|[ヘルプ ビューアーの管理者ガイド](../ide/help-viewer-administrator-guide.md)|インターネットにアクセスできない、またはないネットワーク環境のローカルヘルプのインストールを管理する方法について説明します。|  
|[Visual Studio のインストール](../install/install-visual-studio-2015.md)|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]のインストール方法を説明するトピックへの手順とリンクを示します。|