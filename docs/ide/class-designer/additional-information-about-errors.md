---
title: クラス デザイナーのエラー
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- vs.classdesigner.CPlusPlusViewInDiagramNoTypeFound
- vs.classdesigner.CPlusPlusNoTypeFound
- vs.classdesigner.CannotShowBaseType
- vs.classdesigner.MatchOrphanTypesAtLoad
- vs.classdesigner.CannotShowType
- vs.classdesigner.AssociationTypeNotFoundError
- vs.classdesigner.ViewInDiagramNoTypesFound
- vs.classdesigner.CannotImplementInterface
- vs.classdesigner.CannotShowImplementedInterface
- vs.classdesigner.ViewInDiagramUnparsableTypeFound
- vs.classdesigner.AssociationTypeNotFound
- vs.classdesigner.CPlusPlusTypeCannotBeAdded
helpviewer_keywords:
- errors, class diagrams
- errors, Class Designer
- error messages, Class Designer
- error messages, class diagrams
- Class Designer [Visual Studio], errors
- class diagrams, errors
ms.assetid: 79d70e70-704c-4255-ab68-c10d6949470e
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dc8b2c013a3e685a6071f4a12d63e3ca475051a0
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75596516"
---
# <a name="class-designer-errors"></a>クラス デザイナーのエラー

**クラス デザイナー**はソース ファイルの場所を追跡しないため、プロジェクト構造を変更するか、プロジェクト内でソース ファイルを移動すると、**クラス デザイナー**が型を見失うことがあります。たとえば、typedef 型、基本クラス型、またはアソシエーション型のソースの型を変更する場合によくあります。 **クラス デザイナーはこの型を表示できません**などのエラーが発生することがあります。 エラーを修正するには、変更または再配置したソース コードをもう一度クラス ダイアグラムにドラッグして再表示します。

## <a name="resources"></a>リソース

以下のリソースで、その他のエラーや警告に関して役立つ情報を参照できます。

- 「[Visual C++ コードの使用](working-with-visual-cpp-code.md)」には、クラス ダイアグラムでの C++ の表示に関するトラブルシューティング情報が含まれます。
- [Visual Studio クラス デザイナー フォーラム](https://social.msdn.microsoft.com/Forums/en-US/home?forum=vsclassdesigner)は、**クラス デザイナー**に関する質問のためのフォーラムです。

## <a name="see-also"></a>参照

- [クラスと型の設計と表示](designing-and-viewing-classes-and-types.md)
