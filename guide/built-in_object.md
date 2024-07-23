객체는 템플릿 엔진에서 템플릿으로 전달된다. 그리고 사용자의 코드는 객체를 전달할 수 있다. (with 와 range 문을 볼 때 예제로 확인할 수 있다.) 이후에 보게 될 tuple 함수와 같이 템플릿 내에서 새로운 객체를 만드는 몇 가지 방법이 있다.

객체는 간단히 하나의 값만 가질 수도 있다. 또는 다른 객체나 기능을 포함할 수 있다. 예를 들어, Release 객체는 (Release.Name 과 같은) 여러 객체를 포함하며 Files 객체는 몇 가지 함수를 가지고 있다.

이전 섹션에서는 템플릿에 릴리즈 이름을 삽입하기 위해 {{.Release.Name}} 을 사용하였다. Release 는 내 템플릿에 접근할 수 있는 최상위 객체 중 하나이다.

Release: 이 객체는 릴리스 자체를 서술한다. 여러 객체를 가지고 있다. 그 내부:
Release.Name: 릴리스 이름
Release.Namespace: 릴리스될 네임스페이스 (manifest에서 오버라이드하지 않은 경우)
Release.IsUpgrade: 현재 작업이 업그레이드 또는 롤백인 경우 true 로 설정된다.
Release.IsInstall: 현재 작업이 설치일 경우 true 로 설정.
Release.Revision: 이 릴리스의 리비전 번호. 설치시에는 이 값이 1이며 업그레이드나 롤백을 수행할 때마다 증가한다.
Release.Service: 현재 템플릿을 렌더링하는 서비스. Helm 에서는 항상 Helm 이다.

Values: values.yaml 파일 및 사용자 제공 파일에서 템플릿으로 전달된 값. 기본적으로 Values 는 비어 있다.

Chart: Chart.yaml 파일의 내용. Chart.yaml 안의 모든 데이터는 여기서 접근 가능하다. 예를 들어 {{ .Chart.Name }}-{{ .Chart.Version }} 은 mychart-0.1.0 를 출력한다.
사용가능한 필드는 차트 가이드 에 나열되어 있다.

기타 : https://helm.sh/ko/docs/chart_template_guide/builtin_objects/

빌트인 값은 항상 대문자로 시작한다. 이것은 Go의 명명 규칙을 따르고 있다. 사용자는 자신만의 이름의 만들때, 팀에 적합한 규칙을 자유롭게 사용할 수 있다. 쿠버네티스 차트 팀과 같은 일부 팀에서는 로컬 이름과 빌트인 이름을 구분하기 위해 첫 글자로 소문자만 사용하도록 선택한다. 이 가이드에서는 해당 규칙을 따른다.




