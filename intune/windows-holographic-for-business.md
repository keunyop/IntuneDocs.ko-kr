---
title: Microsoft Intune-Azure를 사용해 Windows Holographic 장치 관리 | Microsoft Docs
description: Microsoft Intune을 사용하여 회사 포털 구성, 준수 정책 만들기, OMA-URI 설정 사용자 지정, 앱 배포, 장치를 그룹으로 분류, 프로필 만들기, 장치 제한, 소프트웨어 업데이트 사용하도록 설정, 사용 약관 설정, VPN 및 Wi-Fi 설정 구성 및 Hello for Business 사용을 포함하여 Windows Holographic for Business를 실행하는 장치에서 다른 작업을 완료할 수 있습니다.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 4/5/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 41c1ea3bf12b83a0f09c8535275ffb58e5f46931
ms.sourcegitcommit: b727b6bd6f138c5def7ac7bf1658068db30a0ec3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="customize-devices-running-windows-holographic-with-intune"></a>Intune을 사용하여 Windows Holographic을 실행하는 장치 사용자 지정

Microsoft Intune은 [Microsoft HoloLens](https://docs.microsoft.com/en-us/hololens/)와 같이 Windows Holographic for Business를 실행하는 장치를 지원합니다.

Microsoft Intune을 사용하여 Windows Holographic을 실행하는 장치를 관리하려면 버전 업그레이드 프로필을 만들어야 합니다. 이 업그레이트 프로필은 Windows Holographic 장치를 Windows Holographic for Business로 업그레이드합니다. Microsoft HoloLens의 경우 Commercial Suite를 구입하여 업그레이드에 필요한 라이선스를 얻을 수 있습니다. 자세한 내용은 [Windows Holographic을 실행하는 장치를 Windows Holographic for Business로 업그레이드](holographic-upgrade.md)를 참조하세요.

Windows Holographic for Business를 실행하는 장치를 사용자 지정하고 관리하려면 이 문서의 작업을 사용할 수 있습니다. 예를 들어 VPN 설정 구성, 소프트웨어 업데이트 등을 관리할 수 있습니다.

## <a name="company-portal"></a>회사 포털
**[회사 포털 앱 구성](company-portal-app.md)**

Intune은 사용자가 회사 데이터 액세스하고, 장치를 등록하고, 앱을 설치하고, IT 부서에 문의하는 회사 포털을 포함합니다. Windows Holographic for Business를 실행하는 장치에 대한 회사 포털 앱을 사용자 지정할 수 있습니다.

## <a name="compliance-policy"></a>준수 정책
**[장치 준수 정책 만들기](compliance-policy-create-windows.md)**

준수 정책은 장치가 준수하려면 반드시 충족해야 할 규칙과 설정입니다. 비준수 장치용 회사 리소스에 대한 액세스를 차단하려면 조건부 액세스를 통해 이러한 정책을 사용할 수 있습니다. Intune에서 Windows Holographic for Business을 실행하는 장치에 대한 액세스를 허용하거나 차단하기 위한 준수 정책을 만들 수 있습니다. 예를 들어 Bitlocker를 사용하도록 설정할 것을 요구하는 정책을 만들 수 있습니다.

**[준수 정책 시작](device-compliance-get-started.md)** 을 참조합니다.

## <a name="deploy-apps"></a>앱 배포
**[Intune에 앱 추가](apps-add.md)**

Intune을 사용하여 Windows Holographic for Business를 실행하는 장치에 앱을 추가할 수 있습니다. 다음을 포함하여 앱을 배포하는 방법은 많습니다.

- [Microsoft Store 앱 추가](store-apps-windows.md)
- [만든 앱 추가](lob-apps-windows.md)
- [그룹에 앱 할당](apps-deploy.md)

## <a name="device-categories-and-groups"></a>장치 범주 및 그룹
**[장치를 그룹으로 분류](device-group-mapping.md)**

판매, 회계, 인사 등의 만든 범주 기반 그룹에 장치를 자동으로 추가하려면 Intune을 사용하여 장치 범주를 만들 수 있습니다. 이를 통해 Windows Holographic for Business를 실행 중인 장치 관리를 더 쉽게 할 수 있습니다.

## <a name="device-configuration-profiles"></a>장치 구성 프로필 
**[구성 프로필 시작](device-profiles.md) 및 [자신의 프로필 만들기](device-profile-create.md)**

Intune은 조직 내의 다른 장치에서 사용하거나 사용하지 않게 할 수 있는 설정 및 기능을 포함합니다. 이러한 설정 및 기능은 프로필을 사용하여 관리됩니다. 예를 들어 Cortana를 사용하도록 설정하거나 Windows Holographic for Business를 실행하는 장치에서 Windows Defender Smart Screen을 사용하는 프로필을 만들 수 있습니다.

프로필에서 OMA URI를 사용하여 일부 설정을 사용자 지정하고 장치 제한을 만들고 VPN(가상 사설망) 및 Wi-Fi를 구성할 수 있습니다.

#### <a name="custom-device-settingscustom-settings-windows-holographicmd"></a>[사용자 지정 장치 설정](custom-settings-windows-holographic.md)

OMA-URI(Open Mobile Alliance Uniform Resource Identifier) 설정을 구성하려면 Intune에서 사용자 지정 프로필을 만들 수 있습니다. OMA-URI 설정을 사용하여 VPN을 사용하도록 설정하거나 Microsoft 업데이트에서 업데이트를 검사하는 등 Windows Holographic for Business의 다양한 기능을 제어합니다.

#### <a name="device-restrictionsdevice-restrictions-windows-holographicmd"></a>[장치 제한 사항](device-restrictions-windows-holographic.md)

장치 제한을 사용하면 암호를 요구하고 [Microsoft Store](https://www.microsoft.com/store/apps/windows?icid=CNavAppsWindowsApps)에서 앱을 설치하고 Bluetooth를 사용하도록 설정하는 등 장치에서 다양한 설정과 기능을 제어할 수 있습니다. 이러한 제한 사항은 Intune 프로필에서 만듭니다. 이 프로필은 Windows Holographic for Business를 실행하는 여러 장치에 적용할 수 있습니다.

#### <a name="configure-vpnvpn-settings-configuremd"></a>[VPN 구성](vpn-settings-configure.md)

VPN(가상 사설망)을 사용하면 사용자가 회사 네트워크에 안전하게 원격으로 액세스할 수 있습니다. Intune에서 Windows Holographic for Business를 실행하는 장치에 대한 특정 설정을 포함하는 VPN 프로필을 만들 수 있습니다. 예를 들어 VPN 프로필을 만듦으로써 모든 Windows Holographic for Business 장치는 연결 유형으로 Citrix VPN를 사용할 수 있습니다.

#### <a name="configure-wi-fiwi-fi-settings-configuremd"></a>[Wi-Fi 구성](wi-fi-settings-configure.md)

또한 Windows Holographic for Business 장치에 무선 네트워크 설정을 할당하는 Intune에서 Wi-Fi 프로필을 만들 수 있습니다. Wi-Fi 프로필을 할당하면 최종 사용자는 네트워크 구성 없이도 회사 네트워크 액세스 권한을 가져옵니다. 예를 들어 Windows Holographic for Business 장치 전용 Wi-Fi 네트워크를 만들 수 있습니다.

## <a name="software-updates"></a>소프트웨어 업데이트
**[소프트웨어 업데이트 관리](windows-update-for-business-configure.md)**

Intune에는 Windows 10 장치용 업데이트 링이라는 기능이 포함되어 있습니다. 이러한 업데이트 링은 업데이트를 설치하는 방법을 결정하는 설정 그룹을 포함합니다. 예를 들어 업데이트를 설치하기 위한 유지 관리 기간을 만들거나 업데이트가 설치된 후 다시 시작을 선택할 수 있습니다. 업데이트 링은 Windows Holographic for Business를 실행하는 여러 장치에 적용할 수 있습니다.

## <a name="terms-and-conditions"></a>Terms and conditions
**[사용자 액세스에 대한 회사의 사용 약관 설정](terms-and-conditions-create.md)**

사용자가 장치를 등록하고 메일을 포함한 회사 앱에 액세스할 수 있기 전에 사용자가 회사의 사용 약관에 동의할 것을 요구할 수 있습니다. Intune에서 사용 약관이 회사 포털에 표시되는 방식을 정의하고 또한 이러한 약관을 Windows Holographic for Business를 실행하는 장치에 할당할 수 있습니다.

## <a name="windows-hello-for-business"></a>비즈니스용 Windows Hello
**[비즈니스용 Windows Hello 사용](windows-hello.md)**

비즈니스용 Hello는 Azure Active Directory 계정을 사용하여 암호, 스마트 카드 또는 가상 스마트 카드를 대신하는 대체 로그인 방법입니다. 비즈니스용 Hello를 사용하면 Windows Holographic for Business 장치는 설정한 최소 길이의 PIN으로 로그인할 수 있습니다.