## 2. Core Concepts

### Services

#### Service 개요
![image](https://github.com/seonwook97/Certificate/assets/92377162/300eff40-da48-495a-9cf8-c9b2af6f945a)
- 쿠버네티스 서비스는 애플리케이션 내부 구성요소 간 그리고 외부와의 통신을 가능하게 함
- 마이크로서비스 간의 느슨한 결합을 가능하게 함
- 주요 기능:
  - 내부 구성요소 간 통신 지원
  - 외부 사용자의 접근 지원
  - 프런트엔드와 백엔드 간 통신 지원
  - 외부 데이터 소스와의 연결 지원

#### Service 유형
![image](https://github.com/seonwook97/Certificate/assets/92377162/d08a77ea-8853-4b30-8ca0-4f96a8d6a5c0)
- **NodePort**: 노드의 포트를 통해 Pod에 접근 가능하게 함
- **ClusterIP**: 클러스터 내부 통신을 위한 가상 IP 생성
- **LoadBalancer**: 클라우드 제공자의 로드 밸런서 프로비저닝

#### NodePort Service 상세
![image](https://github.com/seonwook97/Certificate/assets/92377162/f8c3574c-3cb7-4805-889a-911f9daab7e7)
- **targetPort**: Pod의 실제 애플리케이션 포트 (예: 80)
- **port**: 서비스 자체의 포트
- **nodePort**: 노드의 외부 접근 포트 (기본 범위: 30000-32767)

#### NodePort Service YAML 파일 정의
![image](https://github.com/seonwook97/Certificate/assets/92377162/3dc2133c-da8a-4646-a938-531a1372e677)
```yaml
apiVersion: v1
kind: Service
metadata:
    name: myapp-service
spec: # Service 정의
    type: NodePort # 서비스의 유형: ClusterIP, Nodeport, LoadBalancer
    ports: # list type
     - targetPort: 80 # targetPort를 정의하지 않으면 port와 동일한 것으로 가정
       port: 80 # 필수 필드
       nodePort: 30008 # nodePort를 정의하지 않으면 30,000~32,767 자동 할당
    selector: # Pod YAML에서 labels를 참조
       app: myapp
       type: front-end

**Service 정의 파일 생성**
```sh
kubectl create –f service-definition.yml
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/edcb0e6e-0083-416c-afec-f244a6b88c97)

**Service 보기**
```sh
kubectl get services
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/66edf695-87ed-472e-bd2a-202635cd4297)

**Service 실행**
```sh
curl http://192.168.1.2:30008
```
![image](https://github.com/seonwook97/Certificate/assets/92377162/66533ce3-1639-4623-bd0d-22ce033f7a13)

**다중 Pod 지원**
![image](https://github.com/seonwook97/Certificate/assets/92377162/c2dd29ec-d38f-4aaa-8f62-39ee4c88d8f3)
- 서비스는 라벨 셀렉터를 사용하여 여러 Pod에 연결 가능
- 내장된 로드 밸런서로 무작위 알고리즘을 사용하여 트래픽 분산

**다중 Node 환경**
![image](https://github.com/seonwook97/Certificate/assets/92377162/297b6905-5288-484b-8a81-5dc1bafa7e50)
- 서비스는 자동으로 모든 노드의 동일한 nodePort에 매핑됨
- 클러스터의 모든 노드 IP와 해당 nodePort로 접근 가능
- 서비스의 유연성
  - Pod의 추가/제거 시 서비스가 자동으로 업데이트됨
  - 생성 후 추가 구성 변경이 거의 필요 없음