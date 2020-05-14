---
title: '方法 : アプリケーション マニフェストおよび配置マニフェストに署名する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- manifests [Visual Studio]
- code signing [Visual Studio], Authenticode
- deployment manifests [Visual Studio]
- signing manifests [Visual Studio]
- application manifests [Visual Studio]
- ClickOnce deployment [Visual Studio], signing assemblies
- key files [Visual Studio]
- assemblies [Visual Studio], signing
ms.assetid: 64173505-8bfb-41cf-a0de-b9075173f3a2
caps.latest.revision: 61
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7924201f4cf58e1066434707a8453b0fe1913bc6
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670718"
---
# <a name="how-to-sign-application-and-deployment-manifests"></a>方法 : アプリケーション マニフェストおよび配置マニフェストに署名する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ClickOnce 配置を使用してアプリケーションを発行しようとする場合は、アプリケーション マニフェストと配置マニフェストに、公開キーと秘密キーのペアを使用して署名し、さらに Authenticode テクノロジを使用して署名する必要があります。 これらのマニフェストには、Windows 証明書ストアの証明書またはキー ファイルを使用して署名できます。

 ClickOnce 配置について詳しく、「[ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)」をご覧ください。

 .exe ベースのアプリケーションでは、ClickOnce マニフェストの署名を省略できます。 詳細については、このドキュメントの「未署名のマニフェストの生成」を参照してください。

 キー ファイルの作成については、「[方法 : 公開キーと秘密キーのキー ペアを作成する](https://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114)」をご覧ください。

> [!NOTE]
> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] では、拡張子 .pfx を持つ Personal Information Exchange (PFX) キー ファイルだけがサポートされます。 ただし、プロジェクトのプロパティの **[署名]** ページにある **[ストアから選択]** をクリックすると、現在のユーザーの Windows 証明書ストアから、他の種類の証明書を選ぶことができます。

### <a name="to-sign-application-and-deployment-manifests-using-a-certificate"></a>証明書を使用してアプリケーション マニフェストおよび配置マニフェストに署名するには

1. プロジェクトのプロパティ ウィンドウへ移動します (**ソリューション エクスプローラー** でプロジェクト ノードを右クリックして **[プロパティ]** をクリックするか、 **[クイック起動]** ウィンドウに「**プロジェクトのプロパティ**」と入力するか、**ソリューション エクスプローラー** ウィンドウ内で Alt + Enter キーを押す)。 **[署名]** タブの **[ClickOnce マニフェストに署名する]** チェック ボックスをオンにします。

2. **[ストアから選択]** をクリックします。

     **[証明書の選択]** ダイアログ ボックスが表示され、Windows 証明書ストアの内容が表示されます。

    > [!TIP]
    > **[証明書のプロパティを表示します]** をクリックすると、 **[証明書の詳細]** ダイアログ ボックスが表示されます。 このダイアログ ボックスには、証明書の詳細情報、および追加オプションが含まれています。 追加のヘルプ情報を表示するには **[証明書]** をクリックします。

3. マニフェストの署名に使用する証明書を選択します。

4. また、 **[タイムスタンプ サーバーの URL]** ボックスでタイムスタンプ サーバーのアドレスを指定することもできます。 このサーバーは、マニフェストの署名日時を示すタイムスタンプを提供します。

### <a name="to-sign-application-and-deployment-manifests-using-an-existing-key-file"></a>既存のキー ファイルを使用してアプリケーション マニフェストおよび配置マニフェストに署名するには

1. **[署名]** ページの **[ClickOnce マニフェストに署名する]** チェック ボックスをオンにします。

2. **[ファイルから選択]** をクリックします。

     **[ファイルの選択]** ダイアログ ボックスが表示されます。

3. **[ファイルの選択]** ダイアログ ボックスで、使うキー ファイル (.pfx) の場所を参照し、 **[開く]** をクリックします。

    > [!NOTE]
    > このオプションは、拡張子 .pfx を持つファイルのみをサポートします。 これ以外の形式のキー ファイルや証明書がある場合は、Windows 証明書ストアに格納し、前の手順で説明した証明書を選択します。 選択した証明書の用途に、コードの署名が含まれている必要があります。

     **[ファイルを開くためのパスワードの入力]** ダイアログ ボックスが表示されます。 .pfx ファイルが既に Windows 証明書ストアに格納されている場合やパスワードで保護されていない場合、パスワードの入力は求められません。

