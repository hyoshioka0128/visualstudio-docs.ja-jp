---
title: ウィザード (..Vsz) File |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- .vsz files
- vsz files
- wizards, files
ms.assetid: 72e1d0f3-eef1-455e-b803-96827f030f50
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ab1adde4c7018f136f47769e16a8ce2fedf72c93
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687661"
---
# <a name="wizard-vsz-file"></a>ウィザード (.Vsz) ファイル
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

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
  
 パラメーターを使用すると、.vsz ファイルでウィザードに追加のカスタムパラメーターを渡すことができます。 各値は、バリアントの配列内の文字列要素としてウィザードに渡されます。 詳細については、「 [カスタムパラメーター](../../extensibility/internals/custom-parameters.md)」を参照してください。 カスタムウィザードの開発で .vsz ファイルを使用する方法の詳細については、「」を参照してください [。.Vsz ファイル (プロジェクトコントロール)](https://msdn.microsoft.com/library/b8678fee-6795-46d1-9338-48b22d5e9207)  
  
 既定のロケール ID を .vsz ファイルに追加するには、= xxxx を指定します。ここで、 `FALLBACK_LCID` xxxx はロケール id (たとえば、英語の場合は 1033) を指定します。 `FALLBACK_LCID`パラメーターが定義されている場合、現在の ID が見つからない場合、ウィザードは指定されたフォールバックロケール ID を使用します。  
  
## <a name="see-also"></a>参照  
 [カスタムパラメーター](../../extensibility/internals/custom-parameters.md)   
 [ウィザード](../../extensibility/internals/wizards.md)   
 [テンプレート ディレクトリの説明 (.Vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
