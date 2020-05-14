---
title: '方法: アプリケーション マニフェストと配置マニフェストの署名'
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
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
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fbf25301095ac5ff438514c37f61337e46342860
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75596165"
---
# <a name="how-to-sign-application-and-deployment-manifests"></a>方法: アプリケーション マニフェストと配置マニフェストの署名

ClickOnce 配置を使用してアプリケーションを発行しようとする場合は、アプリケーション マニフェストと配置マニフェストに、公開キーと秘密キーのペアを使用して署名し、さらに Authenticode テクノロジを使用して署名する必要があります。 これらのマニフェストには、Windows 証明書ストアの証明書またはキー ファイルを使用して署名できます。

ClickOnce 配置の詳細については、「[ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)」を参照してください。

*.exe* ベースのアプリケーションでは、ClickOnce マニフェストの署名を省略できます。 詳細については、このドキュメントの「未署名のマニフェストの生成」セクションを参照してください。

キー ファイルの作成については、「[方法 : 公開キーと秘密キーのキー ペアを作成する](/dotnet/framework/app-domains/how-to-create-a-public-private-key-pair)」を参照してください。

> [!NOTE]
> Visual Studio では、拡張子 *.pfx* を持つ Personal Information Exchange (PFX) キー ファイルだけがサポートされます。 ただし、プロジェクトのプロパティの **[署名]** ページにある **[ストアから選択]** をクリックすると、現在のユーザーの Windows 証明書ストアから、他の種類の証明書を選ぶことができます。

## <a name="sign-using-a-certificate"></a>証明書を使用して署名する

1. プロジェクトのプロパティ ウィンドウに移動します (**ソリューション エクスプローラー**でプロジェクト ノードを右クリックし、 **[プロパティ]** を選択します)。 **[署名]** タブの **[ClickOnce マニフェストに署名する]** チェック ボックスをオンにします。

2. **[ストアから選択]** をクリックします。

     **[証明書の選択]** ダイアログ ボックスが表示され、Windows 証明書ストアの内容が表示されます。

    > [!TIP]
    > **[証明書のプロパティを表示します]** をクリックすると、 **[証明書の詳細]** ダイアログ ボックスが表示されます。 このダイアログ ボックスには、証明書と追加オプションの詳細情報があります。 **[証明書]** をクリックすると、追加のヘルプ情報を表示することができます。

3. マニフェストの署名に使用する証明書を選択します。

4. また、 **[タイムスタンプ サーバーの URL]** ボックスでタイムスタンプ サーバーのアドレスを指定することもできます。 このサーバーは、マニフェストの署名日時を示すタイムスタンプを提供します。

## <a name="sign-using-an-existing-key-file"></a>既存のキー ファイルを使用して署名する

1. **[署名]** ページの **[ClickOnce マニフェストに署名する]** チェック ボックスをオンにします。

2. **[ファイルから選択]** をクリックします。

     **[ファイルの選択]** ダイアログ ボックスが表示されます。

3. **[ファイルの選択]** ダイアログ ボックスで、使用するキー ファイル ( *.pfx*) の場所を参照し、 **[開く]** をクリックします。

    > [!NOTE]
    > このオプションでは、拡張子 *.pfx* を持つファイルのみがサポートされます。 これ以外の形式のキー ファイルや証明書がある場合は、Windows 証明書ストアに格納し、前の手順で説明した証明書を選択します。 選択した証明書の用途に、コードの署名が含まれている必要があります。

     **[ファイルを開くためのパスワードの入力]** ダイアログ ボックスが表示されます。 ( *.pfx* ファイルが既に Windows 証明書ストアに格納されている場合やパスワードで保護されていない場合、パスワードの入力は求められません。)

4. キー ファイルにアクセスするパスワードを入力し、**Enter** キーを選択します。

