---
title: '[オプション]、[テキスト エディター]、[HTML (Web フォーム)]、[検証]'
ms.date: 1/15/2019
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.HTML.Validation
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ede4600cb1fa1df118b4635a193d8bff348d5119
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75568283"
---
# <a name="options-text-editor-html-web-forms-validation"></a>[オプション]、[テキスト エディター]、[HTML (Web フォーム)]、[検証]

**[検証]** オプション ページを使用して、HTML エディターでドキュメント内の HTML マークアップの構文をどのようにチェックするかを設定します。 このページにアクセスするには、メニュー バーで **[ツール]**  >  **[オプション]** を選択し、 **[テキスト エディター]**  >  **[HTML (Web フォーム)]**  >  **[検証]** を展開します。

## <a name="validation"></a>検証

- **検証スキーマの検出に DOCTYPE を使用する**

   スキーマは、要素、属性、およびそのスキーマで有効な大文字小文字の設定を決定します。 IntelliSense で使用できるタグと属性も決定します。

   Visual Studio がページの **<!DOCTYPE>** 宣言と **html** 要素の内容を使用してスキーマを判断するように設定するには、このオプションを選択します。 たとえば、このオプションを選択しているときに、ページに `<!DOCTYPE html>` 宣言が含まれている場合、Visual Studio では HTML5 スキーマが使用されます。 ただし、**html** タグに **xmlns** 属性 (`<html>` など) が含まれている場合、Visual Studio では XHTML5 スキーマが使用されます。

- **DOCTYPE が見つからないときのターゲット**

   ページに **<!DOCTYPE>** 宣言が含まれていないときに検証に使用するスキーマを選択します。

  - **エラーの表示**

     検証を有効にするには、このチェック ボックスをオンにします。 チェック ボックスをオフにすると、エディターは検証エラーをマークしません。

     他のチェック ボックスを使用してエディターでマーク対象とする個々のエラーの種類を指定することで、検証を細かく調整できます。

     > [!NOTE]
     > スキーマによっては、個々のエラーの種類をマークできません。 たとえば、ターゲット スキーマとして **[XHTML 1.1]** を選択すると、オプションのチェック ボックスはすべて無効になります。 この場合は、すべての種類のエラーがマークされます。

## <a name="see-also"></a>関連項目

- [[全般]、[環境]、[オプション] ダイアログ ボックス](../../ide/reference/general-environment-options-dialog-box.md)
