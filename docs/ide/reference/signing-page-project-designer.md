---
title: '[署名] ページ (プロジェクト デザイナー)'
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: reference
f1_keywords:
- vs.AddNewStrongNameKey
- ResolveKeySource.KeyFileForSignAssemblyNotImported
- vb.ProjectPropertiesSigning.ChangePasswordDialog
- ResolveKeySource.KeyFileForManifestNotImported
- vb.ProjectPropertiesSigning
- vb.ProjectPropertiesSigning.PasswordNeededDialog
- vb.ProjectPropertiesSigning.PfxPasswordDialog
helpviewer_keywords:
- Project Designer, Signing page
- Signing page in Project Designer
ms.assetid: dab3ba13-2f92-4827-92bd-1be3c35bc48b
author: Mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fee2244792d73924793ae82def1f533b909403c5
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85418861"
---
# <a name="signing-page-project-designer"></a>[署名] ページ (プロジェクト デザイナー)

**プロジェクト デザイナー**の **[署名]** ページを使用して、アプリケーション マニフェストと配置マニフェストに署名し、アセンブリに署名します (厳密な名前の署名)。

アプリケーション マニフェストと配置マニフェストの署名は、アセンブリの署名と同じく **[署名]** ページで実行されますが、異なるプロセスであることに注意してください。

また、キー ファイル情報のストレージは、マニフェストの署名とアセンブリの署名とは異なります。 マニフェストの署名では、キー情報はコンピューターの暗号化ストレージ データベースと現在のユーザーの Windows 証明書ストアに格納されます。 アセンブリの署名では、キー情報はコンピューターの暗号化ストレージ データベースだけに格納されます。

この **[署名]** ページにアクセスするには、**ソリューション エクスプローラー**でプロジェクト ノードを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 **プロジェクト デザイナー**が表示されたら、 **[署名]** タブをクリックします。

## <a name="application-and-deployment-manifest-signing"></a>アプリケーション マニフェストと配置マニフェストの署名

**[ClickOnce マニフェストに署名する]** チェック ボックス

公開キーと秘密キーのペアを使用して、アプリケーション マニフェストと配置マニフェストに署名するには、このチェック ボックスを選択します。 この方法の詳細については、「[方法 : アプリケーション マニフェストおよび配置マニフェストに署名する](../../ide/how-to-sign-application-and-deployment-manifests.md)」を参照してください。

**[ストアから選択]** ボタン

現在のユーザーの個人証明書ストアから既存の証明書を選択できます。 アプリケーション マニフェストと配置マニフェストの署名にこれらの証明書のいずれかを選択することができます。

**[ストアから選択]** をクリックすると、 **[証明書の選択]** ダイアログ ボックスが開きます。ここには、現在有効で (期限が切れていない)、秘密キーを持つ個人証明書ストア内の証明書が一覧表示されます。 選択した証明書の目的には、コード署名を含める必要があります。

**[証明書のプロパティを表示します]** をクリックすると、 **[証明書の詳細]** ダイアログ ボックスが表示されます。 このダイアログ ボックスには、証明書の詳細情報、および追加オプションが含まれています。 追加のヘルプ情報を表示するには **[証明書の詳細情報]** をクリックします。

**[ファイルから選択]** ボタン

既存のキー ファイルから証明書を選択できます。

**[ファイルから選択]** をクリックすると、 **[ファイルの選択]** ダイアログ ボックスが開きます。ここで証明書のキー (.pfx) ファイルを選択することができます。 ファイルはパスワードで保護する必要があり、個人証明書ストアに格納しておくことはできません。

**[ファイルを開くためのパスワードを入力してください]** ダイアログ ボックスで、証明書のキー (.pfx) ファイルを開くためのパスワードを入力します。 パスワード情報は、個人のキー コンテナー一覧と個人用証明書ストアに格納されます。

**[テスト証明書の作成]** ボタン

テスト用の証明書を作成できます。 テスト証明書は、ClickOnce アプリケーション マニフェストと配置マニフェストの署名に使用されます。

