---
title: アプリケーションの設定の管理 (.NET) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- msvse_settingsdesigner.err.nameblank
helpviewer_keywords:
- application settings [Visual Studio]
ms.assetid: 35254321-ad14-47d9-b8c6-39ab3203c5d9
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 85cc90170b2dc665bcdd5acd97860c47ef5a14c4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "74293867"
---
# <a name="managing-application-settings-net"></a>アプリケーションの設定の管理 (.NET)

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

アプリケーション設定を使用すると、アプリケーション情報を動的に格納できます。 たとえば、アプリケーション コードに含まれないクライアント コンピューター情報 (接続文字列など)、ユーザー設定、および実行時に必要なその他の情報を格納できます。

アプリケーション設定は、以前のバージョンの Visual Studio で使用されていた動的プロパティに代わる機能です。

アプリケーション設定には、それぞれ一意の名前を付ける必要があります。 名前には、文字、数字、アンダースコアを自由に組み合わせて使用できますが、先頭には数字を使用できず、また、空白は使用できません。 名前は `Name` プロパティで変更できます。

アプリケーション設定は、XML にシリアル化できる任意のデータ型、または `TypeConverter` / `ToString`/`FromString`を持つ任意のデータ型として保存できます。 一般的な型は、 `String`、 `Integer`、および `Boolean`ですが、 <xref:System.Drawing.Color>、 <xref:System.Object>、または接続文字列として値を保存することもできます。

アプリケーション設定には、値も含まれます。 値は、 **値** プロパティで設定します。また、設定のデータ型と一致している必要があります。

さらに、デザイン時には、アプリケーション設定をフォームまたはコントロールのプロパティに関連付けることができます。

アプリケーション設定には、スコープによって次の 2 種類があります。

- アプリケーション スコープ設定は、Web サービスの URL やデータベース接続文字列などの情報に使用できます。 これらの値は、アプリケーションに関連付けられます。 したがって、ユーザーがこれらを実行時に変更することはできません。

- ユーザー スコープ設定は、終了時のフォームの位置やフォント設定などの情報の保持に使用できます。 ユーザーは実行時に値を変更できます。

  設定の種類は、 **スコープ** プロパティを使用して変更できます。

  プロジェクト システムは、アプリケーション設定を 2 つの XML ファイルに保存します。1 つは、デザイン時に最初のアプリケーション設定を作成したときに作成される app.config ファイルで、もう 1 つは、アプリケーションを実行するユーザーが実行時にユーザー設定の値を変更したときに作成される user.config ファイルです。 アプリケーションが明示的にメソッドを呼び出さない限り、ユーザー設定の変更はディスクに書き込まれないことに注意してください。

## <a name="creating-application-settings-at-design-time"></a>デザイン時におけるアプリケーション設定の作成

デザイン時にアプリケーションの設定を作成するには、 **プロジェクト デザイナー** の **[設定]** ページを使用するか、フォームやコントロールの **[プロパティ]** ウィンドウを使用します。後者では、プロパティに設定を直接関連付けることができます。

アプリケーション スコープ設定 (データベース接続文字列やサーバー リソースへの参照など) を作成した場合、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は、 `<applicationSettings>` タグを使用して app.config に設定を保存します。 接続文字列は、 `<connectionStrings>` タグの下に保存されます。

ユーザー スコープ設定 (既定のフォント、ホーム ページ、ウィンドウ サイズなど) を作成した場合、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は、 `<userSettings>` タグを使用して app.config に設定を保存します。

