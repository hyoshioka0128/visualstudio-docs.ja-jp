---
title: Visual Studio の他のエディションでモデルおよびダイアグラムを読み取る
description: モデルの作成をサポートしていない Visual Studio のバージョンを使用する場合の、Visual Studio でのモデルと図の読み取り、および読み取り専用の動作について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- models, versions of Visual Studio
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ffbf39421f507338d14a6b05a667ec4301375067
ms.sourcegitcommit: 4d394866b7817689411afee98e85da1653ec42f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2020
ms.locfileid: "97360690"
---
# <a name="read-models-and-diagrams-in-other-visual-studio-editions"></a>Visual Studio の他のエディションでモデルおよびダイアグラムを読み取る

モデルの作成をサポートしていないバージョンの Visual Studio でモデルを開くと、モデルは読み取り専用モードで開きます。 このモードでは、ダイアグラムのレイアウトは変更できますが、モデルは変更できません。

モデルの作成をサポートしている Visual Studio のバージョンを確認するには、「 [アーキテクチャツールとモデリングツールのバージョンサポート](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

## <a name="obtaining-access-to-a-model-and-diagrams"></a>モデルおよび図へのアクセス

依存関係図を読み取るには、最初に Visual Studio を使用してモデリングプロジェクトを開き、その中でダイアグラムを開く必要があります。

このため、依存関係図を読み取る場合は、それが作成されたモデリングプロジェクトにもアクセスできる必要があります。 これを行うには、ソース管理からプロジェクトにアクセスするか、プロジェクトファイルのコピーを取得します。

> [!NOTE]
> これは、コードから生成されたコード マップおよび .NET クラス図には適用されません。 これらの図はモデリング プロジェクトとは関係なく表示できます。

依存関係図を読み取るには、最低限必要なファイルセットは次のとおりです。

- 読み取り対象のダイアグラムの2つの図ファイル (例、 **mydiagram. classdiagram と MyDiagram。**[...])。

    > [!NOTE]
    > 依存関係図については、 _Mydiagram_**. レイヤー図の抑制** という名前のファイルも必要です。

- モデリングプロジェクトファイル (**Mymodel. modelproj**)

- ルートモデルファイル (**ModelDefinition\MyModel.uml**)

- ダイアグラムで参照されているすべてのパッケージのパッケージファイル (**Modeldefinition\ mypackagethe uml**)

## <a name="changes-that-you-can-make-in-read-only-mode"></a>読み取り専用モードで行える変更

モデルの作成をサポートしていないバージョンの Visual Studio でモデルおよびその図を開く場合、モデルは変更できません。 つまり、図またはモデル エクスプローラーに表示されている要素と関係は変更できません。 ただし、図のレイアウトに次のような変更を加えることはできます:

- 図形およびコネクタを図に再配置する。

- 図形を展開および折りたたむ。

これらの変更は保存できます。 他のユーザーに変更を表示する場合は、少なくとも更新された **レイアウト** ファイルを送信する必要があります。

## <a name="see-also"></a>関連項目

- [依存関係図: リファレンス](../modeling/layer-diagrams-reference.md)
- [アプリのモデルを生成する](../modeling/create-models-for-your-app.md)
