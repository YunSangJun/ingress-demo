# Ingress Demo Application

## Tea, Coffee 배포

### Deployment

```
kubectl apply -f tea.yaml
kubectl apply -f coffee.yaml
```

### Service

```
kubectl apply -f tea-svc.yaml
kubectl apply -f coffee-svc.yaml
```

## Ingress

`ingress.yaml`에 rewrite annotations을 선언합니다. ingress controller 종류에 맞게 선택합니다.

```
$ vi ingress.yaml
metadata:
  annotations:
    #nginx.org/rewrites: "serviceName=tea rewrite=/tea;serviceName=coffee rewrite=/coffee"
    #ingress.bluemix.net/rewrite-path: "serviceName=tea rewrite=/tea;serviceName=coffee rewrite=/coffee"
```

ingress를 배포합니다.
```
$ kubectl apply -f ingress.yaml
```

## 확인하기

1. `cafe.example.com/tea`

    "Which tea?" 메세지가 출력됩니다.

    클라이언트에서 `/tea`를 요청하면 `tea` 서버의 `/`로 route 됩니다.

    ```
    클라이언트 -> 서버
    /tea    -> /
    ```

2. `cafe.example.com/tea/greentea`

    "Here is a Green Tea!" 메세지가 출력됩니다.

    클라이언트에서 `/tea/greentea`를 요청하면 `tea` 서버의 `/greentea`로 route 됩니다.

    ```
    클라이언트 -> 서버
    /tea/greentea   -> /greentea
    ```

3. `cafe.example.com/others`

    "Which coffee?" 메세지가 출력됩니다.

    클라이언트에서 `/others`를 요청하면 `coffee` 서버 `/`로 route 됩니다.

    ```
    클라이언트 -> 서버
    /others    -> /
    ```

4. `cafe.example.com/others/latte`

    "Here is a Caffe Latte!" 메세지가 출력됩니다.

    클라이언트에서 `/others/latte`를 요청하면 `coffee` 서버의 `/latte`로 route 됩니다.

    ```
    클라이언트 -> 서버
    /coffee/latte   -> /latte
    ```
