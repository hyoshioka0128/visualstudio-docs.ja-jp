---
title: '[デバッグ] ページ (プロジェクト デザイナー) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesDebug
helpviewer_keywords:
- Project Designer, Debug page
- Debug page in Project Designer
ms.assetid: ef11eae9-df96-4e20-aabd-2678ba317140
caps.latest.revision: 37
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 006662d7c07ba0498fff4617eca3fdc7c631d37b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660786"
---
# <a name="debug-page-project-designer"></a>[デバッグ] ページ (プロジェクト デザイナー)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!WARNING]
> このトピックは Windows ストア アプリには適用されません。 Windows デベロッパー センターの「[デバッグ セッションの開始 (VB、C#、C++、および XAML)](../../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md)」を参照してください。

 Visual Basic または C# プロジェクトのデバッグ動作のプロパティを設定するには、**プロジェクト デザイナー**の **[デバッグ]** ページを使用します。

 **[デバッグ]** ページにアクセスするには、**ソリューション エクスプローラー**でプロジェクト ノードを選択します。 **[プロジェクト]** メニューの _[プロジェクト名_**プロパティ]** を選択します。 **プロジェクト デザイナー**が表示されたら、 **[デバッグ]** タブをクリックします。

## <a name="configuration-and-platform"></a>構成およびプラットフォーム
 次のオプションを使用すると、表示または変更する構成およびプラットフォームを選択できます。

 **[構成]** 表示または変更する構成設定を指定します。 設定は、 **[デバッグ]** (既定)、 **[リリース]** 、または **[すべての構成]** のいずれかになります。 詳細については、「[デバッグ構成およびリリース プロジェクト構成](https://msdn.microsoft.com/0440b300-0614-4511-901a-105b771b236e)」を参照してください。

 **[プラットフォーム]** 表示または変更するプラットフォーム設定を指定します。 **[Any CPU]** (既定)、 **[x64]** 、および **[x86]** から選択できます。 詳細については、「[デバッグ構成およびリリース プロジェクト構成](https://msdn.microsoft.com/0440b300-0614-4511-901a-105b771b236e)」を参照してください。

## <a name="start-action"></a>[開始動作]
 **[開始動作]** は、アプリケーションをデバッグするときに開始するアイテムを示します。プロジェクト、カスタム プログラム、URL のいずれかを指定できます。また、省略することもできます。 既定では、このオプションは **[プロジェクトの開始]** に設定されます。 **[デバッグ]** ページの **[開始動作]** 設定で、`StartAction` プロパティの値が決まります。

 **プロジェクトの開始**アプリケーションのデバッグ時に実行可能ファイル (Windows アプリケーションとコンソールアプリケーションプロジェクトの場合) を開始するように指定するには、このオプションを選択します。 既定では、このオプションはオンです。

 **外部プログラムの開始**アプリケーションのデバッグ時に特定のプログラムを起動するように指定するには、このオプションを選択します。

 **URL を使用してブラウザーを起動**するアプリケーションのデバッグ時に特定の URL にアクセスするように指定するには、このオプションを選択します。

## <a name="start-options"></a>開始オプション
 **コマンドライン引数**このテキストボックスに、デバッグに使用するコマンドライン引数を入力します。

 **作業ディレクトリ**このテキストボックスに、プロジェクトの起動に使用するディレクトリを入力します。 または参照ボタン ( **[...]** ) をクリックしてディレクトリを選択します。

 **リモートコンピューターを使用する**リモートコンピューターからアプリケーションをデバッグするには、このチェックボックスをオンにし、テキストボックスにリモートコンピューターのパスを入力します。

## <a name="enable-debuggers"></a>デバッガーを有効にする
 **アンマネージコードのデバッグを有効にする**このオプションは、ネイティブコードのデバッグがサポートされているかどうかを指定します。 COM オブジェクトを呼び出すか、プロジェクトを呼び出すネイティブ コードで記述されたカスタム プログラムを起動して、ネイティブ コードをデバッグする必要がある場合はこのチェック ボックスをオンにします。 アンマネージ コードのデバッグを無効にする場合は、このチェック ボックスをオフにします。 既定では、このチェック ボックスはオフです。

 **SQL Server のデバッグを有効にする**Visual Basic アプリケーションからの SQL プロシージャのデバッグを有効または無効にするには、このチェックボックスをオンまたはオフにします。 既定では、このチェック ボックスはオフです。

 **Visual Studio のホストプロセスを有効にする**Visual Studio ホスティングプロセスを有効にするには、このチェックボックスをオンにします。 既定では、このチェック ボックスはオンです。 詳細については、「[ホスト プロセス (vshost.exe)](../../ide/hosting-process-vshost-exe.md)」を参照してください。

 セキュリティ ゾーンでデバッグするには、このオプションと、[[セキュリティの詳細設定] ダイアログ ボックス](../../ide/reference/advanced-security-settings-dialog-box.md)の **[選択されたアクセス許可セットでこのアプリケーションをデバッグする]** を有効にする必要があります。

## <a name="see-also"></a>参照
 [Visual Studio でのデバッグ](../../debugger/debugging-in-visual-studio.md)[デバッグ構成C#の](../../debugger/project-settings-for-csharp-debug-configurations.md)プロジェクト設定[Visual Basic デバッグ構成のプロジェクト設定](../../debugger/project-settings-for-a-visual-basic-debug-configuration.md)[デバッグプロパティの管理](https://msdn.microsoft.com/92474d16-e7fe-4fac-9287-6bd6b3a7eb68)[方法: ClickOnce アプリケーションのデバッグ方法アクセス許可の制限](../../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)[方法: 構成を作成および編集する](../../ide/how-to-create-and-edit-configurations.md)
