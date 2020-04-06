---
title: オートメーションモデルの概要 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], about automation
- extensibility
ms.assetid: 12b6d6db-0d22-4aaa-aa7d-1365f759b7b0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7b940677c370106ebdcc63c7984d553003251e8a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710005"
---
# <a name="automation-model-overview"></a>オートメーション モデルの概要
オートメーション モデルは、Visual Studio のアドインまたは拡張機能を作成できるオブジェクトのセットで構成されます。 アドインは、Visual Studio 環境を操作し、一般的なタスクを自動化できるアプリケーションです。 Visual Studio 拡張機能は、カスタム Visual Studio コンポーネントを作成したり、テキスト エディターなどの標準コンポーネントの機能を追加したりできます。

## <a name="objects-in-the-automation-model"></a>オートメーション モデル内のオブジェクト
 オートメーション モデルは、共通環境の主要なファセットを制御するオブジェクトの関連グループで構成されます。 次の図は、オートメーション モデルを構成する Visual Studio オブジェクトの広範なセットを示しています。

 ![ビジュアルスタジオオートメーションオブジェクトチャート](../../extensibility/internals/media/vsvisualstudioautomationobjectchart.gif "オブジェクトチャート")

 詳細については、「 [Visual Studio 環境の拡張](https://msdn.microsoft.com/Library/4173a963-7ac7-4966-9bb7-e28a9d9f6792)」を参照してください。

 環境は、さまざまな機能領域のモデルを提供します。 たとえば、コード内にさまざまな要素のコード モデルがあります。 さまざまなドキュメント要素のドキュメント モデルがあります。 プロジェクト領域の 1 つは、VSPackage プロバイダーに特に関心があります。 新しいプロジェクトの種類は、オートメーション モデル[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]とほぼ同じ方法でオートメーション モデルに貢献し[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]、オートメーション モデルに貢献する必要があります。 このプロセスの概要については[、「VSPackages のオートメーションを提供する](../../extensibility/internals/providing-automation-for-vspackages.md)」を参照してください。

 環境のオートメーション モデルの拡張を検討できる場所:

- Project

- ドキュメント

- コード

- ビルド

オートメーションの詳細については、「 [Visual Studio のオートメーションと機能拡張](/visualstudio/extensibility/extensibility-in-visual-studio?view=vs-2015)」を参照してください。 このドキュメントと、VSPackage のオートメーションを提供する方法に関する決定を行う際のリンクを提供するドキュメント。

## <a name="see-also"></a>関連項目
- [方法: アドインを作成する](https://msdn.microsoft.com/Library/50be56d2-e3a5-4cd2-8569-2a0666b268ce)