> [!IMPORTANT]
> 接続文字列を app.config に保存するときは、パスワードやサーバー パスなどの機密情報が接続文字列に表示されないように注意する必要があります。
>
> 接続文字列情報 (ユーザーが入力するユーザー ID やパスワードなど) を外部ソースから受け取った場合は、接続文字列の作成に使用する値に、接続の動作を変更してしまうような接続文字列パラメーターが含まれていないことを注意して確認する必要があります。
>
> 構成ファイル内の機密情報は、"保護された構成" 機能を使用して暗号化することを考慮してください。 詳細については、「[接続情報の保護](https://msdn.microsoft.com/library/1471f580-bcd4-4046-bdaf-d2541ecda2f4)」を参照してください。

> [!NOTE]
> クラス ライブラリには構成ファイル モデルが存在しないため、アプリケーション設定は、クラス ライブラリ プロジェクトでは使用できません。 ただし、Visual Studio Tools for Office DLL プロジェクトは例外で、構成ファイルを使用できます。

## <a name="using-customized-settings-files"></a>カスタマイズした設定ファイルの使用

カスタマイズした設定ファイルをプロジェクトに追加すると、設定をグループ化して管理できます。 1 つのファイルに含まれている設定は、1 つの単位として読み込まれ、保存されます。 したがって、頻繁に使用するグループと頻繁に使用されないグループとでは、設定を別々のファイルに格納できると、設定の読み込みと保存にかかる時間が短縮されます。

たとえば、SpecialSettings.settings という名前のファイルをプロジェクトに追加できます。 `SpecialSettings` クラスは `My` 名前空間に公開されませんが、 **[コードの表示]** では、 `Partial Class SpecialSettings`が格納されているカスタムの設定ファイルを読み込むことができます。

設定デザイナーは、プロジェクトシステムによって作成された設定の設定ファイルを最初に検索します。これは、プロジェクトデザイナーによって [**設定**] タブに表示される既定のファイルです。設定は、プロジェクトの [マイプロジェクト] フォルダー [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] およびプロジェクトの [プロパティ] フォルダーにあります。 [!INCLUDE[csprcs](../includes/csprcs-md.md)] プロジェクト デザイナーは、その次にプロジェクトのルート フォルダーで他の設定ファイルを検索します。 したがって、カスタム設定ファイルはここに置いておく必要があります。 プロジェクト内の他の場所に .settings ファイルを追加しても、プロジェクト デザイナーはそのファイルを見つけることができません。

## <a name="accessing-or-changing-application-settings-at-run-time-in-visual-basic"></a>実行時におけるアプリケーション設定へのアクセスまたは変更 (Visual Basic)

[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] プロジェクトでは、 `My.Settings` オブジェクトを使用することで、実行時にアプリケーション設定にアクセスできます。 **[設定]** ページの **[コードの表示]** ボタンをクリックして、Settings.vb ファイルを表示します。 Settings.vb は `Settings` クラスを定義し、 <xref:System.Configuration.ApplicationSettingsBase.SettingChanging>、 <xref:System.Configuration.ApplicationSettingsBase.PropertyChanged>、 <xref:System.Configuration.ApplicationSettingsBase.SettingsLoaded>、 <xref:System.Configuration.ApplicationSettingsBase.SettingsSaving>の各イベントを Settings クラスで処理できるようにします。 Settings.vb の `Settings` クラスは部分クラスであり、生成されたクラス全体ではなくユーザー所有コードだけが表示されることに注意してください。 `My.Settings` オブジェクトを使用したアプリケーション設定へのアクセスの詳細については、「[アプリケーション設定へのアクセス](https://msdn.microsoft.com/library/e38d0cc7-247a-46ca-ba04-f2913f0adb2e)」を参照してください。

ユーザーが実行時に変更するユーザー スコープ設定の値 (フォームの位置など) は、user.config ファイルに保存されます。 既定値は引き続き app.config に保存されていることに注意してください。

アプリケーションのテストなど、実行時にユーザー スコープ設定を変更した後で設定を既定値にリセットする場合は、 **[同期]** をクリックします。

設定へのアクセスには、 `My.Settings` オブジェクトおよび既定の .settings ファイルを使用することを強くお勧めします。 これは、設定デザイナーを使用して、プロパティを設定に割り当てることができ、さらにアプリケーションのシャットダウン前にユーザー設定が自動的に保存されるためです。 ただし、 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] アプリケーションから設定に直接アクセスすることもできます。 その場合は、 `MySettings` クラスにアクセスし、プロジェクトのルートにあるカスタムの .settings ファイルを使用する必要があります。 また、C# アプリケーションと同様、アプリケーションを終了する前にユーザー設定を保存する必要があります。この方法については、次のセクションで説明します。

<!-- markdownlint-disable MD003 MD020 -->
## <a name="accessing-or-changing-application-settings-at-run-time-in-visual-c"></a>実行時におけるアプリケーション設定へのアクセスまたは変更 (Visual C#)
<!-- markdownlint-enable MD003 MD020 -->

次の [!INCLUDE[csprcs](../includes/csprcs-md.md)] の例に示すように、[!INCLUDE[csprcs](../includes/csprcs-md.md)] などの [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 以外の言語では、`Settings` クラスに直接アクセスする必要があります。

```csharp
Properties.Settings.Default.FirstUserSetting = "abc";
```

ユーザー設定を保持するためには、このラッパー クラスの `Save` メソッドを明示的に呼び出す必要があります。 これは、通常、メイン フォームの `Closing` イベント ハンドラーで行います。 次の [!INCLUDE[csprcs](../includes/csprcs-md.md)] の例では、`Save` メソッドの呼び出しを示します。

```csharp
Properties.Settings.Default.Save();
```

`Settings` クラスを使用してアプリケーション設定にアクセスする方法の一般情報については、「[アプリケーション設定の概要](https://msdn.microsoft.com/library/0dd8bca5-a6bf-4ac4-8eec-5725d08b38dc)」を参照してください。 設定の反復処理については、この [フォーラム ポスト](https://social.msdn.microsoft.com/Forums/en-US/40fbb470-f1e8-4a02-a4a0-9f62b54d0fc4/is-this-possible-propertiessettingsdefault?forum=csharpgeneral)を参照してください。

## <a name="see-also"></a>参照

- [アプリケーション設定へのアクセス](https://msdn.microsoft.com/library/e38d0cc7-247a-46ca-ba04-f2913f0adb2e)
