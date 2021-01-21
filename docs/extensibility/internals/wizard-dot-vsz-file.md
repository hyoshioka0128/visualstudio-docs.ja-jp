---
title: ウィザード (..Vsz) File |Microsoft Docs
description: IDE がウィザードを開始するために使用する .vsz ファイルについて説明します。 ファイルには、呼び出すウィザードとウィザードに渡す処理に関する情報が含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .vsz files
- vsz files
- wizards, files
ms.assetid: 72e1d0f3-eef1-455e-b803-96827f030f50
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5fe32028f271d02dd518509bb86906197e6acb4e
ms.sourcegitcommit: 19061b61759ce8e3b083a0e01a858e5435580b3e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97487739"
---
# <a name="wizard-vsz-file"></a>ウィザード (.Vsz) ファイル

統合開発環境 (IDE: integrated development environment) では、.vsz ファイルを使用してウィザードを開始します。 これらの .vsz ファイルには、どのウィザードを呼び出すか、およびどの情報をウィザードに渡すかを決定するために IDE が使用する情報が含まれています。

.Vsz ファイルは、セクションのない .ini 形式のテキストファイルのバージョンです。 IDE で認識されている情報は、ファイルの先頭に格納されます。 これにより、IDE が呼び出すウィザードと、IDE に渡される .vsz ファイル内のパラメーターとの間のリンクが提供されます。 ファイルの残りの部分には、ウィザードに固有のパラメーターが用意されています。このパラメーターは、IDE によって収集され、特定のウィザードに渡されます。

次の例は、.vsz ファイルの内容を示しています。

```
VSWizard 8.0
Wizard=VsWizard.CBlankSiteWizard -or- {123-1234556-123334}
Param="WIZARDNAME = Wizard One"
Param="WIZARDUI = FALSE"
```

.Vsz ファイルの各部分を次に示します。

|パーツ|説明|
|----------|-----------------|
|VSWizard|ファイルの最初のパラメーターは、テンプレートファイル形式のバージョン番号です。 このバージョン番号は6.0、7.0、7.1、または8.0 である必要があります。 他の数値を開始できないため、無効な形式エラーが発生します。|
|ウィザード|このフィールドには、ウィザードの OLE ProgID、または IDE によって作成されたウィザードの CLSID の GUID 文字列表現が含まれます。|
|Param|これらの部分は省略可能です。 必要な数だけ追加できます。|

パラメーターを使用すると、.vsz ファイルでウィザードに追加のカスタムパラメーターを渡すことができます。 各値は、バリアントの配列内の文字列要素としてウィザードに渡されます。 詳細については、「 [カスタムパラメーター](../../extensibility/internals/custom-parameters.md)」を参照してください。

既定のロケール ID を .vsz ファイルに追加するには、= xxxx を指定します。ここで、 `FALLBACK_LCID` xxxx はロケール id (たとえば、英語の場合は 1033) を指定します。 `FALLBACK_LCID`パラメーターが定義されている場合、現在の ID が見つからない場合、ウィザードは指定されたフォールバックロケール ID を使用します。

## <a name="see-also"></a>こちらもご覧ください

- [カスタム パラメーター](../../extensibility/internals/custom-parameters.md)
- [ウィザード](../../extensibility/internals/wizards.md)
- [テンプレート ディレクトリの説明 (.Vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
