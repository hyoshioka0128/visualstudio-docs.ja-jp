---
title: ユースケースをドキュメントおよび図にリンクする |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.teamarch.usecasediagram.artifact.properties.artifactlink
- vs.teamarch.usecasediagram.artifact
helpviewer_keywords:
- use case diagrams
ms.assetid: 4c9ed205-9197-4ed5-b39d-ddfa24a0a421
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c713759a8ea75eed3048469327f962668efa4f70
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657640"
---
# <a name="link-a-use-case-to-documents-and-diagrams"></a>ユース ケースをドキュメントおよび図にリンクする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ユース ケース図のユース ケースを、別の図またはドキュメントにリンクできます。 たとえば、ユース ケースを次の図やドキュメントにリンクできます。

- ユーザーと、システムまたはその主要なコンポーネント間の相互作用によって、ユース ケースの目標をどのように実現するかを示すシーケンス図。

- ユース ケース実行時に、ユーザー、システム、またはシステムの主要コンポーネントの詳細なアクションを示すアクティビティ図。

- ユース ケースを詳細に記述する OneNote のページまたは段落。

- ユース ケースを詳細に記述する Word 文書または PowerPoint プレゼンテーション。 このようなドキュメントは、ソリューション内、またはチームがアクセスできる場所 (SharePoint サイト) のいずれかで保持できます。

  ユース ケースをドキュメントにリンクするには、ユース ケース図で成果物を作成し、ユース ケースをその成果物に接続します。 成果物のプロパティで、その他の図またはドキュメントのファイル パスを設定します。 成果物をダブルクリックすると、その他の図またはドキュメントが開きます。

  各ユース ケースには、必要な数の成果物を接続することができます。 またユース ケース図では、成果物を他の種類の要素にリンクすることもできます。

### <a name="to-open-a-document-associated-with-an-artifact"></a>成果物に関連付けられているドキュメントを開くには

- ユース ケース図で、成果物の図形をダブルクリックします。

     関連するドキュメントが開きます。

### <a name="to-link-a-use-case-to-a-diagram-or-file-in-the-same-solution"></a>ユース ケースを、同じソリューション内の図またはファイルにリンクするには

1. シーケンス図やアクティビィティ図を描画して、ユース ケースのシナリオを例示します。

2. ユース ケース図に戻ります。

3. 図またはファイルを、ソリューション エクスプローラーからユース ケース図の空白部分にドラッグします。

4. **依存関係**を使用して、成果物からユースケースに接続します。

### <a name="to-link-to-a-solution-file-such-as-a-word-document-or-powerpoint-presentation"></a>Word 文書や PowerPoint プレゼンテーションなどのソリューション ファイルにリンクするには

1. このドキュメントをソリューションに追加します。

    1. Word 文書をソリューションとして、同じ Windows フォルダーに移動します。

    2. ソリューションエクスプローラーで、ソリューションを右クリックして [ **追加**] をポイントし、[ **既存の項目**] をクリックします。

    3. Word 文書に移動し、[ **追加**] をクリックします。

         ソリューション エクスプローラーのソリューション フォルダーに、Word 文書が表示されます。

2. Word 文書を、ソリューション エクスプローラーからユース ケース図の空白部分にドラッグします。

     新しい成果物が表示されます。

3. **依存関係**を使用して、成果物からユースケースに接続します。

### <a name="to-link-to-a-shared-document-onenote-element-or-web-page"></a>共有ドキュメント、OneNote 要素、または Web ページにリンクを設定するには

1. 共有要素の URL を取得します。 たとえば、"" を開始するネットワークファイルパス、" \\ \\ http://" を開始する web ページまたは Sharepoint URL、または onenote セクション、ページ、または "onenote:" を開始する段落へのリンクなどです。

2. [ツールボックス] で [ **アーティファクト** ] をクリックし、ユースケース図をクリックします。

3. 新しい成果物が選択された状態で、 **Hyperlink** プロパティに URL を入力するか貼り付けます。

    > [!NOTE]
    > ファイルパスを指定する場合は、(' ' で始まる) 共通のワークスペース \\ \\ または Visual Studio ソリューション内のファイルのいずれかでファイルを選択することをお勧めします。 これにより、ソリューションが移動された場合でも、ファイル パスは別のチーム メンバーのコンピューター上で有効なままになります。 Word 文書などのドキュメントをソリューションに追加するには、ソリューションエクスプローラーでソリューションを右クリックし、[ **追加** ] をポイントして、[ **既存の項目**] をクリックします。

## <a name="see-also"></a>参照
 [Uml ユースケース図: リファレンス](../modeling/uml-use-case-diagrams-reference.md) [Uml ユースケース図: ガイドライン](../modeling/uml-use-case-diagrams-guidelines.md)[編集 uml モデルおよび図](../modeling/edit-uml-models-and-diagrams.md)[アプリのモデルの作成](../modeling/create-models-for-your-app.md)
