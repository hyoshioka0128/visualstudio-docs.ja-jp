---
title: F# ではエディット コンティニュはサポートされません | Microsoft Docs
description: F# のデバッグについては、エディット コンティニュはサポートされません。 デバッグ中にコードを編集してもソースに適用されないため、デバッグ対象のコードはソースと一致しなくなります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue [F#]
- Debugging [F#], Edit and Continue
ms.assetid: 40ec77bb-07e3-4b58-9254-ae015009441c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 33d1e8379e71c41e42cbf761ccdfe740342ee642
ms.sourcegitcommit: 47da50a74fcd3db66d97cb20accac983bc41912f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96863089"
---
# <a name="edit-and-continue-not-supported-for-f"></a>F# ではエディット コンティニュはサポートされません。 #
F# コードのデバッグ時は、エディット コンティニュはサポートされません。 デバッグ セッション中に F# コードを編集することは可能ですが、そのような操作は避けてください。 コードの変更はデバッグ セッション中は適用されません。 したがって、デバッグ中に F# コードを編集すると、ソース コードとデバッグ中のコードが一致しなくなります。
