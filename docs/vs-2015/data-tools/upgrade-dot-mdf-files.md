---
title: .Mdf ファイルをアップグレードします。Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- SQL Server Express
- SQL Server LocalDB
- LocalDB
- SQLEXPRESS
- upgrading SQLExpress to SQLExpress
- upgrading to LocalDB
ms.assetid: 14ca6f76-f80e-4926-8020-3fee2d802b75
caps.latest.revision: 36
author: jillre
ms.author: jillfra
manager: jillfra
robots: noindex,nofollow
ms.openlocfilehash: 5b26b8cd9d955309e3be0e17e975bfdeb242e475
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72621403"
---
# <a name="upgrade-mdf-files"></a>.mdf ファイルのアップグレード
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、新しいバージョンの Visual Studio をインストールした後に、データベースファイル (.mdf) をアップグレードするためのオプションについて説明します。 これには、次のタスクの手順が含まれます。

- 新しいバージョンの SQL Server Express LocalDB を使用するようにデータベースファイルをアップグレードする

- 新しいバージョンの SQL Server Express を使用するようにデータベースファイルをアップグレードする

- Visual Studio でデータベースファイルを操作するが、古いバージョンの SQL Server Express または LocalDB との互換性を維持する

- 既定のデータベースエンジン SQL Server Express にする

  Visual Studio を使用して、古いバージョンの SQL Server Express または LocalDB を使用して作成されたデータベースファイル (.mdf) を含むプロジェクトを開くことができます。 ただし、Visual Studio でプロジェクトの開発を続行するには、Visual Studio と同じコンピューターにそのバージョンの SQL Server Express または LocalDB がインストールされている必要があります。または、データベースファイルをアップグレードする必要があります。 データベースファイルをアップグレードしても、以前のバージョンの SQL Server Express または LocalDB を使用してアクセスすることはできません。

  また、ファイルのバージョンが現在インストールされている SQL Server Express または LocalDB のインスタンスと互換性がない場合は、以前のバージョンの SQL Server Express または LocalDB を使用して作成されたデータベースファイルをアップグレードするように求められることもあります。 この問題を解決するには、Visual Studio でファイルをアップグレードするように求められます。

> [!IMPORTANT]
> アップグレードする前に、データベースファイルをバックアップすることをお勧めします。

> [!WARNING]
> LocalDB 2014 (V12) 32 ビットで作成された .mdf ファイルを LocalDB 2016 (V13) にアップグレードすると、そのファイルを、32ビット版の LocalDB で再び開くことができなくなります。  Update 2 では、LocalDB V13 は64ビットのみです。

 データベースをアップグレードする前に、次の条件を考慮してください。

- 以前のバージョンと新しいバージョンの Visual Studio の両方でプロジェクトを操作する場合は、アップグレードしないでください。

- アプリケーションが LocalDB ではなく SQL Server Express を使用する環境で使用される場合は、アップグレードしないでください。

- アプリケーションがリモート接続を使用している場合は、LocalDB ではそれを受け付けないため、アップグレードしないでください。

- アプリケーションがインターネットインフォメーションサービス (IIS) に依存している場合は、アップグレードしないでください。

- サンドボックス環境でデータベースアプリケーションをテストするが、データベースを管理しない場合は、アップグレードを検討してください。

### <a name="to-upgrade-a-database-file"></a>データベースファイルをアップグレードするには

1. **サーバーエクスプローラー**で、[**データベースへの接続**] ボタンをクリックします。

2. [ **接続の追加** ] ダイアログボックスで、次の情報を指定します。

   - **データソース**: `Microsoft SQL Server (SqlClient)`

   - **サーバー名**:

       - 既定のバージョンを使用する場合は `(localdb)\MSSQLLocalDB` 。  これにより、インストールされている Visual Studio のバージョンと最初の LocalDB インスタンスが作成された日時に応じて、ProjectV12 または ProjectV13 のいずれかが指定されます。 **SQL Server オブジェクトエクスプローラー**の [ **MSSQLLocalDB**ノードには、ポイントしているバージョンが表示されます。

       - 特定のバージョンを使用する場合: `(localdb)\ProjectsV12` または `(localdb)\ProjectsV13` (V12 が localdb 2014、V13 が localdb 2016 の場合)。

   - **データベースファイルのアタッチ**: プライマリ .mdf ファイルの物理パス。

   - 論理名(&L):ファイルで使用する名前です****。

3. **[OK]** ボタンを選択します。

4. メッセージが表示されたら、[ **はい** ] をクリックしてファイルをアップグレードします。

   データベースがアップグレードされ、LocalDB データベースエンジンにアタッチされており、以前のバージョンの LocalDB と互換性がなくなりました。

   また、接続のショートカットメニューを開き、[ **接続の変更**] を選択して、LocalDB を使用するように SQL Server Express 接続を変更することもできます。 [ **接続の変更** ] ダイアログボックスで、サーバー名をに変更し `(LocalDB)\MSSQLLocalDB` ます。 **[詳細プロパティ**] ダイアログボックスで、[**ユーザーインスタンス**] が [ **False**] に設定されていることを確認します。

### <a name="to-upgrade-to-a-newer-version-of-sql-server-express"></a>新しいバージョンの SQL Server Express にアップグレードするには

1. データベースへの接続のショートカットメニューで、[ **接続の変更**] を選択します。

2. [ **接続の変更** ] ダイアログボックスで、[ **詳細設定** ] をクリックします。

3. **[詳細プロパティ**] ダイアログボックスで、サーバー名を変更せずに **[OK** ] をクリックします。

   データベースファイルは、現在のバージョンの SQL Server Express と一致するようにアップグレードされます。

### <a name="to-work-with-the-database-in-visual-studio-but-retain-compatibility-with-sql-server-express"></a>Visual Studio でデータベースを操作するが、SQL Server Express との互換性を維持するには

- Visual Studio で、アップグレードせずにプロジェクトを開きます。

  - プロジェクトを実行するには、F5 キーを押します。

  - データベースを編集するには、 **ソリューションエクスプローラー**で .mdf ファイルを開き、 **サーバーエクスプローラー** のノードを展開してデータベースを操作します。

### <a name="to-make-sql-server-express-the-default-database-engine"></a>既定のデータベースエンジンを SQL Server Express するには

1. メニュー バーで、**[ツール]** > **[オプション]** の順に選択します。

2. [ **オプション** ] ダイアログボックスで、[ **データツール** ] オプションを展開し、[ **データ接続** ] ノードを選択します。

3. [ **SQL Server インスタンス名** ] テキストボックスに、使用する SQL Server Express または LocalDB のインスタンスの名前を指定します。 インスタンスに名前が付けられていない場合は、を指定し `.\SQLEXPRESS or (localdb)\MSSQLLocalDB` ます。

4. **[OK]** ボタンを選択します。

   SQL Server Express は、アプリケーションの既定のデータベースエンジンになります。