4. キー ファイルにアクセスするためのパスワードを入力し、Enter キーを押します。

### <a name="to-sign-application-and-deployment-manifests-using-a-test-certificate"></a>テスト証明書を使用してアプリケーション マニフェストおよび配置マニフェストに署名するには

1. **[署名]** ページの **[ClickOnce マニフェストに署名する]** チェック ボックスをオンにします。

2. テスト用の新しい証明書を作成するには、 **[テスト証明書の作成]** をクリックします。

3. **[テスト証明書の作成]** ダイアログ ボックスで、テスト証明書をセキュアにするためにパスワードを入力します。

## <a name="generating-unsigned-manifests"></a>未署名のマニフェストの生成
 .exe ベースのアプリケーションでは、ClickOnce マニフェストの署名を省略できます。 次の手順は、未署名の ClickOnce マニフェストを生成する方法を示しています。

> [!IMPORTANT]
> 未署名のマニフェストにより、アプリケーションの開発およびテストを簡略化できます。 しかし、未署名のマニフェストは、稼動環境に重大なセキュリティ上の問題を発生させます。 インターネットまたは他の悪意のあるコードの提供元から完全に分離されたイントラネット内のコンピューターで ClickOnce アプリケーションを実行する場合のみ、未署名のマニフェストの使用を検討してください。

 既定では、ClickOnce は、生成されるハッシュから 1 つ以上のファイルが除外されるよう指定されていない限り、自動的に署名付きマニフェストを生成します。 つまり、すべてのファイルがハッシュに含まれ、 **[ClickOnce マニフェストに署名する]** チェック ボックスがオフの場合でも、アプリケーションの発行により署名付きマニフェストが生成されます。

#### <a name="to-generate-unsigned-manifests-and-include-all-files-in-the-generated-hash"></a>未署名マニフェストを生成し、生成されるハッシュにすべてのファイルを含めるには

1. ハッシュにすべてのファイルが含まれる未署名マニフェストを生成するには、まず署名付きマニフェストと共にアプリケーションを発行する必要があります。 したがって、前のいずれかの手順に従って ClickOnce マニフェストに署名してから、アプリケーションを発行します。

2. **[署名]** ページの **[ClickOnce マニフェストに署名する]** チェック ボックスをオフにします。

3. アプリケーションの 1 つのバージョンのみ使用できるように発行バージョンをリセットします。 既定では、アプリケーションを発行するたびに発行バージョンのリビジョン番号が自動的にインクリメントされます。 詳しくは、「[方法: ClickOnce の発行バージョンを設定する](../deployment/how-to-set-the-clickonce-publish-version.md)」をご覧ください。

4. アプリケーションを発行します。

#### <a name="to-generate-unsigned-manifests-and-exclude-one-or-more-files-from-the-generated-hash"></a>未署名マニフェストを生成し、生成されるハッシュから 1 つ以上のファイルを除外するには

1. **[署名]** ページの **[ClickOnce マニフェストに署名する]** チェック ボックスをオフにします。

2. **[アプリケーション ファイル]** ダイアログ ボックスを開き、生成されるハッシュから除外するファイルに対して **[ハッシュ]** を **[除外]** に設定します。

    > [!NOTE]
    > ハッシュからファイルを除外すると、ClickOnce によるマニフェストの自動署名が無効になるため、前の手順のように、最初に署名付きマニフェストで発行する必要がありません。

3. アプリケーションを発行します。

## <a name="see-also"></a>参照
 [厳密な名前付きアセンブリ](https://msdn.microsoft.com/library/d4a80263-f3e0-4d81-9b61-f0cbeae3797b)[方法: 公開キーと秘密キーのペアの](https://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114)[署名ページを作成する (プロジェクトデザイナー](../ide/reference/signing-page-project-designer.md) [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md))