> [!NOTE]
> *.pfx* ファイルには証明書チェーンの情報を含めることはできません。 含まれる場合は、次のインポート エラーが発生します。**暗号化の解除のための証明書と秘密キーが見つかりません**。 証明書チェーンの情報を削除するには、*Certmgr.msc*を使用して、*.pfx ファイルをエクスポートするときに**すべての証明書を含める**ための[オプションを無効にする](/previous-versions/aa730868(v=vs.80))ことができます。

## <a name="sign-using-a-test-certificate"></a>テスト証明書を使用して署名する

1. **[署名]** ページの **[ClickOnce マニフェストに署名する]** チェック ボックスをオンにします。

2. テスト用の新しい証明書を作成するには、 **[テスト証明書の作成]** をクリックします。

3. **[テスト証明書の作成]** ダイアログ ボックスで、テスト証明書をセキュアにするためにパスワードを入力します。

## <a name="generate-unsigned-manifests"></a>未署名のマニフェストの生成

*.exe* ベースのアプリケーションでは、ClickOnce マニフェストの署名を省略できます。 次の手順は、未署名の ClickOnce マニフェストを生成する方法を示しています。

> [!IMPORTANT]
> 未署名のマニフェストにより、アプリケーションの開発およびテストを簡略化できます。 しかし、未署名のマニフェストは、稼動環境に重大なセキュリティ上の問題を発生させます。 インターネットまたは他の悪意のあるコードの提供元から完全に分離されたイントラネット内のコンピューターで ClickOnce アプリケーションを実行する場合のみ、未署名のマニフェストの使用を検討してください。

既定では、ClickOnce は、生成されるハッシュから 1 つ以上のファイルが除外されるよう指定されていない限り、自動的に署名付きマニフェストを生成します。 つまり、すべてのファイルがハッシュに含まれ、 **[ClickOnce マニフェストに署名する]** チェック ボックスがオフの場合でも、アプリケーションの発行により署名付きマニフェストが生成されます。

### <a name="to-generate-unsigned-manifests-and-include-all-files-in-the-generated-hash"></a>未署名マニフェストを生成し、生成されるハッシュにすべてのファイルを含めるには

1. ハッシュにすべてのファイルが含まれる未署名マニフェストを生成するには、まず署名付きマニフェストと共にアプリケーションを発行する必要があります。 したがって、前のいずれかの手順に従って ClickOnce マニフェストに署名してから、アプリケーションを発行します。

2. **[署名]** ページの **[ClickOnce マニフェストに署名する]** チェック ボックスをオフにします。

3. アプリケーションの 1 つのバージョンのみ使用できるように発行バージョンをリセットします。 既定では、アプリケーションを発行するたびに発行バージョンのリビジョン番号が自動的にインクリメントされます。 詳細については、[ClickOnce の発行バージョンを設定する](../deployment/how-to-set-the-clickonce-publish-version.md)」を参照してください。

4. アプリケーションを発行します。

### <a name="to-generate-unsigned-manifests-and-exclude-one-or-more-files-from-the-generated-hash"></a>未署名マニフェストを生成し、生成されるハッシュから 1 つ以上のファイルを除外するには

1. **[署名]** ページの **[ClickOnce マニフェストに署名する]** チェック ボックスをオフにします。

2. **[アプリケーション ファイル]** ダイアログ ボックスを開き、生成されるハッシュから除外するファイルに対して **[ハッシュ]** を **[除外]** に設定します。

    > [!NOTE]
    > ハッシュからファイルを除外すると、ClickOnce によるマニフェストの自動署名が無効になるため、前の手順のように、最初に署名付きマニフェストで発行する必要がありません。

3. アプリケーションを発行します。

## <a name="see-also"></a>関連項目

- [厳密な名前付きアセンブリ](/dotnet/framework/app-domains/strong-named-assemblies)
- [方法: 公開キーと秘密キーのキー ペアを作成する](/dotnet/framework/app-domains/how-to-create-a-public-private-key-pair)
- [[署名] ページ (プロジェクト デザイナー)](../ide/reference/signing-page-project-designer.md)
- [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)
