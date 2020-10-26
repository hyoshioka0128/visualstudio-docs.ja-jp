---
title: 管理者ポータルでのサブスクリプションの編集 | Microsoft Docs
author: evanwindom
ms.author: lank
manager: cabuschl
ms.assetid: 97ac8e4d-7a03-42f8-98cb-15bcaa90ef65
ms.date: 07/30/2020
ms.topic: how-to
description: 管理者がサブスクリプションの割り当てを編集する方法を説明します。
ms.openlocfilehash: fb43f9ceae86acf5804a6cd32dd383dcd2e9af38
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "87453733"
---
# <a name="edit-visual-studio-subscription-assignments"></a>Visual Studio サブスクリプションの割り当ての編集
サブスクリプション管理者は、組織内の個人に割り当てられているサブスクリプションに変更を加えることができます。  この記事では、行うことができる変更の種類と、必要な手順について説明します。

   > [!NOTE]
   > Azure Active Directory グループ使って割り当てられたサブスクライバーのサブスクリプションの詳細を変更する必要がある場合は、グループからそれらを削除して、管理ポータルに個別に追加する必要があります。  

## <a name="change-subscriber-information"></a>サブスクライバーの情報を変更する
サブスクライバー情報を編集してエラーを修正したり情報を更新したりすることができます。

サブスクライバーを編集するには、サブスクライバーの電子メール アドレスの横にマウス ポインターを移動すると表示される省略記号 (...) を選択します。 ドロップダウン リストが表示されます。  **[編集]** を選択して、サブスクライバーの詳細を変更します。 
> [!div class="mx-imgBorder"]
> ![編集するサブスクライバーを選択する](_img/edit-license/select-subscriber.png "省略記号をクリックし、[編集] を選択します。")

サブスクライバーの [名]、[姓]、[サブスクリプション レベル]、[電子メール アドレス]、[国]、[言語]、[ダウンロード]、および [参照] フィールドを更新できます。 サブスクライバーの情報を編集して、 **[保存]** をクリックします。

## <a name="edit-multiple-subscribers-using-bulk-edit"></a>一括編集を使用して複数のサブスクライバーを編集する


一括編集プロセスを使用して、一度に複数のサブスクライバーを編集することができます。 この機能は、会社の電子メール アドレスを変更している組織、または組織がダウンロードへのアクセスを制限することにした場合に主に使用されます。

<br>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4vkAF]

   > [!IMPORTANT]
   > 一括編集を使用して、サブスクリプション レベル (つまり Enterprise や Professional など) およびサブスクリプション GUID を変更することはできません。  特定のサブスクリプション GUID をユーザーに割り当てる必要がある場合は、サブスクリプション ID を選択してユーザーを追加するための手順を実行します。 変更されたこれらの項目を一括編集テンプレートでアップロードしようとすると、アップロードは失敗します。

1. 複数のサブスクライバーを一度に追加するには、[サブスクライバー] タブに移動します。上部リボンの **[一括編集]** をクリックします。

2. 一括編集では、Excel テンプレートを使用してサブスクライバー情報を編集します。 一括編集ボックスで、 **[Excel にエクスポート]** をクリックして、すべての情報を含む現在のサブスクライバーの一覧をダウンロードします。
   > [!div class="mx-imgBorder"]
   > ![ライセンスの編集 - 一括編集一覧のエクスポート](_img/edit-license/edit-license-bulk-edit-export.png "現在のサブスクリプションの一覧を作成するには、[Excel にエクスポート] をクリックします。")

3. 次に、アップロードする前に簡単に見つけて必要な変更を行うことができるように、ファイルをローカルに保存します。 アップロードを確実に成功させるには、一括編集ファイル内で**サブスクリプション レベルまたはサブスクリプションの GUID を編集しないでください**。編集すると、アップロードが失敗します。

4. Visual Studio サブスクリプション管理ポータルに戻り、[一括編集] ダイアログ ボックスで **[参照]** をクリックします。 保存した Excel ファイルを選んで、 **[OK]** をクリックします。 アップロードの進行状況が画面に表示されます。
   > [!div class="mx-imgBorder"]
   > ![ライセンスの編集 - 一括編集のファイルのアップロード](_img/edit-license/edit-license-bulk-file-upload1.png "完成した Excel ファイルの場所を参照して選択し、[OK] をクリックします。")

5. ファイルをアップロードしたら、成功したことを知らせる通知が表示されます。 この時点で、編集内容がサブスクライバーの情報に反映されます。

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps ドキュメント](https://docs.microsoft.com/azure/devops/)
- [Azure ドキュメント](https://docs.microsoft.com/azure/)
- [Microsoft 365 ドキュメント](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>次の手順
- 特定のサブスクリプション ID を割り当てる必要がありますか? サブスクリプション ID の割り当てに関する記事を参照してください。 
- 特定のサブスクリプションを検索する方法については、[サブスクリプションの検索](search-license.md)に関する記事を参照してください。
- すべてのサブスクリプションの一覧を作成する必要がありますか?  [サブスクリプションのエクスポート](exporting-subscriptions.md)に関する記事を参照してください。
