---
title: Microsoft Intune에서 디바이스 프로필 할당
description: Azure Portal을 사용하여 사용자 및 디바이스에 디바이스 프로필 및 정책을 할당합니다. Microsoft Intune에서 프로필 할당으로부터 그룹을 제외하는 방법에 대해 알아봅니다.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/08/2019
ms.topic: conceptual
ms.prod: ''
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f6f5414d-0e41-42fc-b6cf-e7ad76e1e06d
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0c950efdd95fd8d856ec677385712a022dead870
ms.sourcegitcommit: 02803863eba37ecf3d8823a7f1cd7c4f8e3bb42c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59570509"
---
# <a name="assign-user-and-device-profiles-in-microsoft-intune"></a>Microsoft Intune에서 사용자 및 디바이스 프로필 할당

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

프로필을 만들고 이 프로필에는 입력한 모든 설정이 포함됩니다. 다음 단계에서는 Azure AD(Azure Active Directory) 사용자 또는 디바이스 그룹에 프로필을 배포 또는 “할당”합니다. 할당된 경우 사용자 및 디바이스는 프로필을 수신하고 입력한 설정이 적용됩니다.

이 문서에서는 프로필을 할당하는 방법을 보여 주고 프로필에서 범위 태그를 사용하는 방법을 설명합니다.

## <a name="assign-a-device-profile"></a>디바이스 프로필 할당

1. [Azure Portal](https://portal.azure.com)에서 **모든 서비스**를 선택하고 **Intune**을 기준으로 필터링하고 **Intune**을 선택합니다.
2. **디바이스 구성** > **프로필**을 선택합니다. 모든 프로필이 나열됩니다.
3. 할당하려는 프로필을 선택한 후 **할당**을 선택합니다.
4. 그룹을 **포함**하거나 **제외**하도록 선택한 다음, 그룹을 선택합니다. 그룹을 선택하면 Azure AD 그룹을 선택합니다. 여러 그룹을 선택하려면 **Ctrl** 키를 누른 상태로 그룹을 선택합니다.

    ![프로필 할당에서 그룹 제외 또는 포함하는 옵션 스크린샷](./media/group-include-exclude.png)

5. 변경 내용을 **저장**합니다.

### <a name="evaluate-how-many-users-are-targeted"></a>대상으로 지정된 사용자 수 평가

프로필을 할당하면 영향을 받는 사용자 수를 **평가**할 수도 있습니다. 이 기능은 사용자 수를 계산하며, 디바이스 수는 계산하지 않습니다.

1. Intune에서 **디바이스 구성** > **프로필**을 선택합니다.
2. 프로필을 선택한 후 **할당** > **평가**를 선택합니다. 메시지는 이 프로필의 대상이 되는 사용자 수를 보여 줍니다.

**평가** 단추가 회색으로 표시되면 프로필이 하나 이상의 그룹에 할당되었는지 확인합니다.


## <a name="use-scope-tags"></a>범위 태그 사용

프로필을 만들거나 업데이트하면 프로필에 범위 태그를 추가할 수도 있습니다.

**범위 태그**는 인사 관리 또는 모든 US-NC 직원과 같은 특정 그룹으로 정책을 할당 및 필터링할 수 있는 좋은 방법입니다. 자세한 내용은 [분산형 IT에 RBAC 및 범위 태그 사용](scope-tags.md)을 참조하세요.

## <a name="exclude-groups-from-a-profile-assignment"></a>프로필 할당에서 그룹 제외

Intune 디바이스 구성 프로필을 통해 정책 할당에서 그룹을 제외할 수 있습니다. 예를 들어 **모든 회사 사용자** 그룹에 디바이스 프로필을 할당하되 **Senior Management Staff** 그룹의 구성원을 제외할 수 있습니다.

할당에서 그룹을 제외하거나, 사용자만 제외하거나, 디바이스 그룹만(그룹의 혼합 아님)만 제외하면 Intune은 사용자-디바이스 관계를 확인하지 않습니다. 디바이스 그룹을 제외하고 사용자 그룹을 포함하면 기대한 결과를 가져올 수 없습니다. 혼합 그룹을 사용하거나 다른 충돌이 있는 경우 포함이 제외보다 우선 적용됩니다.

예를 들어 키오스크 디바이스를 제외한 조직의 모든 디바이스에 디바이스 프로필을 할당하려고 합니다. **모든 사용자** 그룹을 포함하되 **모든 디바이스** 그룹을 제외합니다. 이 경우 사용자 디바이스가 **모든 디바이스** 그룹에 속하는 경우에도 모든 사용자와 해당 디바이스에 정책이 적용됩니다.

제외는 그룹의 직접 구성원만 해당하며 사용자와 연결된 디바이스는 포함하지 않습니다. 그러나 사용자가 없는 디바이스는 정책을 얻지 못합니다. 이 문제는 이 디바이스가 **모든 사용자** 그룹과 아무 관계도 없기 때문에 발생합니다.

**모든 디바이스**를 포함하고 **모든 사용자**를 제외하면 모든 디바이스에 정책이 적용됩니다. 이 시나리오의 의도는 연결된 사용자가 있는 디바이스를 이 정책에서 제외하기 위한 것입니다. 하지만 제외는 직접적인 그룹 구성원만 비교하기 때문에 디바이스는 제외하지 않습니다.

## <a name="next-steps"></a>다음 단계

프로필 및 프로필을 실행하는 디바이스를 모니터링하는 방법에 대한 지침은 [디바이스 프로필 모니터링](device-profile-monitor.md)을 참조하세요.