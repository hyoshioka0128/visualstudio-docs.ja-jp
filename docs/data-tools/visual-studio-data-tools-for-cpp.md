---
title: C++ 用のデータ ツール
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85281098"
---
# <a name="visual-studio-data-tools-for-c"></a>C++ 用の Visual Studio データ ツール

データ ソースへのアクセスには、しばしばネイティブ C++ が最速です。 ただし、C++ アプリケーション用の Visual Studio のデータ ツールは、.Net アプリケーション用ほど充実していません。 たとえば、 **[データ ソース]** ウィンドウを使用し、C++ のデザイン サーフェイスにデータソースをドラッグ アンド ドロップできません。 オブジェクト リレーショナル レイヤーが必要な場合は、自分で記述するか、サードパーティ製品を使用する必要があります。 これはデータ バインディング機能にも当てはまります。ただし、Microsoft Foundation Class ライブラリを使用するアプリケーションでは、データをメモリに格納してそれをユーザーに表示する一部のデータベース クラスをドキュメントやビューで使用できます。 詳細については、「[Visual C++ でのデータ アクセス](/cpp/data/data-access-in-cpp)」を参照してください。

ネイティブ C++ アプリケーションで SQL データベースに接続する場合、Windows に含まれる ODBC ドライバーおよび OLE DB ドライバーと、ADO プロバイダーを使用できます。 これらは、これらのインターフェイスがサポートされているすべてのデータベースに接続できます。 標準は ODBC ドライバーです。 OLE DB は下位互換性のために用意されています。 これらのデータ テクノロジの詳細については、[Windows Data Access Components](/previous-versions/windows/desktop/ms692897(v=vs.85)) に関するページを参照してください。

SQL Server 2005 以降のカスタム機能を利用する場合は、[SQL Server Native Client](/sql/relational-databases/native-client/sql-server-native-client) を使用します。 このネイティブ クライアントの 1 つの DLL (ダイナミックリンク ライブラリ) には、SQL Server ODBC ドライバーと SQL Server OLE DB プロバイダーも含まれています。 これらにより、ネイティブ コード API (ODBC、OLE DB、および ADO) で Microsoft SQL Server に接続するアプリケーションがサポートされます。 SQL Server Native Client は、SQL Server Data Tools と共にインストールされます。 これのプログラミング ガイドは、「[SQL Server Native Client プログラミング](/sql/relational-databases/native-client/sql-server-native-client-programming)」です。

## <a name="to-connect-to-localdb-through-odbc-and-sql-native-client-from-a-c-application"></a>C++ アプリケーションから localDB に ODBC と SQL Native Client で接続するには

1. SQL Server Data Tools をインストールします。

2. 接続するサンプルの SQL データベースが必要な場合は、Northwind のデータベースをダウンロードし、それを新しい場所に解凍します。

3. SQL Server Management Studio を使用して、解凍した *Northwind.mdf* ファイルを localDB にアタッチします。 SQL Server Management Studio が起動されたら、(localdb)\MSSQLLocalDB に接続します。

   ![SSMS の接続ダイアログ](../data-tools/media/raddata-ssms-connect-dialog.png)

   次に、左側のウィンドウの localdb ノードを右クリックし、 **[アタッチ]** を選択します。

   ![SSMS でのデータベースのアタッチ](../data-tools/media/raddata-ssms-attach-database.png)

4. ODBC Windows SDK サンプルをダウンロードし、それを新しい場所に解凍します。 このサンプルには、データベースに接続し、クエリとコマンドを発行するための ODBC の基本コマンドがあります。 これらの機能の詳細については、[Microsoft Open Database Connectivity (ODBC)](/sql/odbc/microsoft-open-database-connectivity-odbc) に関するページを参照してください。 (C++ フォルダー内の) ソリューションを最初に読み込む際に、ソリューションを Visual Studio の現在のバージョンにアップグレードするか Visual Studio により尋ねられます。 **[はい]** をクリックします。

5. ネイティブ クライアントを使用する場合には、それの "*ヘッダー*" ファイルと "*ライブラリ*" ファイルが必要です。 これらのファイルには、sql.h に定義されている ODBC 関数以外の SQL Server に固有の関数と定義が含まれています。 **[プロジェクト]**  >  **[プロパティ]**  >  **[VC++ ディレクトリ]** で、次のインクルード ディレクトリを追加します。

   **%ProgramFiles%\Microsoft SQL Server\110\SDK\Include**

   このライブラリ ディレクトリもです。

   **%ProgramFiles%\Microsoft SQL Server\110\SDK\Lib**

6. これらの行を *odbcsql.cpp* に追加します。 #define により、無関係の OLE DB 定義はコンパイルされません。

   ```cpp
   #define _SQLNCLI_ODBC_
   #include <sqlncli.h>
   ```

    なお、このサンプルでは、実際のネイティブ クライアント機能はいずれも使用されないので、上記の手順はコンパイルと実行には不要です。 しかし、プロジェクトはこれでこの機能を使用できるように構成されました。 詳細については、「[SQL Server Native Client プログラミング](/sql/relational-databases/native-client/sql-server-native-client)」を参照してください。

7. ODBC サブシステムで使用するドライバーを指定します。 サンプルにより、コマンドライン引数として、DRIVER 接続文字列属性が渡されます。 **[プロジェクト]**  >  **[プロパティ]**  >  **[デバッグ]** で、次のコマンド引数を追加します。

   ```cpp
   DRIVER="SQL Server Native Client 11.0"
   ```

8. **F5** キーを押してアプリケーションをビルドし、実行します。 ドライバーにより、データベースの入力を求めるダイアログ ボックスが表示されます。 「`(localdb)\MSSQLLocalDB`」と入力し、 **[セキュリティ接続を使用する]** を確認します。 **[OK]** を押します。 コンソールに接続の成功を示すメッセージが表示されます。 SQL ステートメントを入力できるコマンド プロンプトも表示されます。 次の画面は、クエリの例と結果を示しています。

   ![ODBC サンプル クエリの出力](../data-tools/media/raddata-odbc-sample-query-output.png)

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
