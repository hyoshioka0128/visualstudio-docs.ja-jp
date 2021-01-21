---
title: コード分析を用いたチェックイン ポリシーに関するバージョンの互換性
ms.date: 11/04/2016
description: Team System 2008 Team Foundation Server と Team Foundation Server 2010 が Visual Studio チェックインポリシーを異なる方法で評価する方法について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 3a681f510da270bc22ae4bc983103f9a5735a127
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94436876"
---
# <a name="version-compatibility-for-code-analysis-check-in-policies"></a>コード分析を用いたチェックイン ポリシーに関するバージョンの互換性

さまざまなバージョンのを使用してコード分析のチェックインポリシーを評価して作成する必要がある場合は、 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] チェックインポリシーの違いを把握しておく必要があり [!INCLUDE[vstsTfsOrcasLong](../code-quality/includes/vststfsorcaslong_md.md)] [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] ます。

## <a name="version-compatibility-for-evaluating-check-in-policies"></a>Check-In ポリシーを評価するためのバージョンの互換性

- コード分析のチェックインポリシーがで評価される場合 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 、に [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 存在するが、に存在しないすべての規則 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] は無視されます。

- コード分析のチェックインポリシーがで評価される場合 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 、に対して排他的なすべての新しい規則 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] は無視されます。

- コード分析のチェックインポリシーで規則アセンブリが指定されている場合、は、認識され [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] ないアセンブリによって指定されたすべての規則を無視します。

- コード分析のチェックインポリシーで、を認識しない規則アセンブリが指定されている場合は [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 、メッセージが表示されます。

## <a name="version-compatibility-for-authoring-check-in-policies"></a>Check-In ポリシーの作成に関するバージョンの互換性

- バージョンのを使用してコード分析のチェックインポリシーを作成した場合、バージョンのを使用して [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 変更することはできません [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 。 また、は [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] ポリシーを評価できません。

- のを使用してコード分析のチェックインポリシーを作成した場合は [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 、のを使用して変更でき [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] ます。また、でポリシーを評価することもでき [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] ます。 のを使用してポリシーを変更した後 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] で、のを使用してポリシーを編集することはできなくなりました [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 。 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] では、厳密な名前が一致しないと、ポリシーを評価できます。

- との両方に適用される規則設定を使用してコード分析のチェックインポリシーを作成するには、 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] でポリシーを作成し、 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 必要なすべての変更を行い、ポリシーを保存する必要があります。 規則に対する変更がにのみ存在する場合は [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 、でポリシーを変更して保存し [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] ます。

   でポリシーを保存すると [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 、のみに存在する規則の設定を変更できなくなり [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] ます。
