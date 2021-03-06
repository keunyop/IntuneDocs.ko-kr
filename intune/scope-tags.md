---
title: Microsoft Intune에서 범위 태그를 사용하여 정책 필터링 - Azure | Microsoft Docs
description: 범위 태그를 사용하여 특정 역할에 대한 구성 프로필을 필터링합니다.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/08/2019
ms.topic: article
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 57a14e1e3c4caea570667096fec71cecf2d88ddf
ms.sourcegitcommit: 916fed64f3d173498a2905c7ed8d2d6416e34061
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66045185"
---
# <a name="use-role-based-access-control-rbac-and-scope-tags-for-distributed-it"></a>분산형 IT에 RBAC(역할 기반 액세스 제어) 및 범위 태그 사용

역할 기반 액세스 제어와 범위 태그를 사용하면 올바른 관리자가 올바른 Intune 개체에 대한 올바른 액세스 권한과 가시성을 갖도록 설정할 수 있습니다. 역할은 관리자가 어떤 개체에 대해 어떤 액세스 권한을 갖는지를 결정합니다. 범위 태그는 관리자가 볼 수 있는 개체를 결정합니다.

예를 들어, 시애틀 지사 관리자에게 정책 및 프로필 관리자 역할이 할당되었다고 가정하겠습니다. 이 관리자가 시애틀 디바이스에만 적용되는 프로필과 정책만 확인하고 관리할 수 있도록 설정하려고 합니다. 이렇게 하려면 다음을 수행합니다.

1. 시애틀이라는 범위 태그를 만듭니다.
2. 정책 및 프로필 관리자 역할에 대한 역할 할당을 다음과 같이 만듭니다. 
    - 멤버(그룹) = 시애틀 IT 관리자라는 보안 그룹. 이 그룹의 모든 관리자는 범위(그룹)에 포함된 사용자/디바이스에 대한 정책과 프로필을 관리할 수 있는 권한을 갖게 됩니다.
    - 범위(그룹) = 시애틀 사용자라는 보안 그룹. 이 그룹의 모든 사용자/디바이스는 멤버(그룹)의 관리자가 관리하는 프로필 및 정책을 가질 수 있습니다. 
    - 범위(태그) = 시애틀. 멤버(그룹)의 관리자는 시애틀 범위 태그가 있는 디바이스를 볼 수 있습니다.
3. 멤버(그룹)의 관리자가 액세스할 수 있게 하려는 정책 및 프로필에 시애틀 범위 태그를 추가합니다.
4. 멤버(그룹)의 관리자에게 표시할 디바이스에 시애틀 범위 태그를 추가합니다. 


## <a name="to-create-a-scope-tag"></a>범위 태그를 만들려면

1. Intune에서 **역할** > **범위(태그)**  > **만들기**를 선택합니다.

    ![범위 태그 만들기 스크린샷입니다.](./media/scope-tags/create-scope-tag.png)

2. **이름** 및 **설명**을 제공합니다.
3. **만들기**를 선택합니다.

## <a name="to-assign-a-scope-tag-to-a-role"></a>범위 태그를 역할에 할당하려면

1. Intune에서 **역할** > **모든 역할** > 역할 선택 > **할당** > **할당**을 선택합니다.

    ![역할에 범위를 할당하는 스크린샷입니다.](./media/scope-tags/assign-scope-to-role.png)

2. **할당 이름**과 **설명**을 제공합니다.
3. **멤버(그룹)**  > **추가**를 선택하고, 이 할당의 일부로 설정할 그룹을 선택하고, **선택** > **확인**을 누릅니다. 이 그룹의 사용자는 범위(그룹)에 포함된 사용자/디바이스에 대한 정책과 프로필을 관리할 수 있는 권한을 갖게 됩니다.

    ![멤버 그룹 선택 스크린샷입니다.](./media/scope-tags/select-member-groups.png)

4. 특정 그룹 세트로 사용자/디바이스를 관리하려면, **범위(그룹)**  > **선택된 그룹** > **포함할 그룹 선택**을 선택하고 그룹 선택 > **선택** > **확인**을 누릅니다. 이 그룹의 모든 사용자/디바이스는 멤버(그룹)의 관리자가 관리하는 프로필 및 정책을 가질 수 있습니다.

    ![범위 그룹 선택 스크린샷입니다.](./media/scope-tags/select-scope-groups.png)

    또는 **모든 디바이스**, **모든 사용자** 또는 **모든 사용자 및 모든 디바이스**를 선택합니다.

    ![범위 그룹 선택에 대한 다른 옵션의 스크린샷입니다.](./media/scope-tags/scope-group-other-options.png)
    
