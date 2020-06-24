---
title: C++ 用データツール
ms.date: 11/04/2016
ms.topic: overview
dev_langs:
- CPP
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
- cplusplus
ms.openlocfilehash: 063efeebff92698b8e5db66880360713c73fe150
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281098"
---
# <a name="visual-studio-data-tools-for-c"></a>C++ 用の Visual Studio データ ツール

多くの場合、ネイティブ C++ では、データソースにアクセスするときのパフォーマンスが最速になります。 ただし、Visual Studio の C++ アプリケーション用のデータツールは、.NET アプリケーションの場合と同様に豊富ではありません。 たとえば、[**データソース**] ウィンドウを使用して、データソースを C++ デザインサーフェイスにドラッグアンドドロップすることはできません。 オブジェクトリレーショナルレイヤーが必要な場合は、独自のものを作成するか、サードパーティ製品を使用する必要があります。 これはデータバインディング機能にも当てはまりますが、Microsoft Foundation Class ライブラリを使用するアプリケーションでは、一部のデータベースクラスをドキュメントやビューと共に使用して、データをメモリに格納し、ユーザーに表示することができます。 詳細については、「 [Visual C++ でのデータアクセス](/cpp/data/data-access-in-cpp)」を参照してください。

SQL データベースに接続するには、ネイティブ C++ アプリケーションで、Windows に含まれている ODBC および OLE DB ドライバーと ADO プロバイダーを使用できます。 これらのインターフェイスをサポートする任意のデータベースに接続できます。 ODBC ドライバーは標準です。 OLE DB は、旧バージョンとの互換性のために用意されています。 これらのデータテクノロジの詳細については、「 [Windows Data Access Components](/previous-versions/windows/desktop/ms692897(v=vs.85))」を参照してください。

SQL Server 2005 以降のカスタム機能を利用するには、 [SQL Server native client](/sql/relational-databases/native-client/sql-server-native-client)を使用します。 Native client には、1つのネイティブダイナミックリンクライブラリ (DLL) に SQL Server ODBC ドライバーと SQL Server OLE DB プロバイダーも含まれています。 これらは、ネイティブコード Api (ODBC、OLE DB、ADO) を使用して Microsoft SQL Server するアプリケーションをサポートします。 SQL Server Native Client SQL Server Data Tools と共にインストールされます。 プログラミングガイドについては、「 [SQL Server native client プログラミング](/sql/relational-databases/native-client/sql-server-native-client-programming)」を参照してください。

## <a name="to-connect-to-localdb-through-odbc-and-sql-native-client-from-a-c-application"></a>ODBC を使用して localDB に接続し、C++ アプリケーションから SQL Native Client するには

1. SQL Server Data Tools をインストールします。

2. 接続するサンプルの SQL データベースが必要な場合は、Northwind データベースをダウンロードし、新しい場所に解凍します。

3. SQL Server Management Studio を使用して、解凍した*Northwind .mdf*ファイルを localDB にアタッチします。 SQL Server Management Studio が開始されたら、(localdb) \MSSQLLocalDB. に接続します。

   ![SSMS の接続ダイアログ](../data-tools/media/raddata-ssms-connect-dialog.png)

   次に、左側のウィンドウで localdb ノードを右クリックし、[**アタッチ**] を選択します。

   ![SSMS のデータベースのアタッチ](../data-tools/media/raddata-ssms-attach-database.png)

4. ODBC Windows SDK サンプルをダウンロードし、新しい場所に解凍します。 このサンプルでは、データベースへの接続とクエリとコマンドの実行に使用される基本的な ODBC コマンドを示します。 これらの関数の詳細については、 [Microsoft Open Database Connectivity (ODBC)](/sql/odbc/microsoft-open-database-connectivity-odbc)を参照してください。 ソリューションを初めて読み込むと (C++ フォルダー内にあります)、Visual Studio はソリューションを現在のバージョンの Visual Studio にアップグレードすることを提供します。 **[はい]** をクリックします。

5. Native client を使用するには、その*ヘッダー*ファイルと*lib*ファイルが必要です。 これらのファイルには、SQL .h で定義されている ODBC 関数以外の SQL Server に固有の関数と定義が含まれています。 [**プロジェクト**の  >  **プロパティ**  >  ] [**VC + + ディレクトリ**] で、次のインクルードディレクトリを追加します。

   **%ProgramFiles%\Microsoft SQL Server\110\SDK\Include**

   このライブラリディレクトリは次のようになります。

   **%ProgramFiles%\Microsoft SQL Server\110\SDK\Lib**

6. これらの行を*odbcsql .cpp*に追加します。 #Define によって、無関係の OLE DB 定義がコンパイルされるのを防ぐことができます。

   ```cpp
   #define _SQLNCLI_ODBC_
   #include <sqlncli.h>
   ```

    このサンプルでは、実際には native client の機能を使用していないので、コンパイルして実行するために上記の手順は必要ありません。 しかし、この機能を使用できるようにプロジェクトが構成されました。 詳細については、「 [SQL Server Native Client プログラミング](/sql/relational-databases/native-client/sql-server-native-client)」を参照してください。

7. ODBC サブシステムで使用するドライバーを指定します。 このサンプルでは、のドライバー接続文字列属性をコマンドライン引数として渡します。 [**プロジェクト**のプロパティ] [  >  **Properties**  >  **デバッグ**] で、次のコマンド引数を追加します。

   ```cpp
   DRIVER="SQL Server Native Client 11.0"
   ```

8. **F5** キーを押してアプリケーションをビルドし、実行します。 ドライバーから、データベースを入力するように求めるダイアログボックスが表示されます。 `(localdb)\MSSQLLocalDB`「」と入力し、[**信頼できる接続を使用する**] をオンにします。 **[OK]** を押します。 接続が成功したことを示すメッセージが表示されたコンソールが表示されます。 SQL ステートメントを入力できるコマンドプロンプトも表示されます。 次の画面は、クエリの例と結果を示しています。

   ![ODBC サンプルクエリの出力](../data-tools/media/raddata-odbc-sample-query-output.png)

## <a name="see-also"></a>こちらもご覧ください

- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
