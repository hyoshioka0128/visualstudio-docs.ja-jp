---
title: プロダクト キーを使用してターミナル サービスによるインターネット デモンストレーションをサポートする | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: 1c5ede60-cb5a-4d5f-a6a2-a1f536f6c4ad
ms.date: 03/09/2020
ms.topic: conceptual
description: プロダクト キーを使用してターミナル サービスによるインターネット デモンストレーションをサポートし、RDS アクセスを有効にする方法を説明します
ms.openlocfilehash: 2d5f23f0d161ee9f50569e0ff7f8ce585c8c49ff
ms.sourcegitcommit: eeff6f675e7850e718911647343c5df642063d5e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2020
ms.locfileid: "80232441"
---
# <a name="internet-demonstrations-via-terminal-services"></a>ターミナル サービスを介したインターネット デモンストレーション
Visual Studio サブスクリプションがあれば、ターミナル サービス (Windows Server 2003 または Windows Server 2008) やリモート デスクトップ サービス (Windows Server 2008 R2 以降) を介してエンド ユーザーに自分のプログラムのインターネット デモンストレーションへアクセスしてもらうことができます。 この方法で、最大 200 人の匿名ユーザーが同時に会員のデモンストレーションにアクセスすることができます。 デモンストレーションに実稼動データを使用することはできません。 Visual Studio サブスクライバーは、自分のアプリケーションのデモンストレーションをエンド ユーザーに提供することができます。 ターミナル サービス (TS) またはリモート デスクトップ サービス (RDS) を使用したこのインターネット デモンストレーションのシナリオにおいてのみ、Visual Studio サブスクリプションを持たないエンド ユーザーがデモンストレーション アプリケーションを操作できます。これは、そのソフトウェアが Visual Studio サブスクリプションでライセンスを付与されている間に限ります。

これは、開発/テスト権限に追加されるもので、Visual Studio サブスクライバーが必要に応じて必要な数の RDS または TS 接続を使用することができます。

## <a name="enabling-rds-access"></a>RDS アクセスを有効にする
Visual Studio サブスクライバーは、[サブスクライバー ポータル](https://my.visualstudio.com?wt.mc_id=o~msft~docs)の [[プロダクト キー]](https://my.visualstudio.com/productkeys?wt.mc_id=o~msft~docs) タブに提供されるプロダクト キーを入力し、Windows Server に RDS でアクセスできるユーザー数を増やすことができます。 プロダクト キーを取得するには、[プロダクト キー] ページに接続して下方向にスクロールし、実行中の Windows Server のバージョンを表示します。 [Windows Server <バージョン> R2 リモート デスクトップ サービス <ユーザーまたはデバイス> 接続] を検索し、 **[キーの要求]** リンクをクリックします。 たとえば、Windows Server 2012 R2 で RDS を使用して、展開にユーザー CAL を使用している場合は、[Windows Server 2012 リモート デスクトップ サービス ユーザー接続 (50)] を選択します。
Windows Server 2008 R2 では、種類ごとに 5 つのキーが利用でき、各キーが 20 の接続に対応します。 Windows Server 2012 R2 では、種類ごとに 4 つのキーが利用でき、それぞれ 50 の接続に対応します。

## <a name="to-enable-additional-connections-in-windows-server"></a>Windows Server への追加の接続を有効にするには:
1. サーバー マネージャーを開きます。
2. 左側にあるナビゲーション ウィンドウでサーバーのリストを開きます。
3. ライセンス サーバーを右クリックして、[ライセンスのインストール] を選択します。
4. ウィザードの手順に従って操作します。  契約の種類を選択するときには [License Pack (量販店での購入)] を選択し、個人用ポータルから取得したプロダクト キーを入力します。

次の条件が満たされている場合、エンド ユーザーは RDS を介してアプリケーションにアクセスするために接続できます。
- ユーザーは匿名 (認証されていない状態) でなければなりません。
- 接続はインターネット経由でなければなりません。
- 最大で 200 の同時ユーザー接続をアプリケーションのデモンストレーションに使用できます。
- ユーザー接続を有効にするプロダクト キーは Visual Studio サブスクライバーが取得しなければなりません。

## <a name="see-also"></a>関連項目
- [Windows Server ドキュメント](https://docs.microsoft.com/windows-server/)
- [Visual Studio ドキュメント](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps ドキュメント](https://docs.microsoft.com/azure/devops/)
- [Azure ドキュメント](https://docs.microsoft.com/azure/)
- [Microsoft 365 ドキュメント](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>次の手順
RDS の配置に関するガイダンスが必要な場合は、 https://techcommunity.microsoft.com/t5/Ask-The-Performance-Team/bg-p/AskPerf のマルチパート ブログ シリーズ「**Remote Desktop Services (RDS) 2012 session deployment (リモート デスクトップ サービス (RDS) 2012 セッションの配置)** 」をご覧ください。 

質問がある場合は、Microsoft [リモート デスクトップ サービス フォーラム](https://social.technet.microsoft.com/Forums/windowsserver/home?forum=winserverTS)にアクセスしてください。
