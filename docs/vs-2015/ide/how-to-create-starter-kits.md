---
title: '方法 : スタート キットを作成する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Starter Kits, creating
ms.assetid: ed7d1844-7c01-424a-a831-5003efe0f7bc
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f9df8d85c600cd383a9a9059e689e6cb9f232d8f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668038"
---
# <a name="how-to-create-starter-kits"></a>方法 : スタート キットを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

スタート キットには、アプリケーションを変更または展開する方法を示す、完成したアプリケーションのコードとドキュメントが含まれています。 スタート キットの作成は、基本的には通常のプロジェクト テンプレートの作成と同じです。ただし、スタート キットにはドキュメント ファイルが含まれており、スタート キットを基にしてプロジェクトを作成するときに開くように設定されている点が異なります。

## <a name="designing-and-developing-a-starter-kit"></a>スタート キットの設計と開発
 まず、開発するスタート キットの種類を特定し、対象ユーザーを定義します。 次に、目的に応じてプロジェクトおよびドキュメントを設計します。

 サンプル アプリケーションまたはプラグインを作成する場合は、以下を実行します。

- ビルド エラーが発生しないプロジェクトを作成します。

- テンプレート コードを追加して、追加タスクを実装します (省略可能)。

- ドキュメントを準備します。

  学習ツールを作成する場合は、以下を実行します。

- ビルド エラーが発生しないプロジェクトを作成します。

- コード スニペットや項目テンプレートなどのリソースを整理します。

- ドキュメントを準備します。

## <a name="creating-a-template"></a>テンプレートの作成
 プロジェクトとドキュメントが完成したら、スタート キット用のプロジェクト テンプレートを作成できます。 このプロセスは、プロジェクト テンプレートの作成とまったく同じです。

 次のトピックには、テンプレートの作成に関する情報が含まれます。

 [方法: プロジェクトテンプレートを作成](../ide/how-to-create-project-templates.md)するテンプレートの**エクスポート**ウィザードを使用してテンプレートを作成する方法について説明します。

 [方法: 既存のテンプレートを更新する](../ide/how-to-update-existing-templates.md)エクスポートされたテンプレートを編集する方法について説明します。 この手順を使用して .vstemplate ファイルを変更し、スタート キットをカスタマイズします。

## <a name="see-also"></a>参照
 [プロジェクトと項目テンプレートの作成テンプレートの](../ide/creating-project-and-item-templates.md)[カスタマイズ](../ide/customizing-project-and-item-templates.md) [Visual Studio テンプレートスキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
