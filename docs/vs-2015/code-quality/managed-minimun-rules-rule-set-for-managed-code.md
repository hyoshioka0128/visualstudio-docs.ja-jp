---
title: マネージコードに対するマネージ最小 Rules 規則セット |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
ms.assetid: 44a50c54-8dd3-42b2-8387-532a150e5a6c
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 83f8654a3cca246fa4853add231008e2fadbfc1d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667913"
---
# <a name="managed-minimun-rules-rule-set-for-managed-code"></a>マネージド コードの "マネージ最小規則" 規則セット
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

マネージ最小規則は、潜在的なセキュリティホール、アプリケーションのクラッシュ、その他の重要な論理エラーやデザインエラーなど、コードの最も重大な問題に焦点を当てています。 プロジェクトにカスタムの規則セットを作成する場合は、必ずこの規則セットを含める必要があります。

|ルール|説明|
|----------|-----------------|
|[CA1001](../code-quality/ca1001-types-that-own-disposable-fields-should-be-disposable.md)|破棄可能なフィールドを所有する型は、破棄可能でなければなりません|
|[CA1821](../code-quality/ca1821-remove-empty-finalizers.md)|空のファイナライザーを削除します|
|[CA2213](../code-quality/ca2213-disposable-fields-should-be-disposed.md)|破棄可能なフィールドは破棄されなければなりません|
|[CA2231](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)|ValueType.Equals のオーバーライドで、演算子 equals をオーバーロードします|
