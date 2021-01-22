---
title: '[デバッグ] ページ (プロジェクト デザイナー)'
description: プロジェクト デザイナーの [デバッグ] ページを使用して、Visual Basic または C# プロジェクトのデバッグ プロパティを設定します。 設定の説明についてはこの記事を参照してください。
ms.custom: SEO-VS-2020
ms.date: 06/27/2018
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesDebug
helpviewer_keywords:
- Project Designer, Debug page
- Debug page in Project Designer
ms.assetid: ef11eae9-df96-4e20-aabd-2678ba317140
author: Mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8567b762e9858205e3ca8d6aafa8a3dba17a90fe
ms.sourcegitcommit: a436ba564717b992eb1984b28ea0aec801eacaec
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98205776"
---
# <a name="debug-page-project-designer"></a>[デバッグ] ページ (プロジェクト デザイナー)

Visual Basic または C# プロジェクトのデバッグ動作のプロパティを設定するには、**プロジェクト デザイナー** の **[デバッグ]** ページを使用します。

**[デバッグ]** ページにアクセスするには、**ソリューション エクスプローラー** でプロジェクト ノードを選択します。 **[プロジェクト]** メニューの **[\<ProjectName> プロパティ]** を選択します。 **プロジェクト デザイナー** が表示されたら、 **[デバッグ]** タブをクリックします。

> [!NOTE]
> このトピックは UWP アプリには適用されません。 UWP アプリの[デバッグ セッションの開始 (VB、C#、C++、および XAML)](../../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md) に関するページを参照してください。

## <a name="configuration-and-platform"></a>構成およびプラットフォーム

次のオプションを使用すると、表示または変更する構成およびプラットフォームを選択できます。

**構成**

表示または変更する構成設定を指定します。 設定は、 **[デバッグ]** (既定)、 **[リリース]** 、または **[すべての構成]** のいずれかになります。

**プラットフォーム**

表示または変更するプラットフォーム設定を指定します。 **[Any CPU]** (既定)、 **[x64]** 、および **[x86]** から選択できます。

## <a name="start-action"></a>[開始動作]

**[開始動作]** は、アプリケーションをデバッグするときに開始するアイテムを示します。プロジェクト、カスタム プログラム、URL のいずれかを指定できます。また、省略することもできます。 既定では、このオプションは **[プロジェクトの開始]** に設定されます。 **[デバッグ]** ページの **[開始動作]** 設定で、`StartAction` プロパティの値が決まります。

**プロジェクトの開始**

アプリケーションのデバッグ時に、実行可能ファイル (Windows アプリケーションとコンソール アプリケーション プロジェクトの場合) を起動することを指定するには、このオプションを選択します。 既定では、このオプションはオンです。

**外部プログラムの開始**

アプリケーションのデバッグ時に特定のプログラムが起動されるように指定するには、このオプションを選択します。

**ブラウザーを開始時に使用する URL**

アプリケーションのデバッグ時に特定の URL にアクセスすることを指定するには、このオプションを選択します。

## <a name="start-options"></a>開始オプション

**コマンド ライン引数**

このテキスト ボックスには、デバッグに使用するコマンド ライン引数を入力します。

**作業ディレクトリ**

このテキスト ボックスには、プロジェクトの起動元のディレクトリを入力します。 または参照ボタン ( **[...]** ) をクリックしてディレクトリを選択します。

**リモート コンピューターの使用**

リモート コンピューターからアプリケーションをデバッグするには、このチェック ボックスをオンにし、テキスト ボックスにリモート コンピューターへのパスを入力します。

## <a name="debugger-engines"></a>デバッガー エンジン

**ネイティブ コードのデバッグを有効にする**

このオプションでは、ネイティブ コードのデバッグをサポートするかどうかを指定します。 COM オブジェクトを呼び出すか、プロジェクトを呼び出すネイティブ コードで記述されたカスタム プログラムを起動して、ネイティブ コードをデバッグする必要がある場合はこのチェック ボックスをオンにします。 アンマネージ コードのデバッグを無効にする場合は、このチェック ボックスをオフにします。 既定では、このチェック ボックスはオフです。

**SQL Server デバッグを有効にする**

Visual Basic アプリケーションから SQL プロシージャのデバッグを有効または無効にする場合は、このチェック ボックスをオンまたはオフにします。 既定では、このチェック ボックスはオフです。

## <a name="see-also"></a>関連項目

- [デバッガーでのはじめに](../../debugger/debugger-feature-tour.md)
- [C# デバッグ構成のプロジェクト設定](../../debugger/project-settings-for-csharp-debug-configurations.md)
- [Visual Basic デバッグ構成のプロジェクト設定](../../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [ClickOnce アプリをセキュリティで保護する](../../deployment/securing-clickonce-applications.md)
- [方法: 構成を作成および編集する](../../ide/how-to-create-and-edit-configurations.md)
