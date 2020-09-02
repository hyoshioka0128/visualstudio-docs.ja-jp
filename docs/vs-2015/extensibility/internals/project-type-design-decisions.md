---
title: プロジェクトの種類の設計上の決定 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project types, project file persistence
- project types, commitment mechanics
- project types, items
- project types, design decisions
ms.assetid: f68671fe-fd7a-4e56-a0b5-330b0f1fedb1
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cd26e08ab153e96fc601e89788008cb0e9ca38c8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704079"
---
# <a name="project-type-design-decisions"></a>プロジェクト タイプのデザインの方針
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

新しいプロジェクトの種類を作成する前に、プロジェクトの種類に関するいくつかの設計上の決定を行う必要があります。 プロジェクトに含める項目の種類、プロジェクトファイルを永続化する方法、および使用するコミットメントモデルを決定する必要があります。  
  
## <a name="project-items"></a>プロジェクト アイテム  
 プロジェクトでファイルまたは抽象オブジェクトを使用しますか? ファイルを使用する場合、これらは参照ベースまたはディレクトリベースのファイルになりますか。 ファイルまたは抽象オブジェクトはローカルとリモートのどちらになりますか。  
  
 プロジェクト内の項目はファイルにすることも、データベースリポジトリ内のオブジェクトやインターネット経由のデータ接続など、より抽象的なオブジェクトにすることもできます。 項目がファイルの場合、プロジェクトは参照ベースまたはディレクトリベースのプロジェクトにすることができます。  
  
 参照ベースのプロジェクトでは、複数のプロジェクトに項目を表示できます。 ただし、項目が表す実際のファイルは、1つのディレクトリにのみ存在します。 ディレクトリベースのプロジェクトでは、すべてのプロジェクト項目がディレクトリ構造に存在します。 詳細については、「 [NIB: プロジェクトでの項目管理](https://msdn.microsoft.com/762e606b-7f44-4b66-97a1-e30a703654a0)」を参照してください。  
  
 ローカル項目は、アプリケーションがインストールされているのと同じコンピューターに格納されます。 リモート項目は、ローカルネットワーク内の別のサーバー、またはインターネット上の他の場所に格納できます。  
  
## <a name="project-file-persistence"></a>プロジェクトファイルの永続化  
 データは共通のフラットファイルシステムまたは構造化ストレージに格納されますか。 標準エディターまたはプロジェクト固有のエディターを使用してファイルを開きますか?  
  
 データを永続化するために、ほとんどのアプリケーションはデータをファイルに保存し、ユーザーが情報を確認または変更する必要があるときにそのデータを読み戻します。  
  
 構造化ストレージ (複合ファイルとも呼ばれます) は、通常、複数のコンポーネントオブジェクトモデル (COM) オブジェクトが、永続化されたデータを1つのファイルに格納する必要がある場合に使用します。 構造化ストレージでは、複数の異なるソフトウェアコンポーネントが1つのディスクファイルを共有できます。  
  
 プロジェクト内の項目の永続性に関して考慮する必要があるオプションがいくつかあります。 次のいずれかのオプションを実行できます。  
  
- 各ファイルが変更されたときに個別に保存します。  
  
- 複数のトランザクションを1回の **保存** 操作でキャプチャします。  
  
- ファイルをローカルに保存した後、サーバーに発行するか、アイテムがリモートオブジェクトへのデータ接続を表している場合は、別の方法を使用してプロジェクトアイテムを保存します。  
  
  永続化の詳細については、「 [プロジェクトの永続](../../extensibility/internals/project-persistence.md) 化」と「 [プロジェクト項目を開いて保存](../../extensibility/internals/opening-and-saving-project-items.md)する」を参照してください。  
  
## <a name="project-commitment-model"></a>プロジェクトコミットメントモデル  
 永続化されたデータオブジェクトは、直接モードまたはトランザクションモードで開くことができますか。  
  
 データオブジェクトが直接モードで開かれると、データに加えられた変更が直ちに、またはユーザーが手動でファイルを保存したときに反映されます。  
  
 トランザクションモードでデータオブジェクトを開くと、変更はメモリ内の一時的な場所に保存され、ユーザーが手動でファイルの保存を選択するまでコミットされません。 その時点で、すべての変更が同時に行われるか、変更は行われません。  
  
## <a name="see-also"></a>参照  
 [チェックリスト: 新しいプロジェクトの種類の作成](../../extensibility/internals/checklist-creating-new-project-types.md)   
 [NIB: プロジェクトでの項目管理](https://msdn.microsoft.com/762e606b-7f44-4b66-97a1-e30a703654a0)   
 [プロジェクト項目を開いて保存する](../../extensibility/internals/opening-and-saving-project-items.md)   
 [プロジェクトの永続化](../../extensibility/internals/project-persistence.md)   
 [プロジェクトモデルの要素](../../extensibility/internals/elements-of-a-project-model.md)   
 [プロジェクトモデルコアコンポーネント](../../extensibility/internals/project-model-core-components.md)   
 [プロジェクト タイプの作成](../../extensibility/internals/creating-project-types.md)
