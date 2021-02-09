---
title: カスタムパラメーター |Microsoft Docs
description: ウィザードの開始後にウィザードの操作を制御するカスタムパラメーターを作成する方法については、.vsz ファイルを変更する方法に関するページを参照してください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- wizards, custom parameters
- custom parameters
ms.assetid: ba5c364b-66e6-47ea-9760-a0b70de8f0a0
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1b4927e63bec93fbe7b6730e131a0893372aa70d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99902965"
---
# <a name="custom-parameters"></a>カスタムパラメーター
カスタムパラメーターは、ウィザードが開始された後のウィザードの操作を制御します。 関連する .vsz ファイルは、統合開発環境 (IDE: integrated development environment) によってパッケージ化され、ウィザードの開始時に文字列の配列としてウィザードに渡されるユーザー定義パラメーターの配列を提供し *ます。* 次に、ウィザードは文字列の配列を解析し、情報を使用してウィザードの実際の操作を制御します。 この方法では、 *.vsz* ファイルの内容に応じて、ウィザードを使用して機能をカスタマイズできます。

 一方、コンテキストパラメーターは、ウィザードを起動したときのプロジェクトの状態を定義します。 詳細については、「 [コンテキストパラメーター](../../extensibility/internals/context-parameters.md)」を参照してください。

 カスタムパラメーターを持つ *.vsz* ファイルの例を次に示します。

```
VSWIZARD 8.0
Wizard=VsWizard.VsWizard_Engine
Param="WIZARD_NAME = Sample Wizard"
Param="WIZARD_UI = FALSE"
Param="RELATIVE_PATH = VSWizards\Classwiz\ATL"
Param="PREPROCESS_FUNCTION = CanAddATLSupport"
Param="PROJECT_TYPE = CSPROJ"
```

 *.Vsz* ファイルの作成者は、パラメーターの値を追加します。 ユーザーが [**ファイル**] メニューまたは **ソリューションエクスプローラー** 内のプロジェクトを右クリックして [**新しいプロジェクト**] または [**新しい項目の追加**] を選択すると、IDE によってこれらの値が文字列の配列に収集されます。 次に、IDE はフラグが設定されたプロジェクトのメソッドを呼び出し、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A> <xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION> プロジェクトは <xref:EnvDTE.IVsExtensibility.RunWizardFile%2A> ウィザードを実行して結果を返すメソッドを呼び出します。

 このウィザードでは、文字列の配列を解析し、文字列に対して適切に動作します。 このようにして、カスタムパラメーターを実装することで、さまざまな機能を実行する1つのウィザードを作成できます。 言い換えると、ウィザードの中には、3つの異なる *.vsz* ファイルが含まれていることがあります。 各ファイルは、さまざまな状況でウィザードの動作を制御するために、さまざまなカスタムパラメーターのセットを渡します。

 詳細については、「 [ウィザード (.vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)」を参照してください。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>
- [コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)
- [ウィザード](../../extensibility/internals/wizards.md)
- [ウィザード (.vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
