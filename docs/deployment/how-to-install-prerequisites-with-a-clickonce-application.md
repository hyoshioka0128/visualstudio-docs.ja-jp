---
title: ClickOnce アプリを使用した必須コンポーネントのインストール
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], prerequisites
- prerequisites, ClickOnce
- components, bootstrapping
ms.assetid: e964fca5-fdfd-47cf-a1c9-7fb96b1c88b5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 52e815c45f776635d811c073114e22c3bd002de0
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2020
ms.locfileid: "90809121"
---
# <a name="how-to-install-prerequisites-with-a-clickonce-application"></a>方法: ClickOnce アプリケーションと共に必須コンポーネントをインストールする
すべてのアプリケーションでは、実行する前に、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 正しいバージョンの .NET Framework がコンピューターにインストールされている必要があります。多くのアプリケーションには、その他の前提条件もあります。 アプリケーションを発行するときに [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 、アプリケーションと共にパッケージ化する前提条件コンポーネントのセットを選択できます。 インストール時に、前提条件ごとにチェックが行われ、既に存在するかどうかが確認されます。インストールされていない場合は、アプリケーションをインストールする前にインストールされ [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。

 パッケージ化および発行の前提条件ではなく、コンポーネントのダウンロード先を指定することもできます。 たとえば、発行するすべてのアプリケーションに必須コンポーネントを含めるのではなく、すべての前提条件のインストーラーを含む、集中管理されたファイル共有または Web の場所を使用することができます。インストール時には、コンポーネントがダウンロードされ、その場所からインストールされます。

> [!IMPORTANT]
> 最初のアプリケーションを発行する前に、開発用コンピューターに前提条件インストーラーパッケージを追加する必要があり [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 詳細については、「 [方法: ClickOnce アプリケーションに必須コンポーネントを含める](../deployment/how-to-include-prerequisites-with-a-clickonce-application.md)」を参照してください。

 必須コンポーネントは、**プロジェクトデザイナー**の [**発行**] ペインからアクセスできる [**必須コンポーネント**] ダイアログボックスで管理されます。

> [!NOTE]
> 事前に定義された前提条件の一覧に加えて、独自のコンポーネントを一覧に追加することができます。 詳細については、「 [ブートストラップパッケージの作成](../deployment/creating-bootstrapper-packages.md)」を参照してください。

### <a name="to-specify-prerequisites-to-install-with-a-clickonce-application"></a>ClickOnce アプリケーションと共にインストールするための前提条件を指定するには

1. **ソリューションエクスプローラー**でプロジェクトを選択し、[**プロジェクト**] メニューの [**プロパティ**] をクリックします。

2. [ **発行** ] ペインを選択します。

3. [ **必須コンポーネント** ] ボタンをクリックして、[ **必須コンポーネント** ] ダイアログボックスを開きます。

4. **[必須コンポーネント]** ダイアログ ボックスの **[必須コンポーネントをインストールするセットアップ プログラムを作成する]** チェック ボックスをオンにします。

5. [ **前提条件** ] 一覧で、インストールするコンポーネントを確認し、[ **OK]** をクリックします。

     選択したコンポーネントは、アプリケーションと共にパッケージ化および発行されます。

### <a name="to-specify-a-different-download-location-for-prerequisites"></a>前提条件として別のダウンロード場所を指定するには

1. **ソリューションエクスプローラー**でプロジェクトを選択し、[**プロジェクト**] メニューの [**プロパティ**] をクリックします。

2. [ **発行** ] ペインを選択します。

3. [ **必須コンポーネント** ] ボタンをクリックして、[ **必須コンポーネント** ] ダイアログボックスを開きます。

4. **[必須コンポーネント]** ダイアログ ボックスの **[必須コンポーネントをインストールするセットアップ プログラムを作成する]** チェック ボックスをオンにします。

5. [ **必須コンポーネントのインストール場所の指定** ] セクションで、[ **次の場所から必須コンポーネントをダウンロード**する] を選択します。

6. ドロップダウンリストから場所を選択するか、URL、ファイルパス、または FTP の場所を入力して、[OK] をクリックし **ます。**

    > [!NOTE]
    > 指定されたコンポーネントのインストーラーが指定された場所に存在することを確認する必要があります。

## <a name="see-also"></a>こちらもご覧ください
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)