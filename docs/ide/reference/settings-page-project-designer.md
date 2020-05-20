---
title: '[設定] ページ (プロジェクト デザイナー)'
ms.date: 06/14/2018
ms.topic: reference
f1_keywords:
- ApplicationSettingsOverview
helpviewer_keywords:
- Settings page in Project Designer
- Project Designer, Settings page
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4f4ca1def334241999445e3f11cf142aa426d962
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75566775"
---
# <a name="settings-page-project-designer"></a>[設定] ページ (プロジェクト デザイナー)

プロジェクト デザイナーの **[設定]** ページを使用し、プロジェクトのアプリケーション設定を指定します。 アプリケーション設定を使用することで、アプリケーションのプロパティ設定やその他の情報を動的に格納し、取得できます。 また、クライアント コンピューターでカスタム アプリケーションとユーザー設定を維持できます。 詳細については、[アプリケーション設定の管理](../managing-application-settings-dotnet.md)に関するページを参照してください。

この [**設定**] ページにアクセスするには、**ソリューション エクスプローラー**でプロジェクト ノードを選択し、**[プロジェクト]**、**[プロパティ]** の順に選択します。 プロジェクト デザイナーが表示されたら、 **[設定]** タブを選択します。

## <a name="header-bar"></a>ヘッダー バー

**[設定]** ページの上部にあるヘッダー バーにはコントロールがいくつかあります。

**[同期]**

**同期**すると、実行時に、またはデバッグ中にアプリケーションで使用されるユーザー スコープ設定がデザイン時に定義された既定値に復元されます。 データを復元するには、実行時に生成されたアプリケーション固有のファイルをプロジェクト データではなく、ディスクから削除します。

**[Web 設定の読み込み]**

**Web 設定を読み込む**と、 **[ログイン]** ダイアログ ボックスが表示されます。このボックスで、認証済みユーザーや匿名ユーザーの設定を読み込むことができます。 このボタンは、 **[サービス]** ページでクライアント アプリケーション サービスを有効にし、**Web 設定サービスの場所**を指定している場合にのみ有効になります。

**[コードの表示]**

C# プロジェクトの場合、 **[コードの表示]** ボタンをクリックすると、*Settings.cs* ファイルのコードが表示されます。 このファイルでは、`Settings` クラスが定義されています。このクラスによって、`Settings` オブジェクトの特定のイベントを処理できます。 Visual Basic 以外の言語では、ユーザー設定を保持するためには、このラッパー クラスの `Save` メソッドを明示的に呼び出す必要があります。 これは、通常、メイン フォームの **Closing** イベント ハンドラーで行います。 `Save` メソッドの呼び出しの例を次に示します。

```csharp
Properties.Settings.Default.Save();
```

Visual Basic プロジェクトの場合、 **[コードの表示]** ボタンをクリックすると、*Settings.vb* ファイルのコードが表示されます。 このファイルでは、`MySettings` クラスが定義されています。このクラスによって、`My.Settings` オブジェクトの特定のイベントを処理できます。 `My.Settings` オブジェクトを使用してアプリケーション設定にアクセスする方法の詳細については、[アプリケーション設定にアクセスする](/dotnet/visual-basic/developing-apps/programming/app-settings/accessing-application-settings)方法に関するページを参照してください。

アプリケーション設定にアクセスする方法の詳細については、[Windows フォームのアプリケーション設定](/dotnet/framework/winforms/advanced/application-settings-for-windows-forms)に関するページを参照してください。

**アクセス修飾子**

**[アクセス修飾子]** ボタンでは、*Settings.Designer.cs* または *Settings.Designer.vb* で Visual Studio により生成される `Properties.Settings` (C#) または `My.Settings` (Visual Basic) ヘルパー クラスのアクセス レベルが指定されます。

Visual C# プロジェクトの場合、アクセス修飾子は **[内部]** か **[パブリック]** になります。

Visual Basic プロジェクトの場合、アクセス修飾子は **[フレンド]** か **[パブリック]** になります。

既定では、設定は C# の場合は **[内部]** 、Visual Basic の場合は **[フレンド]** になります。 Visual Studio が **[内部]** または **[フレンド]** としてヘルパー クラスを生成するとき、実行可能ファイル ( *.exe*) アプリケーションは、クラス ライブラリ ( *.dll* ファイル) に追加したリソースや設定にアクセスできません。 クラス ライブラリからリソースや設定を共有する必要がある場合、アクセス修飾子を **[パブリック]** に設定します。

設定ヘルパー クラスに関する詳細については、[アプリケーション設定の管理](../managing-application-settings-dotnet.md)に関するページを参照してください。

## <a name="settings-grid"></a>設定グリッド

**設定グリッド**は、アプリケーション設定の構成に使用されます。 このグリッドには次の列があります。

**Name**

このフィールドにアプリケーション設定の名前を入力します。

**Type**

ドロップダウン リストを使用し、設定の種類を選択します。 **[文字列]** 、 **[(接続文字列)]** 、 **[System.Drawing.Font]** など、最も頻繁に使用される種類がドロップダウン リストに表示されます。 一覧の最後にある **[参照]** を選択し、 **[種類の選択]** ダイアログ ボックスから種類を選択して別の種類を選択できます。 種類を選択すると、ドロップダウン リストの共通の種類にその種類が追加されます (現在のソリューションのみ)。

**スコープ**

**[アプリケーション]** または **[ユーザー]** を選択します。

接続文字列など、アプリケーション スコープ設定はアプリケーションに関連付けられます。 ユーザーは実行時にアプリケーション スコープ設定を変更できません。

システム フォントなど、ユーザー スコープ設定はユーザー設定に使用することが意図されています。 ユーザーは実行時にユーザー スコープ設定を変更できます。

**[値]**

アプリケーション設定に関連付けられているデータまたは値。 たとえば、設定がフォントの場合、その値には「**Verdana, 9.75pt, style=Bold**」などが想定されます。

## <a name="see-also"></a>関連項目

- [アプリケーション設定の管理](../managing-application-settings-dotnet.md)
- [アプリケーション設定へのアクセス (Visual Basic)](/dotnet/visual-basic/developing-apps/programming/app-settings/accessing-application-settings)
