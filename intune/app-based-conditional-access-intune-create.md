---
title: "Intune을 사용한 앱 기반 조건부 액세스 정책"
description: "이 항목에서는 Intune을 사용하여 앱 기반 조건부 액세스 정책을 구성하는 방법을 설명합니다."
keywords: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 06/28/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: d1693515-de18-4553-91ef-801976cd3ec7
ms.reviewer: chrisgre
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: a7f054868d0bae061f348239614f3a40b96a15b1
ms.sourcegitcommit: fd2e8f6f8761fdd65b49f6e4223c2d4a013dd6d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="set-up-app-based-conditional-access-policies"></a>앱 기반 조건부 액세스 정책 설정

[!INCLUDE[azure_portal](./includes/azure_portal.md)]

이 항목에서는 승인된 앱 목록에 포함된 앱에 대해 앱 기반 조건부 액세스 정책을 설정하는 방법에 대한 지침을 제공합니다. 승인된 앱 목록은 Microsoft에서 테스트한 앱으로 구성됩니다.

> [!IMPORTANT]
> 이 항목에서는 Exchange Online을 사용하여 앱 기반 조건부 액세스 정책을 추가하는 단계를 안내하지만, 승인된 앱 목록에서 SharePoint Online, Microsoft Teams 등의 다른 앱을 추가할 때도 동일한 단계를 사용할 수 있습니다.

## <a name="to-create-an-app-based-conditional-access-policy"></a>앱 기반 조건부 액세스 정책을 만들려면
1.  [Azure Portal](https://portal.azure.com)로 이동한 다음 자격 증명을 사용하여 로그인합니다.

2.  **추가 서비스**를 선택하고 "Intune"을 입력합니다.

3.  **Intune 앱 보호**를 선택합니다.

4.  **Intune 모바일 응용 프로그램 관리** 블레이드에서 **모든 설정**을 선택합니다.

5.  **조건부 액세스** 섹션에서 **Exchange Online**을 선택합니다.

    ![Exchange Online 옵션이 강조 표시된 조건부 액세스 섹션을 보여 주는 설정 블레이드 스크린샷](./media/MAM-conditional-access-1.png)

6. **허용된 앱** 블레이드에서 **Allow apps that support Intune app policies**(Intune 앱 정책을 지원하는 앱 허용) 옵션을 선택하여 앱 보호 정책에서 지원하는 앱만 Exchange Online에 액세스할 수 있도록 합니다. 이 옵션을 선택하는 경우 지원되는 앱 목록이 표시됩니다.

    > [!NOTE]
    > iOS 및 Android에서 Exchange Online에 연결하는 기본 제공 메일 클라이언트를 비롯하여 모든 Exchange Active Sync 메일 클라이언트에서 메일을 주고받을 수 없게 됩니다. 사용자는 대신 Outlook 메일 앱을 사용해야 한다고 알리는 단일 메일을 받습니다.

7. 사용자에게 이 정책을 적용하려면 **제한된 사용자 그룹** 블레이드를 열고 **사용자 그룹 추가**를 선택합니다. 이 정책을 받아야 하는 사용자 그룹을 하나 이상 선택하세요.

    ![사용자 그룹 추가 옵션이 강조 표시된 제한된 사용자 그룹 블레이드의 스크린샷](./media/mam-ca-add-user-group.png)

8. 이전 단계에서 선택한 사용자 그룹에 있는 사용자 중 일부를 이 정책에 의해 영향을 받지 않도록 할 수 있습니다. 이 경우 제외된 사용자 그룹 목록에 사용자 그룹을 추가합니다. **Exchange Online** 블레이드에서 **제외된 사용자 그룹**을 선택합니다. **사용자 그룹 추가**를 선택하여 사용자 그룹 목록을 엽니다. 이 정책에서 제외할 그룹을 선택합니다.

## <a name="to-modify-or-delete-user-groups-from-an-existing-app-based-ca-policy"></a>기존 앱 기반 CA 정책에서 사용자 그룹을 수정하거나 삭제하려면

1. **제한된 사용자 그룹** 블레이드를 열고 삭제할 사용자 그룹을 강조 표시합니다.
2. 삭제 옵션을 보려면 타원을 클릭합니다.
3. **삭제**를 선택하여 목록에서 사용자 그룹을 제거합니다.

## <a name="next-steps"></a>다음 단계
[최신 인증이 없는 앱 차단](app-modern-authentication-block.md)

### <a name="see-also"></a>참고 항목

[앱 보호 정책을 사용하여 앱 데이터 보호](app-protection-policies.md)