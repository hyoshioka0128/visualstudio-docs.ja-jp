---
title: .mdf ファイルのアップグレード
description: 新しいバージョンの Visual Studio をインストールした後に、データベースファイル (.mdf) をアップグレードするためのオプションを確認します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- SQL Server Express
- SQL Server LocalDB
- LocalDB
- SQLEXPRESS
- upgrading SQLExpress to SQLExpress
- upgrading to LocalDB
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: cbea7761ed5f36265464f2afe9a64550ddc5e62a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866308"
---
# <a name="upgrade-mdf-files"></a>.mdf ファイルのアップグレード

このトピックでは、新しいバージョンの Visual Studio をインストールした後で、データベースファイル (*.mdf*) をアップグレードするためのオプションについて説明します。 これには、次のタスクの手順が含まれます。

- 新しいバージョンの SQL Server Express LocalDB を使用するようにデータベースファイルをアップグレードする

- 新しいバージョンの SQL Server Express を使用するようにデータベースファイルをアップグレードする

- Visual Studio でデータベースファイルを操作するが、古いバージョンの SQL Server Express または LocalDB との互換性を維持する

- 既定のデータベースエンジン SQL Server Express にする

Visual Studio を使用して、古いバージョンの SQL Server Express または LocalDB を使用して作成されたデータベースファイル (*.mdf*) を含むプロジェクトを開くことができます。 ただし、Visual Studio でプロジェクトの開発を続行するには、Visual Studio と同じコンピューターにそのバージョンの SQL Server Express または LocalDB がインストールされている必要があります。または、データベースファイルをアップグレードする必要があります。 データベースファイルをアップグレードしても、以前のバージョンの SQL Server Express または LocalDB を使用してアクセスすることはできません。

また、ファイルのバージョンが現在インストールされている SQL Server Express または LocalDB のインスタンスと互換性がない場合は、以前のバージョンの SQL Server Express または LocalDB を使用して作成されたデータベースファイルをアップグレードするように求められることもあります。 この問題を解決するには、Visual Studio でファイルをアップグレードするように求められます。

> [!IMPORTANT]
> アップグレードする前に、データベースファイルをバックアップすることをお勧めします。

> [!WARNING]
> Localdb 2014 (V12) 32 ビットで作成された *.mdf* ファイルを localdb 2016 (V13) 以降にアップグレードした場合、そのファイルを、32ビットバージョンの localdb で再び開くことはできません。

データベースをアップグレードする前に、次の条件を考慮してください。

- 以前のバージョンと新しいバージョンの Visual Studio の両方でプロジェクトを操作する場合は、アップグレードしないでください。

- アプリケーションが LocalDB ではなく SQL Server Express を使用する環境で使用される場合は、アップグレードしないでください。

- アプリケーションがリモート接続を使用している場合は、LocalDB ではそれを受け付けないため、アップグレードしないでください。

- アプリケーションがインターネットインフォメーションサービス (IIS) に依存している場合は、アップグレードしないでください。

- サンドボックス環境でデータベースアプリケーションをテストするが、データベースを管理しない場合は、アップグレードを検討してください。

### <a name="to-upgrade-a-database-file-to-use-the-localdb-version"></a>LocalDB バージョンを使用するようにデータベースファイルをアップグレードするには

1. **サーバーエクスプローラー** で、[**データベースへの接続**] ボタンをクリックします。

2. [ **接続の追加** ] ダイアログボックスで、次の情報を指定します。

    - **データソース**: `Microsoft SQL Server (SqlClient)`

    - **サーバー名**:

        - 既定のバージョンを使用する場合は `(localdb)\MSSQLLocalDB` 。  これにより、インストールされている Visual Studio のバージョンと最初の LocalDB インスタンスが作成された日時に応じて、ProjectV12 または ProjectV13 のいずれかが指定されます。 **SQL Server オブジェクトエクスプローラー** の [ **MSSQLLocalDB** ノードには、ポイントしているバージョンが表示されます。

        - 特定のバージョンを使用する場合: `(localdb)\ProjectsV12` または `(localdb)\ProjectsV13` (V12 が localdb 2014、V13 が localdb 2016 の場合)。

    - **データベースファイルのアタッチ**: プライマリ *.mdf* ファイルの物理パス。

    - 論理名(&L):ファイルで使用する名前です。

3. **[OK]**  ボタンを選択します。

4. メッセージが表示されたら、[ **はい** ] をクリックしてファイルをアップグレードします。

    データベースがアップグレードされ、LocalDB データベースエンジンにアタッチされており、以前のバージョンの LocalDB と互換性がなくなりました。

また、接続のショートカットメニューを開き、[ **接続の変更**] を選択して、LocalDB を使用するように SQL Server Express 接続を変更することもできます。 [ **接続の変更** ] ダイアログボックスで、サーバー名をに変更し `(LocalDB)\MSSQLLocalDB` ます。 **[詳細プロパティ**] ダイアログボックスで、[**ユーザーインスタンス**] が [ **False**] に設定されていることを確認します。

### <a name="to-upgrade-a-database-file-to-use-the-sql-server-express-version"></a>SQL Server Express のバージョンを使用するようにデータベースファイルをアップグレードするには

1. データベースへの接続のショートカットメニューで、[ **接続の変更**] を選択します。

2. [ **接続の変更** ] ダイアログボックスで、[ **詳細設定** ] をクリックします。

3. **[詳細プロパティ**] ダイアログボックスで、サーバー名を変更せずに **[OK** ] をクリックします。

    データベースファイルは、現在のバージョンの SQL Server Express と一致するようにアップグレードされます。

### <a name="to-work-with-the-database-in-visual-studio-but-retain-compatibility-with-sql-server-express"></a>Visual Studio でデータベースを操作するが、SQL Server Express との互換性を維持するには

- Visual Studio で、アップグレードせずにプロジェクトを開きます。

  - プロジェクトを実行するには、 **F5** キーを押します。

  - データベースを編集するには、**ソリューションエクスプローラー** で *.mdf* ファイルを開き、**サーバーエクスプローラー** のノードを展開してデータベースを操作します。

### <a name="to-make-sql-server-express-the-default-database-engine"></a>既定のデータベースエンジンを SQL Server Express するには

1. メニュー バーで、 **[ツール]**  >  **[オプション]** の順に選択します。

2. [ **オプション** ] ダイアログボックスで、[ **データベースツール** ] オプションを展開し、[ **データ接続**] を選択します。

3. [ **SQL Server インスタンス名** ] テキストボックスに、使用する SQL Server Express または LocalDB のインスタンスの名前を指定します。 インスタンスに名前が付けられていない場合は、を指定し `.\SQLEXPRESS or (LocalDB)\MSSQLLocalDB` ます。

4. **[OK]**  ボタンを選択します。

    SQL Server Express は、アプリケーションの既定のデータベースエンジンになります。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのアクセス](accessing-data-in-visual-studio.md)
