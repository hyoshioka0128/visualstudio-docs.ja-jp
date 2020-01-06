---
title: Visual Studio の他のエディションでモデルおよびダイアグラムを読み取る
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
ms.openlocfilehash: ebe4cdcefb7b823090cca8976055de5a3ebb9b1a
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595411"
---
# <a name="read-models-and-diagrams-in-other-visual-studio-editions"></a>Visual Studio の他のエディションでモデルおよびダイアグラムを読み取る

モデルの作成をサポートしていないバージョンの Visual Studio でモデルを開くと、モデルは読み取り専用モードで開きます。 このモードでは、ダイアグラムのレイアウトは変更できますが、モデルは変更できません。

モデルの作成をサポートする Visual Studio のバージョンを確認するを参照してください。[アーキテクチャとモデリング ツールのバージョンのサポート](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)します。

## <a name="obtaining-access-to-a-model-and-diagrams"></a>モデルおよび図へのアクセス

依存関係図を読み取るには、まず Visual Studio を使用して、モデリング プロジェクトを開き、し、その中で図を開く必要があります。

このため、依存関係図を読みたい場合も必要が作成されたモデリング プロジェクトへのアクセス。 これを行うか、ソース管理からプロジェクトにアクセスするか、プロジェクト ファイルのコピーを取得します。

> [!NOTE]
> これは、コードから生成されたコード マップおよび .NET クラス図には適用されません。 これらの図はモデリング プロジェクトとは関係なく表示できます。

依存関係図を読み取るには、必要なファイルの最小セットがとおりです。

- 2 つのダイアグラム ファイルを読み取るには、たとえば、ダイアグラムの**MyDiagram.classdiagram と MyDiagram.classdiagram.layout**します。

    > [!NOTE]
    > 依存関係を示す図については、という名前のファイルもがする必要があります_MyDiagram_ **. layerdiagram.suppressions**します。

- モデリング プロジェクト ファイル (**MyModel.modelproj**)

- ルート モデル ファイル (**ModelDefinition\MyModel.uml**)

- ダイアグラムで参照されているすべてのパッケージのパッケージ ファイル (**ModelDefinition\MyPackage.uml**)

## <a name="changes-that-you-can-make-in-read-only-mode"></a>読み取り専用モードで行える変更

モデルの作成をサポートしていないバージョンの Visual Studio でモデルおよびその図を開く場合、モデルは変更できません。 つまり、図またはモデル エクスプローラーに表示されている要素と関係は変更できません。 ただし、図のレイアウトに次のような変更を加えることはできます:

- 図形およびコネクタを図に再配置する。

- 図形を展開および折りたたむ。

これらの変更は保存できます。 変更内容を他のユーザーに表示されるようにする場合は、送信しなければならない以上で、更新された **.layout**ファイル。

## <a name="see-also"></a>関連項目

- [依存関係図: リファレンス](../modeling/layer-diagrams-reference.md)
- [アプリのモデルを生成する](../modeling/create-models-for-your-app.md)
