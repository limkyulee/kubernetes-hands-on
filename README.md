# Kubernetes Hands-on

Kubernetes 기본 리소스를 직접 작성하고 적용해 보는 실습용 저장소입니다.

현재는 단일 Pod 매니페스트 예제를 포함합니다.

## 프로젝트 구조

```text
.
├── kubernetes/
│   ├── nginx.yaml   # nginx Pod 예제
│   └── pod.yaml     # my-app Pod 예제
└── settings.json    # YAML 스키마 설정
```

## 사전 준비

- Kubernetes 클러스터
  - Docker Desktop Kubernetes, minikube, kind 등
- `kubectl`
- 현재 컨텍스트가 실습용 클러스터를 바라보도록 설정

```bash
kubectl config current-context
kubectl cluster-info
```

## 매니페스트 적용

### nginx Pod 생성

```bash
kubectl apply -f kubernetes/nginx.yaml
```

생성 상태 확인:

```bash
kubectl get pods
kubectl describe pod nginx
```

### my-app Pod 생성

```bash
kubectl apply -f kubernetes/pod.yaml
```

`kubernetes/pod.yaml`은 `my-app:latest` 이미지를 사용합니다. 해당 이미지는 저장소 안에서 빌드되지 않으므로, 로컬 클러스터에서 접근 가능한 이미지로 준비하거나 매니페스트의 `image` 값을 변경해야 합니다.

상태 확인:

```bash
kubectl get pod my-app
kubectl describe pod my-app
```

## 로그 확인

```bash
kubectl logs nginx
kubectl logs my-app
```

## 리소스 삭제

```bash
kubectl delete -f kubernetes/nginx.yaml
kubectl delete -f kubernetes/pod.yaml
```

## 파일 설명

| 파일 | 설명 |
| --- | --- |
| `kubernetes/nginx.yaml` | `nginx` 이미지를 사용하는 `nginx` Pod 정의 |
| `kubernetes/pod.yaml` | `my-app:latest` 이미지를 사용하는 `my-app` Pod 정의 |
| `settings.json` | Kubernetes YAML 스키마 매핑 설정 |

## 참고 명령어

```bash
kubectl get pods -o wide
kubectl get events --sort-by=.metadata.creationTimestamp
kubectl describe pod <pod-name>
kubectl delete pod <pod-name>
```
