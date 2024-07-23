# k8s_helm_practice
쿠버에서 helm 쓰는거 잠깐 스터디
*쿠버 자체는 알고 있단 전재로 helm과 엮이는 거만 주로 설명

1. 임의로 차트 만듬 

```bash
helm create mychart 
```

2. mychart/templates 훑어보기

NOTES.txt : 차트 도움말. helm install 실행할때 표시된다 함
deployment.yaml : 디플로이먼트 기본 양식
service.yaml : 서비스 기본 양식
(마찬가지로 hpa나 이런거도 오토스케일링 기본~~~)
_helpers.tpl : 차트 전체에서 다시 사용할 수 있는 템플릿 헬퍼를 지정하는 공간

3. 직접 작성해보게 지움

```bash
rm -rf mychart/templates/*

```

4. configmap 작성

5. (그냥 해봐)
```bash
helm install full-coral ./mychart
```

6. 
```bash
helm get manifest full-coral
```

7. install 이란 명령어로 저 차트를 설치할 수 있고 get manifest 해보면 올라간거 확인이됨...

설명 : helt get manifest 명령은 릴리스 이름(full-coral)을 가지고 서버에 업로드된 쿠버네티스 리소스를 모두 출력한다. 각 파일은 ---로 시작하여 YAML 문서의 시작을 표시한 다음 자동으로 생성된 주석이 나타나 이 YAML 문서를 생성한 템플릿 파일을 알려준다.

여기서 이 YAML 데이터가 정확히 configmap.yaml 파일에 입력한 것임을 알 수 있다.

8. 삭제
```bash
helm uninstall full-coral
```

9. configmap.yaml 수정 
name: {{ .Release.Name }}-configmap 
요런식으로 이름자리에 들어갈 값을 따로 지정함
템플릿 지시문 {{ }} 요거로 감싼다

10. .Release 로 시작하는데 Release는 헬름 내장객체 (내가 정의한 객체는 values.yaml에 넣음 보통)

```bash
helm install clunky-serval ./mychart
helm get manifest clunky-serval
```
11. 템플릿을 실제 환경 없이 렌더링 테스트 하고 싶다면

```bash
helm install --debug --dry-run goodly-guppy ./mychart
```

주의 : --dry-run 을 사용하면 코드를 쉽게 테스트할 수 있지만, 쿠버네티스가 당신이 만든 템플릿을 받아들일지는 확신할 수 없을 것이다. --dry-run 이 작동됐다는 이유로 차트가 설치될 것이라고 생각하지 않는 것이 가장 좋다.

실제로는 자원적 여유가 된다면 EKS등 환경에서는 테스트용 클러스터나, 테스트용 네임스페이스를 할당하고 테스트를 해보는게 안전할듯? 드라이런은 실 쿠버환경에서 오류가 없을거라 보장이 안되나봄 - 다만 여기서 조차 걸리는 기본적인 에러들을 체크는 되것지.