5. **범위(태그)**  > **추가**를 선택하고, 이 역할에 추가할 태그를 선택하고, **선택** > **확인**을 누릅니다. 멤버(그룹)의 사용자는 동일한 범위 태그도 포함하는 정책 및 프로필에 대한 액세스 권한도 갖게 됩니다.

    ![범위 태그 선택 스크린샷입니다.](./media/scope-tags/select-scope-tags.png)

6. **확인**을 선택합니다. 

## <a name="to-add-a-scope-tag-to-a-configuration-profile"></a>범위 태그를 구성 프로필에 추가하려면
1. Intune에서 **디바이스 구성** > **프로필**을 선택하고, 프로필을 선택합니다.

    ![프로필 선택 스크린샷입니다.](./media/scope-tags/choose-profile.png)

2. **속성** > **범위(태그)**  > **추가**를 선택합니다.

    ![범위 태그 추가 스크린샷입니다.](./media/scope-tags/add-scope-tags.png)

3. **태그 선택**에서 프로필에 추가할 태그를 선택합니다.
4. **선택** > **확인** > **저장**을 선택합니다.

## <a name="to-assign-a-scope-tag-to-an-app-configuration-policy"></a>앱 구성 정책에 범위 태그를 할당하려면
**디바이스 등록 유형**이 **관리 디바이스**로 설정된 디바이스에 대해 다음을 수행합니다.
1. **클라이언트 앱** > **앱 구성 정책**을 선택하고 앱 구성 정책을 선택합니다.
2. **속성** > **범위(태그)** 를 선택하고 정책에 할당할 태그를 선택합니다.

**디바이스 등록 유형**이 **관리되는 앱**으로 설정된 디바이스에 대해:
1. **클라이언트 앱** > **앱 구성 정책**을 선택하고 앱 구성 정책을 선택합니다.
2. **범위(태그)** 를 선택하고 정책에 할당할 태그를 선택합니다.


## <a name="to-assign-a-scope-tag-to-an-ios-app-provisioning-profile"></a>iOS 앱 프로비저닝 프로필에 범위 태그를 할당하려면
1. Intune에서 **클라이언트 앱** > **iOS 앱 프로비저닝 프로필**을 선택하고 프로필을 선택합니다.
2. **속성** > **범위(태그)** 를 선택하고 프로필에 할당할 태그를 선택합니다.
3. **선택** > **확인** > **저장**을 선택합니다.

## <a name="to-assign-a-scope-tag-to-an-apple-volume-purchase-program-vpp-token"></a>Apple VPP(Volume Purchase Program) 토큰에 범위 태그를 할당하려면
1. Intune에서 **클라이언트 앱** > **Apple VPP 토큰**을 선택하고 VPP 토큰을 선택합니다.
2. **범위(태그)** 를 선택하고 프로필에 할당할 태그를 선택합니다. VPP 토큰과 연결된 VPP 앱 및 전자책은 할당된 태그를 상속합니다.
3. **선택** > **확인** > **저장**을 선택합니다.

## <a name="scope-tag-details"></a>범위 태그 세부 정보
범위 태그를 사용하는 경우, 다음 세부 정보를 기억해야 합니다.

- 현재 범위 태그를 할당할 수 있는 대상은 다음과 같습니다.
    - 역할 할당
    - 디바이스 준수 정책
    - 디바이스 구성 프로필
    - Windows 10 업데이트 링
    - 관리되는 디바이스
    - 앱
    - 앱 구성 정책 – 관리 디바이스
    - Powershell 스크립트
    - DEP 토큰
    - iOS 앱 프로비전 프로필
    - VPP(Volume Purchase Program) 토큰
- 관리자가 Intune에서 개체를 만들면 이 관리자에게 할당된 모든 범위 태그가 새 개체에 자동으로 할당됩니다.
- Intune RBAC는 Azure Active Directory 역할에 적용되지 않습니다. 따라서 Intune 서비스 관리자 및 전역 관리자 역할은 소유하는 범위 태그가 무엇이든 Intune에 대해 전체 관리자 액세스 권한을 갖습니다.
- 범위 태그가 있는 역할 할당의 관리자는 범위 태그가 없는 Intune 개체도 볼 수 있습니다.
- 역할 할당에 있는 범위 태그만 할당할 수 있습니다.
- 역할 할당의 범위(그룹)에 나열된 그룹만 대상으로 할 수 있습니다.
- 역할에 범위 태그가 할당되어 있으면 Intune 개체의 모든 범위 태그를 삭제할 수 없습니다. 하나 이상의 범위 태그는 필수입니다.

## <a name="next-steps"></a>다음 단계

[역할](role-based-access-control.md) 및 [프로필](device-profile-assign.md)을 관리합니다.
