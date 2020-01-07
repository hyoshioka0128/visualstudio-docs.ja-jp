---
title: CodeIndex コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- command-line tools [Team Foundation Server]
- TFSConfig
- CodeIndex command [Team Foundation Server]
ms.assetid: b79568d4-6a64-4ca9-a1ee-3e57f92a9c5c
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 070106dc4db0f5200c1346bbbf8c0b653aa104e5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72619678"
---
# <a name="codeindex-command"></a>CodeIndex コマンド
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**CodeIndex** コマンドを使用して、Team Foundation Server でコード インデックス作成を管理します。 たとえば、インデックスをリセットして CodeLens 情報を修正したり、コード インデックス作成をオフにしてサーバー パフォーマンスの問題を調査したりします。

 **必要なアクセス許可**

 **CodeIndex** コマンドを使用するには、**Team Foundation 管理者**セキュリティ グループのメンバーである必要があります。 「[Team Foundation Server のアクセス許可の参照](https://msdn.microsoft.com/library/39997de5-b7fb-4777-b779-07de0543abe6)」を参照してください。

> [!NOTE]
> 管理資格情報を使ってログオンしている場合でも、このコマンドを実行するには、昇格した特権でコマンド プロンプト ウィンドウを開く必要があります。 また、Team Foundation のアプリケーション層からこのコマンドを実行する必要があります。

## <a name="syntax"></a>構文

```
TFSConfig CodeIndex /indexingStatus | /setIndexing:[ on | off | keepupOnly ] | /ignoreList:[ add | remove | removeAll | view ] ServerPath | /listLargeFiles [/fileCount:FileCount] [/minSize:MinSize] | /reindexAll | /destroyCodeIndex [/noPrompt] | /temporaryDataSizeLimit:[ view | <SizeInGBs> | disable ] | /indexHistoryPeriod:[ view | all | <NumberOfMonths> ] [/collectionName:CollectionName | /collectionId:CollectionId]
```

#### <a name="parameters"></a>パラメーター

|**引数**|**説明**|
|------------------|---------------------|
|`CollectionName`|チーム プロジェクト コレクションの名前を指定します。 名前に空白が含まれる場合は、"Fabrikam Web Site" のように引用符で囲みます。|
|`CollectionId`|チーム プロジェクト コレクションの ID 番号を指定します。|
|`ServerPath`|コード ファイルのパスを指定します。|

|**オプション**|**説明**|
|----------------|---------------------|
|**/indexingStatus**|コード インデックス作成サービスの状態と構成を表示します。|
|**/setIndexing:** [ on &#124; off &#124; keepupOnly ]|-   **on**: すべての変更セットのインデックス作成を開始します。<br />-   **off**: すべての変更セットのインデックス作成を停止します。<br />-   **keepupOnly**: 以前に作成された変更セットのインデックス作成を停止し、新しい変更セットのインデックス作成のみを開始します。|
|**/ignoreList:** [ add &#124; remove &#124; removeAll &#124; view ] `ServerPath`<br /><br /> ワイルドカード文字 (*) を、サーバー パスの先頭、末尾、または両端に使用できます。|インデックスを作成しないコード ファイルとそのパスの一覧を指定します。<br /><br /> -   **add**: インデックスを作成しないファイルを無視ファイル リストに追加します。<br />-   **remove**: インデックスを作成するファイルを無視ファイル リストから削除します。<br />-   **removeAll**: 無視ファイル リストをクリアし、すべてのファイルのインデックス作成を開始します。<br />-   **view**: インデックスを作成しないすべてのファイルを表示します。|
|**/listLargeFiles [/fileCount:** `FileCount` **/minSize:** `MinSize`]|KB 単位で指定されたサイズを超えるファイルを指定された数だけ表示します。 その後で、 **/ignoreList** オプションを使用して、これらのファイルをインデックス作成から除外することができます。|
|**/reindexAll**|以前にインデックスを作成したデータをクリアし、インデックス作成を再び開始します。|
|**/destroyCodeIndex [/noPrompt]**|コード インデックスを削除し、すべてのインデックス データを削除します。 **/noPrompt** のオプションを使用する場合は、確認を要求されません。|
|**/temporaryDataSizeLimit**:[ view &#124; <`SizeInGBs`> &#124; disable ]|変更セットを処理するときに CodeLens が作成する一時データの量を制御します。 制限の既定値は 2 GB です。<br /><br /> -   **view**: 現在のサイズ制限を表示します。<br />-   `SizeInGBs`: サイズの制限を変更します。<br />-   **disable**: サイズの制限を削除します。<br /><br /> CodeLens が新しい変更セットを処理する前に、この制限の検査が行われます。 一時データがこの制限を超える場合、CodeLens は過去の変更セット (新しい変更セットではない) の処理を一時停止します。 データがクリーンアップされ、この制限内に収まると、CodeLens は処理を再開します。 クリーンアップは 1 日に 1 度、自動的に行われます。 このことは、クリーンアップの実行が始まるまでは、一時データがこの制限を超えている可能性があることを意味します。|
|**/indexHistoryPeriod**:[ view &#124; all &#124; <`NumberOfMonths`> ]|変更履歴のインデックスを作成する期間を制御します。 これは、CodeLens の履歴の表示量に影響します。 制限の既定値は 12 か月です。 つまり、CodeLens が過去 12 か月間の変更履歴のみを表示するという意味です。<br /><br /> -   **view**: 現在の月数を表示します。<br />-   **all**: すべての変更履歴のインデックスを作成します。<br />-   `NumberOfMonths`: 変更履歴のインデックスの作成に使用する月数を変更します。|
|**/collectionName:** `CollectionName`|**CodeIndex** コマンドを実行する対象のチーム プロジェクト コレクションの名前を指定します。 **/CollectionId** を使用しない場合は必ず指定します。|
|**/collectionId:** `CollectionId`|**CodeIndex** コマンドを実行する対象のチーム プロジェクト コレクションの ID 番号を指定します。 **/CollectionName** を使用しない場合は必ず指定します。|

## <a name="examples"></a>使用例

> [!NOTE]
> 例として登場する企業、組織、製品、ドメイン名、電子メール アドレス、ロゴ、人物、場所、およびイベントはすべて架空のものです。  実在する会社、組織、製品、ドメイン名、電子メールアドレス、ロゴ、人物、場所、イベントなどとは一切関係ありません。

 コード インデックス作成の状態と構成を表示するには:

```
TFSConfig CodeIndex /indexingStatus /collectionName:"Fabrikam Web Site"
```

 すべての変更セットのインデックス作成を開始するには:

```
TFSConfig CodeIndex /setIndexing:on /collectionName:"Fabrikam Web Site"
```

 以前に作成された変更セットのインデックス作成を停止し、新しい変更セットのインデックス作成のみを開始するには:

```
TFSConfig CodeIndex /setIndexing:keepupOnly /collectionName:"Fabrikam Web Site"
```

 10 KB を超えるファイルを最大 50 個検索するには:

```
TFSConfig CodeIndex /listLargeFiles /fileCount:50 /minSize:10 /collectionName:"Fabrikam Web Site"
```

 特定のファイルをインデックス作成から除外し、無視ファイル リストに追加するには:

```
TFSConfig CodeIndex /ignoreList:add "$/Fabrikam Web Site/Catalog.cs" /collectionName:"Fabrikam Web Site"
```

 インデックスを作成しないすべてのファイルを表示するには:

```
TFSConfig CodeIndex /ignoreList:view
```

 以前にインデックスを作成したデータをクリアし、インデックス作成を再び開始するには:

```
TFSConfig CodeIndex /reindexAll /collectionName:"Fabrikam Web Site"
```

 すべての変更履歴を保存するには:

```
TFSConfig CodeIndex /indexHistoryPeriod:all /collectionName:"Fabrikam Web Site"
```

 CodeLens 一時データのサイズ制限を取り払い、一時データのサイズに関係なくインデックス作成を続けるには:

```
TFSConfig CodeIndex /temporaryDataSizeLimit:disable /collectionName:"Fabrikam Web Site"
```

 確認後にコード インデックスを削除するには:

```
TFSConfig CodeIndex /destroyCodeIndex /collectionName:"Fabrikam Web Site"
```

## <a name="see-also"></a>関連項目
 TFSConfig[コマンドラインツール](https://msdn.microsoft.com/be8c997a-b97b-4e59-97f5-04db0a601a6c)を使用した TFS の[サーバー構成の管理](https://msdn.microsoft.com/94424190-3b6b-4f33-a6b6-5807f4225b62)
