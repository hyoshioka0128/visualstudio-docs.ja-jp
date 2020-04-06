---
title: ウィザード |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], providing wizard support
ms.assetid: 59d9a77f-ee80-474b-a14f-90f477ab717b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d65cf2dcc10380b0ac750c8e1b0e7fd56eab95b5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703209"
---
# <a name="wizards"></a>ウィザード
ウィザードを作成した後は、通常、統合開発環境 (IDE) に追加して、他の[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ユーザーが使用できるようにします。 追加したウィザードが **[新しいプロジェクトの追加]** または [**新しい項目の追加]** ダイアログ ボックスに表示されます。 [**新しいプロジェクトの追加**] ダイアログ ボックスまたは [**新しい項目の追加**] ダイアログ ボックスを表示するには、**ソリューション エクスプローラ**で開いているソリューションを右クリックし、[**追加**] をポイントして、[**新しいプロジェクト**] または **[新しい項目**] をクリックします。

 ウィザードを実装すると、 [ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **新しいプロジェクトの追加 ]** ダイアログ ボックスまたは [**新しい項目の追加**] ダイアログ ボックスを開くときや、ソリューション**エクスプローラ**で項目を右クリックしたときに、使用可能な値のツリー ビューから選択できます。

 ウィザードでは、新しいプロジェクトの名前をローカライズするオプションを指定したり、ユーザーがウィザードを選択したときに表示されるアイコンを指定したりできます。 また、新しい項目が他の利用可能な項目に対して相対的に表示される順序を制御することもできます。項目はアルファベット順に整理する必要はありません。

 また、ウィザードを開いたときに渡されるカスタム パラメータに基づいて、異なる起動するウィザードを指定することもできます。

 このセクションのトピックでは、ウィザードを使用できるウィザードとテンプレートの[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]一覧に表示する **[新しいプロジェクトの追加**] ダイアログ ボックスと **[新しい項目の追加**] ダイアログ ボックスを使用するために実装するファイルと、IDE で正しく動作するためにウィザードが満たす必要がある要件について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [テンプレート ディレクトリの説明 (.Vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)

 どのテンプレート ディレクトリ記述ファイルの概要を示し、IDE でフォルダ、ウィザード .vsz ファイル、およびプロジェクトに関連付けられたテンプレート ファイルをダイアログ ボックスに表示するしくみについて説明します。

- [ウィザード (.Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)

 ウィザードを起動する方法と、.vsz ファイルの 3 つの部分を示す方法について説明します。

- [ウィザード インターフェイス (IDTWizard)](../../extensibility/internals/wizard-interface-idtwizard.md)

 ウィザードが`IDTWizard`IDE で動作するために実装する必要があるインターフェイスについて説明します。

- [コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)

 ウィザードの実装方法と、IDE がコンテキスト パラメータを実装に渡すときの動作について説明します。

- [カスタム パラメーター](../../extensibility/internals/custom-parameters.md)

 カスタム パラメータを使用して、ウィザードの起動後にウィザードの操作を制御する方法について説明します。

## <a name="related-sections"></a>関連項目
- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 新しいプロジェクトの種類のデザイン方法に関する情報を提供するその他のトピックへのリンクを示します。

- [プロジェクトの拡張](../../extensibility/extending-projects.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクトおよびソリューションを使用してコード ファイルとリソース ファイルを編成する方法、またソース管理を実装する方法について説明します。
