# 안녕,webOS 오픈소스 버전!

webOS 오픈소스 버전을 소개합니다. 이 소개페이지는 여러분이 처음 앱을 개발하고 환경을<br/>
설정해주는 걸 도와줄겁니다.

## 환경설정

처음 환경설정에 대해 확인해봅니다.

webOS 오픈소스버전(이하 webOS)는 2가지 선택적 환경을 제공합니다.

- **native 환경** : 실제 환경에서 확인하고 싶은 사람들을 위해 webOS는 공식적으로 <br/>   **Raspberry pi(RPI)3 Model B**를 지원합니다.

- **virtual 환경** : RPI3를 가지고 있지 않은 개발자를 위해 가상환경을 통한 테스트를 지원합니다.<br/>webOS는 SDK의 기능중 **emulator**를 지원해 도와줍니다.

여러분은 환경에 맞추어서 webOS 이미지를 build해야 합니다.

### native 환경

- 시작하기전 [시스템 요구사항](https://www.webosose.org/docs/guides/setup/system-requirements/)을 확인합니다.

- build source code를 통해 RPI3 이미지를 만듭니다. 잘 작동하게 하기 위해<br/> [RPI3 설정](https://www.webosose.org/docs/guides/setup/building-webos-ose/#configuring-the-build-for-raspberry-pi-3)페이지를 참고합니다.

- RPI3에 build된 [이미지를 설치](https://www.webosose.org/docs/guides/setup/flashing-webos-ose/) 합니다.

- RPI3기기에 이미지를 설치했다면 주 기기와 RPI3 사이의 [네트워킹 설정](https://www.webosose.org/docs/guides/setup/setting-up-networking/)을 합니다.

### virtual 환경

- 시작하기전에 [build시스템](https://www.webosose.org/docs/guides/setup/system-requirements/#build-system-requirements), [가상환경이 실행될 OS](https://www.webosose.org/docs/guides/setup/system-requirements/#host-machine-requirements), [가상환경을 실행시킬 시스템](https://www.webosose.org/docs/tools/sdk/emulator/emulator-user-guide/#system-requirements)을 확인합니다.

- 가상환경에서 실행키기 위한 이미지를 build하세요.잘 작동하게 하기 위해 가상환경을 위한<br/> [빌드 설정](https://www.webosose.org/docs/guides/setup/building-webos-ose/#configuring-the-build-for-the-emulator)을 확인합니다.

- 가상환경을 위한 [사용자 안내](https://www.webosose.org/docs/tools/sdk/emulator/emulator-user-guide/)에 따라 설정합니다.

## 여러분의 첫 번째 webOS APP

환경설정을 마쳤다면 webOS에서 여러분의 첫번째 APP을 개발하여 실행시킬 준비가 된 것입니다.

### CLI(command line interface) 설치

web APP을 개발하기 위해서는 CLI를 사용해야 합니다. webOS의 SDK의 기능중 하나로 <br/>기본으로 제공됩니다. 여러분은 CLI를 이용해 Javascript(JS) Service도 개발 가능합니다.

여러분의 OS에 개발을 위한 [CLI를 설치하는법](https://www.webosose.org/docs/tools/sdk/cli/cli-user-guide/#installing-cli)을 소개합니다.

### web APP개발

[web APP개발을 위한 설명서](https://www.webosose.org/docs/tutorials/web-apps/developing-external-web-apps/)를 따라해 개발을 시작합니다.

## 다음은 무엇일까요?

만약 여러분이 web APP으로 감싸서 단독으로 돌아가는 JS Service에 관심이 있다면 [JS Service를 개발하기 위한 설명서](https://www.webosose.org/docs/tutorials/js-services/developing-external-js-services/)를 확인해보세요
