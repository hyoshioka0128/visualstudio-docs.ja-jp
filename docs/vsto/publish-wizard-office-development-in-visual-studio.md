---
title: 発行ウィザード (Visual Studio での Office 開発)
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.ProjectProperties.PublishWizard
- VST.PublishWizard.Publish.2007System
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ClickOnce deployment [Office development in Visual Studio], Publish Wizard
- deploying applications [Office development in Visual Studio], Publish Wizard
- Office applications [Office development in Visual Studio], Publish Wizard
- Publish Wizard, Office solutions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5d14abdd9ba6547a3aaf131084168be2e453dd04
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "77558174"
---
# <a name="publish-wizard-office-development-in-visual-studio"></a>発行ウィザード (Visual Studio での Office 開発)
  **発行ウィザード**を使用して、ソリューションファイルを指定した場所にコピーし、マニフェストファイルを作成して、セットアッププログラムを作成します。

 このウィザードにアクセスするには、[**ビルド**] メニューの [ *SolutionName*の**発行**] をクリックします。 **ソリューションエクスプローラー**から**発行ウィザード**にアクセスすることもできます。 プロジェクトノードのショートカットメニューを開き、[ **発行**] を選択します。

 以下の各セクションでは、ウィザードのページについて説明します。

## <a name="where-do-you-want-to-publish-the-application"></a>アプリケーションをどこに発行しますか?
 **このアプリケーションを発行する場所を指定します** 必須。 発行場所は、 **発行ウィザード** によってビルドからマニフェスト、アセンブリ、一時証明書、その他のファイルなどのソリューションファイルがコピーされるディレクトリです。 このディレクトリへの書き込みアクセス権が必要です。

 ディスクパス、ファイル共有、FTP サイト、または web サイトの URL として場所を入力するか、[ **参照** ] ボタンをクリックして場所を参照します。 パスは次の形式で指定できます。

- *C:\Deploy\MyApplication*や*\MyApplication*など、標準の Windows 形式の相対パスまたは絶対パス。

- * \\ \ServerName\MyApplication \\ *などの汎用名前付け規則 (UNC) パス。

- などの web サイトの URL `http://www.contoso.com/MyApplication` 。

  既定では、IIS がインストールされている場合は発行場所が、 *http://localhost/projectname/* iis がインストールされていない場合は発行 \ ディレクトリになります。

> [!NOTE]
> ターゲットコンピューターで Windows Vista が実行されている場合は、さらに考慮すべき点があります。 ローカル発行オプションを使用するには、Windows Vista コンピューターの管理者である必要があります。 また、IIS がインストールされているかどうかに関係なく、既定の場所は常に*発行 \\ *ディレクトリになります。

## <a name="what-is-the-default-installation-path-on-end-user-computers"></a>エンドユーザーのコンピューターの既定のインストールパスは何ですか。
 インストールパスは省略可能です。 必要に応じて、後でインストールパスを設定できます。 詳細については、「 [方法: Office ソリューションのインストールパスを変更する](https://msdn.microsoft.com/d0eaa07b-2d72-4902-899f-2f9fb165b8fd)」を参照してください。

 インストールパスは、エンドユーザーがカスタマイズをインストールするディレクトリです。 このディレクトリは、ソリューションで更新プログラムを確認するために使用するパスでもあります。 前のページの [**このアプリケーションを公開する場所を指定**してください] ボックスに入力したパスと同じパスでない限り、**発行ウィザード**ではこの場所にソリューションが配置されません。

 **Web サイトから** エンドユーザーがソリューションをインストールする際に従う URL を指定します。

 **UNC パスまたはファイル共有から** エンドユーザーがソリューションをインストールするときに従う UNC パスを指定します。

 **Cd-rom または Dvd-rom から** このオプションにはインストールパスは必要ありません。

 Visual Studio は CD または DVD に書き込みません。 出力を CD または DVD に手動でコピーする必要があります。

## <a name="see-also"></a>関連項目
- [ClickOnce を使用して Office ソリューションを配置する](../vsto/deploying-an-office-solution-by-using-clickonce.md)
- [[発行] ページ、プロジェクトデザイナー &#40;Visual Studio での Office 開発&#41;](../vsto/publish-page-project-designer-office-development-in-visual-studio.md)
- [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)
