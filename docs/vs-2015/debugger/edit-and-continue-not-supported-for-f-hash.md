---
title: F# ではエディット コンティニュはサポートされません | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Edit and Continue [F#]
- Debugging [F#], Edit and Continue
ms.assetid: 40ec77bb-07e3-4b58-9254-ae015009441c
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a4fef61335679e3f82d5916726981e003bf9c332
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62428465"
---
# <a name="edit-and-continue-not-supported-for-f"></a>F# ではエディット コンティニュはサポートされません。 #
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

F# コードのデバッグ時は、エディット コンティニュはサポートされません。 デバッグ セッション中に F# コードを編集することは可能ですが、そのような操作は避けてください。 コードの変更はデバッグ セッション中は適用されません。 したがって、デバッグ中に F# コードを編集すると、ソース コードとデバッグ中のコードが一致しなくなります。
