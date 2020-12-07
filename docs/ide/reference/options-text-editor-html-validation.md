---
title: '[オプション]、[テキスト エディター]、[HTML (Web フォーム)]、[検証]'
description: '[HTML] セクションの [検証] ページを使用して、ドキュメント内の HTML マークアップの構文を HTML エディターでチェックする方法を設定する方法について説明します。'
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: b65edc2b6c48bc76075e909d0f9bd1341a1b6dd8
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96040564"
---
# <a name="options-text-editor-html-web-forms-validation"></a>[オプション]、[テキスト エディター]、[HTML (Web フォーム)]、[検証]

**[検証]** オプション ページを使用して、HTML エディターでドキュメント内の HTML マークアップの構文をどのようにチェックするかを設定します。 このページにアクセスするには、メニュー バーで **[ツール]**  >  **[オプション]** を選択し、 **[テキスト エディター]**  >  **[HTML (Web フォーム)]**  >  **[検証]** を展開します。

## <a name="validation"></a>検証

- **検証スキーマの検出に DOCTYPE を使用する**

   スキーマは、要素、属性、およびそのスキーマで有効な大文字小文字の設定を決定します。 IntelliSense で使用できるタグと属性も決定します。

   Visual Studio がページの **<!DOCTYPE>** 宣言と **html** 要素の内容を使用してスキーマを判断するように設定するには、このオプションを選択します。 たとえば、このオプションを選択しているときに、ページに `<!DOCTYPE html>` 宣言が含まれている場合、Visual Studio では HTML5 スキーマが使用されます。 ただし、**html** タグに **xmlns** 属性 (`<html xmlns="http://www.w3.org/1999/xhtml">` など) が含まれている場合、Visual Studio では XHTML5 スキーマが使用されます。

- **DOCTYPE が見つからないときのターゲット**

   ページに **<!DOCTYPE>** 宣言が含まれていないときに検証に使用するスキーマを選択します。

  - **エラーの表示**

     検証を有効にするには、このチェック ボックスをオンにします。 チェック ボックスをオフにすると、エディターは検証エラーをマークしません。

     他のチェック ボックスを使用してエディターでマーク対象とする個々のエラーの種類を指定することで、検証を細かく調整できます。

     > [!NOTE]
     > スキーマによっては、個々のエラーの種類をマークできません。 たとえば、ターゲット スキーマとして **[XHTML 1.1]** を選択すると、オプションのチェック ボックスはすべて無効になります。 この場合は、すべての種類のエラーがマークされます。

## <a name="see-also"></a>関連項目

- [[全般]、[環境]、[オプション] ダイアログ ボックス](../../ide/reference/general-environment-options-dialog-box.md)
