---
title: ウィザード (.Vsz) ファイル |マイクロソフトドキュメント
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
ms.openlocfilehash: 0fedf409c0ca320c054ddf1cc16318d08d25463a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703308"
---
# <a name="wizard-vsz-file"></a>ウィザード (.Vsz) ファイル

統合開発環境 (IDE) では、.vsz ファイルを使用してウィザードを起動します。 これらの .vsz ファイルには、IDE がどのウィザードを呼び出し、ウィザードに渡す情報を決定するために使用する情報が含まれています。

.vsz ファイルは、セクションを持たない .ini 形式のテキスト ファイルのバージョンです。 IDE に認識されている情報は、ファイルの先頭に格納されます。 これにより、IDE によって呼び出されるウィザードと、IDE に渡される .vsz ファイル内のパラメーターとの間のリンクが提供されます。 ファイルの残りの部分には、ウィザード固有のパラメータが用意されており、IDE によって収集されて特定のウィザードに渡されます。

次の例は、.vsz ファイルの内容を示しています。

```
VSWizard 8.0
Wizard=VsWizard.CBlankSiteWizard -or- {123-1234556-123334}
Param="WIZARDNAME = Wizard One"
Param="WIZARDUI = FALSE"
```

次に、.vsz ファイルの各部分を示します。

|要素|説明|
|----------|-----------------|
|VS ウィザード|ファイルの最初のパラメータは、テンプレート ファイル形式のバージョン番号です。 このバージョン番号は 6.0、7.0、7.1、または 8.0 でなければなりません。 他の番号を開始できず、無効な形式エラーが発生します。|
|ウィザード|このフィールドには、ウィザードの OLE ProgID が含まれているか、または IDE によって共同作成されるウィザードの CLSID の GUID 文字列表現が含まれます。|
|Param|これらの部品はオプションです。 必要な数だけ追加できます。|

パラメーターを使用すると、.vsz ファイルは、追加のカスタム パラメーターをウィザードに渡すことができます。 各値は、バリアントの配列の文字列要素としてウィザードに渡されます。 詳細については、「[カスタム パラメータ](../../extensibility/internals/custom-parameters.md)」を参照してください。

.vsz ファイルにデフォルトのロケール ID を追加`FALLBACK_LCID`するには、=xxxx を指定します。 パラメーター`FALLBACK_LCID`が定義されている場合、現行 ID が見つからない場合、ウィザードは指定されたフォールバック・ロケール ID を使用します。

## <a name="see-also"></a>関連項目

- [カスタム パラメーター](../../extensibility/internals/custom-parameters.md)
- [ウィザード](../../extensibility/internals/wizards.md)
- [テンプレート ディレクトリの説明 (.Vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
