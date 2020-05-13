---
title: プロジェクトタイプ設計の決定 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, project file persistence
- project types, commitment mechanics
- project types, items
- project types, design decisions
ms.assetid: f68671fe-fd7a-4e56-a0b5-330b0f1fedb1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5e33ac1c4168593b881f799dfdfb94005fb55fc1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706373"
---
# <a name="project-type-design-decisions"></a>プロジェクト タイプのデザインの方針
新しいプロジェクトタイプを作成する前に、プロジェクトタイプに関していくつかの設計決定を行う必要があります。 プロジェクトに含める項目の種類、プロジェクト ファイルの永続化方法、使用するコミットメント モデルを決定する必要があります。

## <a name="project-items"></a>プロジェクト アイテム
 プロジェクトでファイルまたは抽象オブジェクトを使用しますか? ファイルを使用する場合、参照ベースまたはディレクトリベースのファイルになりますか? ファイルまたは抽象オブジェクトはローカルかリモートか。

 プロジェクト内の項目は、ファイルにすることも、データベース リポジトリ内のオブジェクトやインターネット上のデータ接続などのより抽象的なオブジェクトにすることもできます。 項目がファイルの場合、プロジェクトは参照ベースまたはディレクトリベースのプロジェクトのいずれかになります。

 参照ベースのプロジェクトでは、複数のプロジェクトに項目を表示できます。 ただし、アイテムが表す実際のファイルは、1 つのディレクトリにのみ配置されます。 ディレクトリベースのプロジェクトでは、すべてのプロジェクト項目がディレクトリ構造に存在します。

 ローカル項目は、アプリケーションがインストールされているコンピューターに格納されます。 リモートアイテムは、ローカルネットワークの別のサーバーに保存することも、インターネット上の他の場所に保存することもできます。

## <a name="project-file-persistence"></a>プロジェクト ファイルの永続性
 データは共通のフラット・ファイル・システムに格納されるか、構造化ストレージに格納されるか。 標準エディタまたはプロジェクト固有のエディタを使用してファイルを開く

 ほとんどのアプリケーションでは、データを保存するためにデータをファイルに保存し、ユーザーが情報を確認または変更する必要があるときにデータを読み取ります。

 構造化ストレージは、複合ファイルとも呼ばれ、複数のコンポーネント オブジェクト モデル (COM) オブジェクトが 1 つのファイルに保存する必要がある場合に通常使用されます。 構造化ストレージでは、複数の異なるソフトウェア コンポーネントで 1 つのディスク ファイルを共有できます。

 プロジェクト内の項目の永続性について考慮するオプションがいくつかあります。 次のいずれかのオプションを実行できます。

- 変更後、各ファイルを個別に保存します。

- 1 回の**保存**操作で多数のトランザクションをキャプチャします。

- ファイルをローカルに保存してからサーバーに発行するか、または項目がリモート オブジェクトへのデータ接続を表す場合は、プロジェクト アイテムを保存する別の方法を使用します。

  永続性の詳細については、「[プロジェクトの永続性](../../extensibility/internals/project-persistence.md)」および「[プロジェクト項目を開いて保存](../../extensibility/internals/opening-and-saving-project-items.md)する 」を参照してください。

## <a name="project-commitment-model"></a>プロジェクトコミットメントモデル
 永続化されたデータ オブジェクトは、直接モードまたはトランザクション モードで開かれますか?

 データ オブジェクトを直接モードで開くと、データに加えられた変更は、すぐに反映されるか、またはユーザーがファイルを手動で保存したときに反映されます。

 トランザクション モードを使用してデータ オブジェクトを開くと、変更はメモリ内の一時的な場所に保存され、ユーザーが手動でファイルの保存を選択するまでコミットされません。 その時点で、すべての変更が一緒に行われるか、変更は行われません。

## <a name="see-also"></a>関連項目
- [チェック リスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [プロジェクト項目のオープンと保存](../../extensibility/internals/opening-and-saving-project-items.md)
- [プロジェクトの永続化](../../extensibility/internals/project-persistence.md)
- [プロジェクト モデルの要素](../../extensibility/internals/elements-of-a-project-model.md)
- [プロジェクト モデルのコア コンポーネント](../../extensibility/internals/project-model-core-components.md)
- [プロジェクト タイプの作成](../../extensibility/internals/creating-project-types.md)
