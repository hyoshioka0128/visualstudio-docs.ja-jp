---
title: カスタム パラメータ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- wizards, custom parameters
- custom parameters
ms.assetid: ba5c364b-66e6-47ea-9760-a0b70de8f0a0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cd52a49daa7d57a21d8cb0896f7108efa09e32b2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708946"
---
# <a name="custom-parameters"></a>カスタム パラメータ
カスタム パラメータは、ウィザードの起動後のウィザードの操作を制御します。 関連する *.vsz*ファイルは、統合開発環境 (IDE) によってパッケージ化され、ウィザードの起動時に文字列の配列としてウィザードに渡されるユーザー定義のパラメーターの配列を提供します。 ウィザードは文字列の配列を解析し、その情報を使用してウィザードの実際の操作を制御します。 この方法で、ウィザードは *.vsz*ファイルの内容に応じて機能をカスタマイズできます。

 一方、コンテキスト パラメーターは、ウィザードの開始時のプロジェクトの状態を定義します。 詳細については、「コンテキスト[パラメーター](../../extensibility/internals/context-parameters.md)」を参照してください。

 カスタム パラメータを持つ *.vsz*ファイルの例を次に示します。

```
VSWIZARD 8.0
Wizard=VsWizard.VsWizard_Engine
Param="WIZARD_NAME = Sample Wizard"
Param="WIZARD_UI = FALSE"
Param="RELATIVE_PATH = VSWizards\Classwiz\ATL"
Param="PREPROCESS_FUNCTION = CanAddATLSupport"
Param="PROJECT_TYPE = CSPROJ"
```

 *.vsz*ファイルの作成者は、パラメーターの値を追加します。 ユーザーが [**ファイル]** メニューの **[新しいプロジェクト**] または **[新しい項目の追加]** を選択するか、**ソリューション エクスプローラー**でプロジェクトを右クリックすると、IDE はこれらの値を文字列の配列に収集します。 IDE は、フラグを設定して<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A>プロジェクトのメソッド<xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION>を呼び出し、プロジェクトは<xref:EnvDTE.IVsExtensibility.RunWizardFile%2A>、ウィザードを実行し、結果を返す担当メソッドを呼び出します。

 ウィザードは、文字列の配列を解析し、文字列に適切に作用します。 この方法でカスタム パラメーターを実装することにより、さまざまな機能を実行する 1 つのウィザードを作成できます。 つまり、1 つのウィザードに 3 つの異なる *.vsz*ファイルを含めることができました。 各ファイルは、さまざまな状況でウィザードの動作を制御するカスタム パラメーターの異なるセットを渡します。

 詳細については、「[ウィザード (.vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)」を参照してください。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>
- [コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)
- [ウィザード](../../extensibility/internals/wizards.md)
- [ウィザード (.vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
