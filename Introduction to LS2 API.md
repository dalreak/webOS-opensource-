# LS2 API에 대해 소개합니다!

**LS2 API**는 webOS환경에서 제공되는 JSON을 기반으로 한 API입니다. 여러분은 LS2 API을 이용해 webOS Platform에서 돌아가는 APP또는 Service를 만들 수 있습니다.

LS2 API를 사용하고 있는 [com.webos.service.systemservice](https://www.webosose.org/docs/reference/ls2-api/com-webos-service-systemservice/)(이하 basic Service)를 이용해<br/> 기본적인 설명을 여러분에게 하려고 합니다. basic Service는 시스템의 preference나 시간/시간대에 대한 정보를 변경하게 도와주는 Service입니다.

## 기본 소개

여러분은 핵심을 따라 오다 보면 LS2 API를 사용가능하게 도와줄겁니다.

### Service URI

Service URI는 일종의 특별한 주소로서 Luna Bus라는 걸 통해 plaform Service에 접근<br/> 가능하게 해줍니다.service URI는 ```luna://<service name>```형태로 사용됩니다.

반대로 client들 또한 service URI를 통해 basic Service에 요청할 수 있습니다. Service URI는<br/> ```luna://com.webos.service.systemservice```입니다.

### Method

각각의 Service들은 한개 혹은 그 이상의 Method를 가지고 기능들을 제공합니다.Method들은 보통<br/> root의 기능에 묶여 Service됩니다. 만약 root범주에 있지 않은 Method들은 특별한 기능을 하는<br/>것과 묶입니다.

```com.webos.service.systemservice```의 기능중 preference의 설정을 가져오거나 변경가능하게 해주는 root아래에 있는 method를 소개합니다.

- ```getPreferences```
- ```setPreferences```

또 ```com.webos.service.systemservice```가 제공하는 시간관련 method를 소개합니다. 이 method를 통해 system의 시간을 가져오거나 설정할 수 있습니다.

- ```time/getSystemTime```

- ```time/setSystemTime```

### Parameter

Parameter는 JSON object를 통한 service의 옵션을 변경하는 기능입니다.Parameter는 Serviece로 요청할 때 약속된 속성들로 이루어져 있습니다.

예를 들어 약속된 속성중 하나는 subscribe속성입니다.어느 Service로 허용된 요청을 하고 그 요청이 성공하였을 경우 주기적으로 또는 정보가 새로고침되었을 경우 답을 해옵니다.

다음 설명은 ```com.webos.service.systemservice```의 시간 관련 method를 성명합니다

- ```time/getSystemTime```
 - method는 입력 parameter를 필요로 하지 않습니다.
 - ```subscribe```속성의 경우 필요에 따라 넣을 수 있습니다.

- ```time/setSystemTime```
 - method는 필수 입력 parameter로 ```utc(Coordinated Universal Time)```속성을 필요로 합니다.
 - ```timestamp```object를 필요에 따라 넣을 수 있습니다.

### Call Response

Call Response(요청 응답내용)은 Json object로 이루어진 method call에 대한 응답 data이다. 요청이 성공 또는 실패에 따라 ```returnValue```라는 약속된 속성이 변경된다.

- ```returnValue```의 값이 true일경우 API call의 응답내용이 응답object에 추가되어서 같이 들어옵니다.
 - 만약 ```subscribe```속성의 parameter가 true로 설정되어 있을경우 ```subscribed```는 응답object에서 subcription의 성공 유무를 나타냅니다. 만약 ```subcribed```가 true로 올경우 subcription은 성공한 것입니다.

- ```returnValue```가 false를 반환할경우 ```errorCode```그리고 ```errorText```과 같은 속성이 error에 대한 정보를 제공합니다.

### Subscription Response

subcription 응답은 JSON object로 이루어져 있습니다. 2개의 정해진 속성을 반환하는데 ```subcribed```와 ```returnValue```가 반환됩니다. 각각 ```subcribed```는 subcription상태를 나타내고 ```returnValue```의 경우 명령의 상태를 나타냅니다.

## LS2 API의 기본 사용법

LS2 API의 기본 사용법을 소개합니다.

### 호출 Method

method를 사용해 client도 platform service를 요청할 수 있습니다. 응답으로 정해진 JSON object가<br/> 옵니다.

```time/getSystemTime``` method를 사용되는걸 보여줍니다. [luna-send](https://www.webosose.org/docs/tools/commands/luna-send/) 명령을 사용하여 적절한 method URI(**\<service URI>/\<method name>**)를 보내줍니다. `time/getSystemTime` method의 경우 method <br/>URI는 `luna://com.webos.service.systemservice/time/getSystemTime`가 됩니다.

```
$ luna-send -n 1 -f luna://com.webos.service.systemservice/time/getSystemTime '{}'

Call response:
{
    "timezone": "Asia/Seoul",
    "returnValue": true,
    "utc": 1557280839,
    "localtime": {
        "month": 5,
        "day": 8,
        "hour": 11,
        "minute": 0,
        "year": 2019,
        "second": 39
    },
    "TZ": "KST",
    "systemTimeSource": "ntp",
    "timestamp": {
        "source": "monotonic",
        "sec": 730,
        "nsec": 472935963
    },
    "timeZoneFile": "/var/luna/preferences/localtime",
    "offset": 540,
    "isDST": false
}
```

> **추가설명: luna-send의 마지막 '{}'는 parameter가 없다고 명시하는 뜻으로 사용된다**

### 알림을 위한 Subscribing

client는 몇가지 method의 알림을 subcribe할 수 있다. client가 subscription 요청을 method를 통해하게 되는데 보통 변경되거나 최신의 정보가 필요한 경우 사용한다.

> **대부분의 경우 subcription은 `subcribe`라는 parameter을 통해 지원되는데 몇몇의 method의 경우 `subcribe`속성 없이 subscription만 가능한경우도 있다.**

luna-send 명령을 사용해 `time/getSystemTime` method를 subscribing 해보겠다. 테스트 subscription을 위해 luna-send에 `-i`옵션을 이용해 반응형으로 실행한다.

```
$ luna-send -i -f luna://com.webos.service.systemservice/time/getSystemTime '{"subscribe": true}'

Call response:
{
    "timezone": "Asia/Seoul",
    "returnValue": true,
    "utc": 1561617075,
    "localtime": {
        "month": 6,
        "day": 27,
        "hour": 15,
        "minute": 31,
        "year": 2019,
        "second": 15
    },
    "subscribed": true,
    "TZ": "KST",
    "systemTimeSource": "ntp",
    ...
}
```

## 다음은 무엇일까요?

- LS2 API를 어떻게 앱과 서비스에 적용시키는지 이 페이지를 통해 확인해 확인해보세요
 - [LS2 API 웹앱에서 써보기](https://www.webosose.org/docs/guides/development/web-apps/using-ls2-api-in-web-apps/)
- LS2 API를 자세하게 살펴보고 [LS2 API reference](https://www.webosose.org/docs/reference/ls2-api/ls2-api-index/)를 참고해보세요
