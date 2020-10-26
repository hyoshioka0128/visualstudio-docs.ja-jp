---
title: Visual Studio 2015 のロックを解除する | Microsoft Docs"
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: ffb580a1-8b5d-48f5-b811-87f8036f50ea
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a71a045661c48fd36733ecd8d2266470667a5c35
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670591"
---
# <a name="how-to-unlock-visual-studio"></a>Visual Studio のロックを解除する方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio は最大で 30 日間無料で評価できます。 IDE にサインインすると、評価期間を 90 日間延長できます。 Visual Studio の使用を続けるには、次の方法で IDE のロックを解除します。

1. オンライン サブスクリプションを使用する。

2. プロダクト キーを入力する。

## <a name="to-unlock-visual-studio-using-an-online-subscription"></a>オンライン サブスクリプションを使用して Visual Studio のロックを解除するには
 Microsoft アカウントか、職場または学校のアカウントに関連付けられた MSDN または Visual Studio Online サブスクリプションを使用して Visual Studio のロックを解除するには、次の手順を実行します。

1. IDE の右上隅にある [サインイン] ボタンをクリックします (または、[ファイル] > [アカウントの設定] を選択して [アカウント設定] ダイアログを開き、[サインイン] ボタンをクリックします)。

2. Microsoft アカウントか、職場または学校のアカウントの資格情報を入力します。 Visual Studio は、アカウントに関連付けられている MSDN サブスクリプションまたは Visual Studio Team Services サブスクリプションを検索します。

> [!IMPORTANT]
> チーム エクスプローラーのツール ウィンドウから Visual Studio Team Services アカウントに接続すると、Visual Studio は関連付けられているオンライン サブスクリプションを自動的に検索します。 Visual Studio Team Services アカウントに接続した場合は、Microsoft アカウントか、職場または学校アカウントの両方を使用してサインインできます。 そのユーザー アカウントのオンライン サブスクリプションが存在する場合は、Visual Studio は自動的に IDE のロックを解除します。

## <a name="to-unlock-visual-studio-with-a-product-key"></a>プロダクト キーを使って Visual Studio のロックを解除するには

1. [ **ファイル > アカウントの設定** ] を選択して [アカウント設定] ダイアログを開き、[**プロダクトキーを使用したライセンス**] リンクをクリックします。

2. 所定の場所にプロダクト キーを入力します。

> [!TIP]
> Visual Studio のプレリリース版には、プロダクト キーはありません。 プレリリース版を使用するには、IDE にサインインする必要があります。

## <a name="addressing-license-problem-states"></a>ライセンスの問題状態に対応する

### <a name="updating-stale-licenses"></a>古いライセンスの更新
 Visual Studio のライセンスが古くなっているという、次のようなメッセージが表示されることがあります。

 ![Visual Studio の [ユーザー情報] ダイアログ](../ide/media/vs2013-userinfo.png "VS2013_UserInfo")

 このメッセージは、使用しているサブスクリプションはまだ有効だが、サブスクリプションを最新の状態に維持するために Visual Studio が使用するライセンス トークンが更新されなかったため、次のいずれかの理由でライセンス トークンが古くなったことを示します。

1. 長期間にわたって Visual Studio を使用しなかったか、インターネット接続がなかった。

2. Visual Studio からサインアウトした。

   ライセンス トークンの有効期限が切れる前に、最初は、資格情報の再入力を求めるメッセージが Visual Studio から表示されます。

   資格情報を再入力しない場合、トークンの有効期限切れが近づきます。 この場合、[アカウントの設定] ダイアログで、トークンの有効期限が完全に切れるまでの日数が通知されます。 トークンの有効期限が切れた後は、このアカウントの資格情報またはライセンスを前述の別の方法で再入力しないと、Visual Studio の使用を続行できなくなります。

> [!IMPORTANT]
> インターネットへのアクセスが限定的またはアクセスできない環境で長期間にわたって Visual Studio を使用している場合は、Visual Studio の中断を回避するためにプロダクト キーを使用してロックを解除する必要があります。

### <a name="updating-expired-licenses"></a>有効期限が切れたライセンスの更新
 サブスクリプションの有効期限が完全に切れ、Visual Studio へのアクセス権がなくなった場合は、次の操作をする必要があります。

1. サブスクリプションを更新します。 使用中のライセンスの詳細については、[ファイル] > [アカウントの設定] ダイアログで右側にあるライセンス情報を参照してください。

2. 別のアカウントに関連付けられている別のサブスクリプションを持っている場合は、[ファイル] > [アカウントの設定] ダイアログの左側にある [すべてのアカウント] 一覧にそのアカウントを追加するために、[アカウントの追加...] リンク。

## <a name="see-also"></a>参照
 [Visual Studio へのサインイン](../ide/signing-in-to-visual-studio.md)
