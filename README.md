# httpbin-k8s
httpbin deploy on k8s, and export httpbin service via ingress.  version( k8s 1.20.0, ingress-nginx 0.46.0)

# deploy httpbin on k8s

```
git clone https://github.com/j4ckzh0u/httpbin-k8s
cd httpbin-k8s
kubectl apply -f .
kubectl apply -f .
```

> `kubectl apply -f .`有可能需要执行2次，因为需要创建一个ns，在apply的过程中，ns的创建不是最先执行的，所以ns对应的deploy、svc、ingress会报错，再次执行即可。



# Access httpbin

> 假设ingress服务器的IP 为 `192.168.100.1`， ingress的80端口对外暴露的nodeport为`30700`
>
> test.httpbin.io为ingress中配置的服务域名， 如果不需要可以将ingress配置文件中的` host: test.httpbin.io`删除即可。

```
curl -X GET "http://test.httpbin.io:30700/get" -H "accept: application/json" --resolve "test.httpbin.io:30700:192.168.100.1"
```

使用浏览器访问，需要在本机上配置hosts文件，增加`192.168.100.1    test.httpbin.io`解析记录。

打开浏览器，访问`http://test.httpbin.io`即可访问httpbin服务。