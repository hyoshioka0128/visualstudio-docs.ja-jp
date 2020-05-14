---
title: プロジェクトタイプを作成する場合 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, conditions for creating
ms.assetid: 26adc860-ee4a-4f5c-95e1-e41b207dd7e6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 861250dac25288f353cbd5c57f510bf67dadce70
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703432"
---
# <a name="when-to-create-project-types"></a>プロジェクト タイプを作成する状況
新しいプロジェクトタイプを作成すると、ユーザーをカスタマイズ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]するための基礎となります。 ただし、すべての[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]カスタマイズに新しいプロジェクトタイプを作成する必要はありません。 次のガイドラインは、シナリオに新しいプロジェクトの種類が必要かどうかを判断するのに役立ちます。

## <a name="create-a-new-project-type"></a>新しいプロジェクトタイプの作成
 次の 1 つ以上の方法で動作[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]するようにカスタマイズする場合は、プロジェクトの種類を作成する必要があります。

- ビルド、配置、構成、およびソース管理に参加します。

- デバッグサポートを提供します。

- **ソリューション エクスプローラ**にプロジェクト項目を表示する 。

- [**プロジェクトを開く**] ダイアログ ボックスまたは **[新しいプロジェクト**] ダイアログ ボックスを使用します。

- プロジェクトの入れ子をサポートします。

## <a name="extend-an-existing-project-type"></a>既存のプロジェクトの種類を拡張する
 プロジェクトのビルド プロセスの変更など、既存のプロジェクト[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]の種類の動作を変更または拡張するために、次の方法で使用できる新しいプロジェクトの種類を[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]作成できます。

- 複数のファイルを 1 つの単位として扱います。

- 1 つのファイルをサブ項目の階層として表示します。

- エディターの周囲にコマンド コンテキストを表示します。

- エディターのサービス コンテキストを表示します。

## <a name="use-an-existing-project-type"></a>既存のプロジェクトの種類を使用する
 新しいプロジェクトを作成する必要がない場合があります。 次の表は、プロジェクトの種類を作成する必要がないタスクを示しています。

|タスク|説明|
|----------|-----------------|
|コマンドの処理|どの VSPackage もコマンドを処理できます。|
|エディタの作成|カスタムエディターを登録できます。 詳細については、「[ドキュメント ウィンドウとエディター](https://msdn.microsoft.com/library/603625e1-62b6-413a-bc44-089346e166bc)」を参照してください。|
|ウィンドウの所有|新しいプロジェクト タイプを追加しなくても、ツール ウィンドウとドキュメント ウィンドウの両方を作成できます。|
|プロパティ ウィンドウでプロパティを公開する|すべてのオブジェクトがプロパティを公開できます。|

## <a name="create-a-project-subtype"></a>プロジェクト サブタイプの作成
 プロジェクトのサブタイプを使用すると、新しいプロジェクトタイプを作成しなくても、管理プロジェクトタイプを拡張できます。 プロジェクト のサブタイプは COM 集約を使用して[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]、Microsoft または[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]で記述されたマネージ プロジェクトを拡張します。 COM 集約を使用すると、マネージ プロジェクト システムの実装の大部分を再利用でき、集約とサポート インターフェイスの使用を通じて特定のシナリオに合わせてカスタマイズできます。 プロジェクト のサブタイプの詳細については、「[プロジェクト のサブタイプ](../../extensibility/internals/project-subtypes.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ドキュメント ウィンドウとエディター](https://msdn.microsoft.com/library/603625e1-62b6-413a-bc44-089346e166bc)
- [チェック リスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [Visual Studio での階層](../../extensibility/internals/hierarchies-in-visual-studio.md)
