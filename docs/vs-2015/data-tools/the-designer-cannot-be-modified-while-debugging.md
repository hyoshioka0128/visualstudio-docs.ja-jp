---
title: デバッグ中にデザイナーを変更することはできません |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 487dafe4-d57c-4be1-9e3a-bb0a8699b2fa
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a8e393ad46b6d37bd74806a0a4b84825bd059457
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672276"
---
# <a name="the-designer-cannot-be-modified-while-debugging"></a>デバッグ中はデザイナーを変更できません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このメッセージは、アプリケーションがデバッグ モードで実行されているときに、O/R デザイナーで項目を変更しようとした場合に表示されます。 アプリケーションがデバッグ モードで実行されている場合、O/R デザイナーは読み取り専用です。

### <a name="to-correct-this-error"></a>このエラーを解決するには

- [**デバッグ**] メニューの [**デバッグの停止**] をクリックします。

     アプリケーションのデバッグが停止し、O/R デザイナーの項目を変更できるようになります。

## <a name="see-also"></a>参照
 [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)[チュートリアル: LINQ to SQL クラスの作成 (O/R デザイナー)](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)
