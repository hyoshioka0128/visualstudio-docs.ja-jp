---
title: アカウント オプション リファレンス
ms.date: 12/10/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Environment.RoamingSettings
ms.assetid: 3cfe09d2-1120-46e8-b882-f7056acb778b
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9ff457523024db49502ae982a390d9a7be6ba9dd
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75595905"
---
# <a name="accounts-environment-options-dialog-box"></a>[アカウント] ([オプション] ダイアログ ボックス - [環境])

このページを使用すると、Visual Studio へのサインインに使用するアカウントに関連するさまざまなオプションを設定できます。

## <a name="personalization-account"></a>個人アカウント

### <a name="synchronize-settings-across-devices"></a>デバイス間で設定を同期する

このオプションを使用して、複数のコンピューター間で設定を同期するかどうかを指定します。 詳細については、「[同期された設定](../../ide/synchronized-settings-in-visual-studio.md)」を参照してください。

### <a name="enable-device-code-flow"></a>デバイス コード フローを有効にする

このオプションをオンにすると、 **[ファイル]**  >  **[アカウント設定]** ページで **[アカウントの追加]** を選択したときの Visual Studio の動作が変わります。 **[アカウントにサインイン]** ページが表示されるのではなく、サインインするための URL とコードを Web ブラウザーに貼り付けることができるダイアログ ボックスが表示されます。 このオプションは、たとえば古いバージョンの Internet Explorer を使用していたり、ファイアウォールでアクセスが制限されていたりして、通常の方法では Visual Studio にサインインできない場合に便利です。 詳しくは、「[複数のユーザー アカウントを使って作業する](../work-with-multiple-user-accounts.md#add-an-account-using-device-code-flow)」をご覧ください。

## <a name="registered-azure-clouds"></a>登録済み Azure クラウド

このセクションには、Visual Studio へのサインインに使用されている 1 つまたは複数のアカウントを通じてアクセスできる Azure のクラウド インスタンスが表示されます。 たとえば、会社のデータ センターで Azure の非公開インスタンスにアクセスできる場合があります。 または、Azure のソブリンまたは政府インスタンスへのアクセス権を持っている可能性があります (Azure China 21 Vianet や Azure U.S.Government の Azure など)。 グローバル Azure クラウド インスタンスは既定で一覧に表示され、削除することはできません。

**[追加]** ボタンを選択して、追加の Azure クラウドを登録します。 **[新しい Azure クラウドの追加]** ダイアログには、接続できるいくつかのよく知られている Azure クラウド インスタンスが一覧表示されます。または、非公開の Azure エンドポイントに対する URL を入力することができます。

![新しい Azure クラウド インスタンスを追加する](media/add-new-azure-cloud.png)

追加の Azure クラウドを登録した後は、Visual Studio にサインインするときにサインインする Azure クラウドを選択できます。

## <a name="see-also"></a>関連項目

- [複数のコンピューター間で設定を同期する](../synchronized-settings-in-visual-studio.md)
- [Visual Studio へのサインイン](../signing-in-to-visual-studio.md)
- [複数のユーザー アカウントを使って作業する](../work-with-multiple-user-accounts.md)
- [環境設定](../environment-settings.md)
