---
title: ローカライズされたブートストラップパッケージを作成する |Microsoft Docs
description: 各ロケール用に2つのファイルを作成して、ClickOnce でローカライズされたバージョンのブートストラップパッケージを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- localized bootstrapper packages
- dependencies, creating localized bootstrapper packages
- prerequisites, creating localized bootstrapper packages
ms.assetid: 66a1bc7e-6540-4164-963d-557196a69d8a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9eb06c54caceb2e9329347fb1dd0114749975e7d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99927588"
---
# <a name="how-to-create-a-localized-bootstrapper-package"></a>方法: ローカライズされたブートストラップ パッケージを作成する
ブートストラップパッケージを作成した後、ロケールごとに2つのファイルを作成して、ブートストラップパッケージのローカライズバージョンを作成できます。これには、ソフトウェアライセンス条項ファイル ( *eula .rtf* など) とパッケージマニフェスト (*package.xml*) があります。

 既定では、Visual Studio 2010 には .NET Framework 4、.NET Framework 4 Client Profile、F# Runtime 2.0、および F# Runtime 4.0 用のローカライズ版のブートストラップ パッケージのみが用意されています。 3 つのステップを実行することにより、その他のブートストラップのローカライズ版パッケージを作成できます。

1. SDKs\Windows\v7.0A\Bootstrapper\Packages のロケール名の後に、という名前のフォルダーを作成します。 *\\ \<BootstrapperPackageName>*

2. ブートストラップ パッケージのソフトウェア ライセンス条項を示すファイルを作成し、新しいフォルダーに格納します。

3. *package.xml* という名前のパッケージマニフェストを作成し、文字列とカルチャを更新して、そのファイルを新しいフォルダーに配置します。 ターゲット言語で Visual Studio のブートストラップを既に作成している場合は、Visual Studio *package.xml* ファイルをコピーして、この手順で変更することができます。

> [!NOTE]
> セットアップ プロジェクトを使用してアプリケーションを配置する場合は、**Localization** プロパティを変更してアプリケーションをローカライズできます。

 [!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-create-a-localized-bootstrapper-package"></a>ローカライズ版のブートストラップ パッケージを作成するには

1. ロケール名に基づいた名前のフォルダーを作成します。

     32ビットのコンピューターで、 *SDKs\Windows\v7.0A\Bootstrapper\Packages \\ \<BootstrapperPackageName> \\* フォルダーにフォルダーを作成します。

     64ビットコンピューターで、 *\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages \\ \<BootstrapperPackageName> \\* フォルダーにフォルダーを作成します。

     次の表は、ロケールに合わせるために使用できるフォルダー名を示します。

    |Locale|[フォルダー名]|
    |------------|-----------------|
    |簡体中国語|zh-Hans|
    |繁体中国語|zh-Hant|
    |チェコ語|cs|
    |ドイツ語|de|
    |英語|en|
    |スペイン語|es|
    |フランス語|fr|
    |イタリア語|it|
    |韓国語|ko|
    |日本語|ja|
    |ポーランド語|pl|
    |ポルトガル語 (ブラジル)|pt-BR|
    |ロシア語|ru|
    |トルコ語|tr|

2. ブートストラップ パッケージのソフトウェア ライセンス条項を示すファイルを作成し、新しいフォルダーに格納します。

3. *package.xml* という名前のパッケージマニフェストを作成し、新しいフォルダーに配置します。 詳細については、「 [方法: パッケージマニフェストを作成](../deployment/how-to-create-a-package-manifest.md)する」を参照してください。

4. パッケージ マニフェストの `<Strings>` セクションを更新して、文字列がロケールに対応する正しい言語で表示されるようにします。

5. `<String Name="Culture">` の値をフォルダー名と一致するように変更します。

6. *package.xml* ファイルを保存します。

### <a name="to-create-a-bootstrapper-package-for-net-framework-35-service-pack-1-localized-in-french"></a>フランス語でローカライズした .NET Framework 3.5 Service Pack 1 用のブートストラップ パッケージを作成するには

1. *Fr* という名前のフォルダーを作成します。 フォルダー名はロケール名と一致する必要があります。

     32 ビット コンピューターでは、このフォルダーは *\Program Files\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages\DotNetFX35SP1\\* フォルダーに作成します。

     64ビットコンピューターで、 *\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages\DotNetFX35SP1 \\* フォルダーにフォルダーを作成します。

2. ソフトウェアライセンス条項のローカライズ版を *fr* フォルダーに配置します。

3. \Microsoft ファイル *(x86) SDKs\Windows\v7.0A\Bootstrapper\Packages\DotNetFX35SP1\en\package.xml* ファイルを *fr* フォルダーにコピーし、XML デザイナーでファイルを開きます。

4. パッケージ マニフェストの `<Strings>` セクションを更新して、エラー文字列がフランス語で表示されるようにします。

5. `<String Name="Culture">`値を *fr* に変更します。

6. *package.xml* ファイルを保存します。

## <a name="see-also"></a>関連項目
- [ブートストラップ パッケージの作成](../deployment/creating-bootstrapper-packages.md)
- [アプリケーション配置の必要条件](../deployment/application-deployment-prerequisites.md)
- [方法: パッケージ マニフェストを作成する](../deployment/how-to-create-a-package-manifest.md)