**[テスト証明書の作成]** をクリックすると、 **[テスト証明書の作成]** ダイアログ ボックスが開きます。ここでテスト証明書の厳密な名前のキー ファイルのパスワードを入力することができます。 このファイルの名前は *projectname*_TemporaryKey.pfx です。 パスワードを入力せずに **[OK]** をクリックすると、.pfx ファイルはパスワードで暗号化されません。

**[タイムスタンプ サーバーの URL]** ボックス

署名にタイムスタンプを記録するサーバーのアドレスを指定します。 証明書を提供すると、この外部サイトによってアプリケーションが署名された時間が確認されます。

## <a name="assembly-signing"></a>アセンブリの署名

**[アセンブリの署名]** チェック ボックス

アセンブリに署名し、厳密な名前のキー ファイルを作成するには、このチェック ボックスをオンにします。 **プロジェクト デザイナー**を使用してアセンブリに署名する詳細については、「[方法: アセンブリに署名する (Visual Studio)](../managing-assembly-and-manifest-signing.md#how-to-sign-an-assembly-in-visual-studio)」を参照してください。

このオプションは、Windows ソフトウェア開発キット (Windows SDK) で提供される Al.exe ツールを使用して、アセンブリに署名します。 Al.exe の詳細については、「[方法: 厳密な名前でアセンブリに署名する](/dotnet/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name)」を参照してください。

**[厳密な名前のキー ファイルを選択してください]** 一覧

アセンブリに署名するために使用する新規または既存の厳密な名前のキー ファイルを指定できます。 **[\<Browse...>]** を選択して、既存のキー ファイルを選択します。

**[\<New...>]** を選択して、アセンブリの署名に使用する新しいキー ファイルを作成します。 **[厳密な名前キーの作成]** ダイアログ ボックスが表示されます。ここでキー ファイル名を指定し、パスワードを使用してキー ファイルを保護することができます。 パスワードの長さは 6 文字以上にする必要があります。 パスワードを指定すると、Personal Information Exchange (.pfx) ファイルが作成されます。パスワードを指定しない場合は、厳密な名前のキー (.snk) ファイルが作成されます。

**[パスワードの変更]** ボタン

アセンブリの署名に使用される、Personal Information Exchange (.pfx) キー ファイルのパスワードを変更します。

**[パスワードの変更]** をクリックすると、 **[キー パスワードの変更]** ダイアログ ボックスが開きます。 このダイアログ ボックスでは、**古いパスワード**はキー ファイルの現在のパスワードです。 **新しいパスワード**の長さは 6 文字以上にする必要があります。 パスワード情報は、現在のユーザーの Windows 証明書ストアに格納されます。

**[遅延署名のみ]** チェック ボックス

遅延署名を有効にするには、このチェック ボックスを選択します。

遅延署名されたプロジェクトは実行されず、デバッグできないことに注意してください。 ただし、[Sn.exe (厳密名ツール)](/dotnet/framework/tools/sn-exe-strong-name-tool) と `-Vr` オプションを使用すると、開発時に検証をスキップできます。

> [!NOTE]
> アセンブリに署名するときに、秘密キーへのアクセス権がない場合があります。 たとえば、組織には、開発者が日常的にアクセスしない厳重に保護されたキーのペアがある場合があります。 公開キーは使用可能ですが、秘密キーへのアクセスは少数のユーザーに限定されます。 このような場合は、*遅延*または*部分署名*を使用して公開キーを提供し、アセンブリが引き渡されるまで、秘密キーの追加を遅らせることができます。

## <a name="see-also"></a>関連項目

- [プロジェクトのプロパティのリファレンス](../../ide/reference/project-properties-reference.md)
- [アセンブリおよびマニフェストへの署名の管理](../../ide/managing-assembly-and-manifest-signing.md)
- [方法: アプリケーション マニフェストと配置マニフェストの署名](../../ide/how-to-sign-application-and-deployment-manifests.md)
- [方法: アセンブリに署名する (Visual Studio)](../managing-assembly-and-manifest-signing.md#how-to-sign-an-assembly-in-visual-studio)
- [方法: 厳密な名前でアセンブリに署名する](/dotnet/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name)
- [厳密な名前付きアセンブリ](/dotnet/framework/app-domains/strong-named-assemblies)
