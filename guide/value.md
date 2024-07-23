기본 객체 중 하나는 Values이다. 이 객체는 차트로 전달된 값에 접근할 수 있게 해준다. 이 객체의 내용들은 여러 출처에서 나온다:

본 차트에 포함된 values.yaml 파일
서브 차트의 경우, 부모 차트의 values.yaml 파일
-f 플래그 (helm install -f myvals.yaml ./mychart)가 있는 helm install 또는 helm upgrade로 전달된 values.yaml 파일
--set (such as helm install --set foo=bar ./mychart)과 함께 전달된 개별 매개변수
위 목록은 적용될 값의 순서이다: 기본 값인 values.yaml은 부모 차트의 values.yaml에 의해 재정의될 수 있고, 사용자가 제공한 values.yaml 파일에 의해 재정의될 수 있으며, --set 매개변수에 의해 재정의될 수 있다.

