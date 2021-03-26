---
title: ウィザード |Microsoft Docs
description: Visual Studio で使用可能なウィザードとテンプレート、およびウィザードが IDE で満たす必要のある要件について、ウィザードを一覧表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], providing wizard support
ms.assetid: 59d9a77f-ee80-474b-a14f-90f477ab717b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b5c5cb9649689f711844f97e0b57ab23248e9a00
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074159"
---
# <a name="wizards"></a>ウィザード
ウィザードを作成した後は、通常、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 他のユーザーが使用できるように統合開発環境 (IDE) に追加します。 追加したウィザードは、[ **新しいプロジェクトの追加** ] または [ **新しい項目の追加** ] ダイアログボックスに表示されます。 [ **新しいプロジェクトの追加** ] または [ **新しい項目の追加** ] ダイアログボックスを表示するには、 **ソリューションエクスプローラー** で開いているソリューションを右クリックし、[ **追加**] をポイントして、[ **新しいプロジェクト** ] または [ **新しい項目**] をクリックします。

 でウィザードを実装すると、ユーザーが [ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **新しいプロジェクトの追加** ] ダイアログボックスまたは [ **新しい項目の追加** ] ダイアログボックスを開いたとき、または **ソリューションエクスプローラー** 内の項目を右クリックしたときに、使用可能な値のツリービューから選択できるようになります。

 ウィザードでは、新しいプロジェクトまたはユーザーの名前をローカライズするオプションを指定できます。また、ウィザードを選択したときにユーザーに表示されるアイコンを決定することもできます。 また、使用可能な他の項目と比較して、新しい項目を表示する順序を制御することもできます。項目をアルファベット順に整理する必要はありません。

 ウィザードを開いたときに渡されるカスタムパラメーターに基づいて、異なる方法で起動するウィザードを指定することもできます。

 このセクションの各トピックでは、[ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **新しいプロジェクトの追加** ] ダイアログボックスと [ **新しい項目の追加** ] ダイアログボックスを使用してウィザードを一覧表示し、使用可能なウィザードとテンプレートを表示する方法、およびウィザードが IDE で正しく動作するために満たす必要がある要件について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [テンプレート ディレクトリの説明 (.Vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)

 テンプレートディレクトリ記述ファイルの概要と、ダイアログボックス内のプロジェクトに関連付けられているフォルダー、ウィザード .vsz ファイル、およびテンプレートファイルを IDE でどのように表示するかについて説明します。

- [ウィザード (.Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)

 IDE によるウィザードの起動方法と、.vsz ファイルの3つの部分の一覧を示します。

- [ウィザード インターフェイス (IDTWizard)](../../extensibility/internals/wizard-interface-idtwizard.md)

 `IDTWizard`IDE で動作するためにウィザードが実装する必要のあるインターフェイスについて説明します。

- [コンテキストパラメーター](../../extensibility/internals/context-parameters.md)

 ウィザードの実装方法と、IDE がコンテキストパラメーターを実装に渡すときの動作について説明します。

- [カスタムパラメーター](../../extensibility/internals/custom-parameters.md)

 ウィザードを起動した後に、カスタムパラメーターを使用してウィザードの操作を制御する方法について説明します。

## <a name="related-sections"></a>関連項目
- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 新しいプロジェクトの種類をデザインする方法に関する情報を提供するその他のトピックへのリンクを示します。

- [プロジェクトの拡張](../../extensibility/extending-projects.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクトおよびソリューションを使用してコード ファイルとリソース ファイルを編成する方法、またソース管理を実装する方法について説明します。
