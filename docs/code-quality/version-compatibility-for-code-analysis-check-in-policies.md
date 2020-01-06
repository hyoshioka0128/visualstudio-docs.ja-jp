---
title: コード分析を用いたチェックイン ポリシーに関するバージョンの互換性
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- version compatibility, code analysis check-in policy
- check-in policies, version compatibility for code analysis
ms.assetid: 1af376e3-3be7-4445-803b-76a858567a5b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4757b3a105ff02a92944d9b45e645e2c63a8b81c
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75587161"
---
# <a name="version-compatibility-for-code-analysis-check-in-policies"></a>コード分析を用いたチェックイン ポリシーに関するバージョンの互換性

さまざまなバージョンの [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)]を使用してコード分析チェックインポリシーを評価して作成する必要がある場合は、[!INCLUDE[vstsTfsOrcasLong](../code-quality/includes/vststfsorcaslong_md.md)] と [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] チェックインポリシーの評価方法の違いを把握しておく必要があります。

## <a name="version-compatibility-for-evaluating-check-in-policies"></a>チェックインポリシーを評価するためのバージョンの互換性

- コード分析のチェックインポリシーが [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]で評価される場合、[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] に存在していても [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] に存在しないすべての規則は無視されます。

- コード分析のチェックインポリシーが [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]で評価されると、[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] に限定されたすべての新しい規則は無視されます。

- コード分析のチェックインポリシーで規則アセンブリが指定されている場合、[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] は、認識されないアセンブリによって指定されたすべての規則を無視します。

- コード分析のチェックインポリシーで [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] が認識しない規則アセンブリが指定されている場合は、メッセージが表示されます。

## <a name="version-compatibility-for-authoring-check-in-policies"></a>チェックインポリシーを作成するためのバージョンの互換性

- [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] バージョンの [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)]を使用してコード分析チェックインポリシーを作成した場合は、[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] バージョンの [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] を使用して変更することはできません。 また、[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] はポリシーを評価できません。

- [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]で [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] を使用してコード分析のチェックインポリシーを作成した場合は、[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] で [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] を使用して変更することができ、ポリシーは [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]で評価することもできます。 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]で [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] を使用してポリシーを変更した後、[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]で [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] を使用してポリシーを編集することはできなくなりました。 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] は、厳密な名前が一致しないと、ポリシーを評価できます。

- [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] と [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]の両方に適用されるルール設定を使用してコード分析のチェックインポリシーを作成するには [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]でポリシーを作成し、すべての変更を行い、ポリシーを保存する必要があります。 ルールに対する変更が [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]にのみ存在する場合は、[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]でポリシーを変更して保存します。

   [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]にポリシーを保存すると、[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] にのみ存在する規則の設定を変更できなくなります。
