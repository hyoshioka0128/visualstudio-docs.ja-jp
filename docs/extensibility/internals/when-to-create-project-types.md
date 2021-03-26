---
title: プロジェクトの種類を作成する場合 |Microsoft Docs
description: ユーザーのために Visual Studio をカスタマイズするために新しいプロジェクトの種類が必要かどうかを判断する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, conditions for creating
ms.assetid: 26adc860-ee4a-4f5c-95e1-e41b207dd7e6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 427c35a03f9d0cb11667ca9eaf88f144d018f620
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074302"
---
# <a name="when-to-create-project-types"></a>プロジェクト タイプを作成する状況
新しいプロジェクトの種類を作成すると、ユーザー向けにカスタマイズするための基礎と [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] なります。 ただし、すべてのカスタマイズに新しいプロジェクトの種類を作成する必要はありません [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 次のガイドラインは、シナリオに新しいプロジェクトの種類が必要かどうかを判断するのに役立ちます。

## <a name="create-a-new-project-type"></a>新しいプロジェクトの種類を作成する
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]次の1つまたは複数の方法で動作するようにをカスタマイズする場合は、プロジェクトの種類を作成する必要があります。

- ビルド、配置、構成、ソース管理に参加します。

- デバッグサポートを提供します。

- **ソリューションエクスプローラー** にプロジェクト項目を表示します。

- [ **プロジェクトを開く** ] または [ **新しいプロジェクト** ] ダイアログボックスを使用します。

- プロジェクトの入れ子をサポートします。

## <a name="extend-an-existing-project-type"></a>既存のプロジェクトの種類を拡張する
 次の方法でを使用して、プロジェクト [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のビルドプロセスを変更するなど、既存のプロジェクトの種類の動作を変更または拡張できる、新しいプロジェクトの種類を作成することができ [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] ます。

- 複数のファイルを1つの単位として操作します。

- サブ項目の階層として1つのファイルを表示します。

- エディターの周囲にコマンドコンテキストを表示します。

- エディターのサービスコンテキストを表示します。

## <a name="use-an-existing-project-type"></a>既存のプロジェクトの種類を使用する
 新しいプロジェクトを作成する必要はない場合があります。 次の表に、プロジェクトの種類を作成する必要がないタスクを示します。

|タスク|説明|
|----------|-----------------|
|コマンドの処理|VSPackage は、コマンドを処理できます。|
|エディターのビルド|カスタムエディターを登録できます。 詳細については、「 [ドキュメントウィンドウとエディター](/previous-versions/bb165691(v=vs.100))」を参照してください。|
|所有しているウィンドウ|新しいプロジェクトの種類を追加せずに、ツールウィンドウとドキュメントウィンドウの両方を作成できます。|
|プロパティウィンドウでのプロパティの公開|すべてのオブジェクトがプロパティを公開できます。|

## <a name="create-a-project-subtype"></a>プロジェクトのサブタイプを作成する
 プロジェクトのサブタイプを使用して、新しいプロジェクトの種類を作成することなく、マネージプロジェクトの種類を拡張することができます。 プロジェクトのサブタイプは、COM 集計を使用して、Microsoft またはで記述されたマネージプロジェクトを拡張し [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] ます。 COM 集計を使用すると、マネージプロジェクトシステムの実装の大部分を再利用しながら、集計やサポートインターフェイスを使用して特定のシナリオに合わせてカスタマイズできます。 プロジェクトのサブタイプの詳細については、「 [プロジェクトのサブタイプ](../../extensibility/internals/project-subtypes.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [ドキュメントウィンドウとエディター](/previous-versions/bb165691(v=vs.100))
- [チェックリスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [Visual Studio での階層](../../extensibility/internals/hierarchies-in-visual-studio.md)