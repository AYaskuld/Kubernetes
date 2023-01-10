<div align="center">
<H1>Kubernetes Networking Objects</H1>
</div>
<br>

## 1. Ingress
 - **Ingress** - открывает доступ к сервису извне кластера.  
Ingress предоставляет службам маршруты HTTP и HTTPS за пределами кластера, внутри кластера. Маршрутизация трафика контролируется правилами, определенными для ресурса Ingress.

 - **Ingress Class** - ресурс Kubernetes который определяет правила маршрутизации трафика.  
Ingress могут быть реализованы разными контроллерами, часто с разной конфигурацией. Каждый Ingress должен указывать класс, ссылку на ресурс IngressClass, который содержит дополнительную конфигурацию, включая имя контроллера, который должен реализовать класс.

 - **Ingress Controllers** -  контроллер входящего трафика. 

## 2. Service
**Service** - это абстракция Kubernetes, которая, используя labels, выбирает поды, на которые следует перенаправлять трафик.  
Хотя у каждого пода есть уникальный IP-адрес, эти IP-адреса не доступны за пределами кластера без использования сервиса. Сервисы позволяют приложениям принимать трафик. Сервисы могут быть по-разному открыты, в зависимости от указанного поля type в ServiceSpec.

Для некоторых частей вашего приложения (например, внешних интерфейсов) вы можете захотеть предоставить сервису внешний IP-адрес, который находится за пределами вашего кластера.  
Kubernetes ```ServiceTypes``` позволяет вам указать, какой тип публикации нужен.  
Типы публикаций:  
 - ```ClusterIP```:  делает Service доступным только внутри кластера.  
 - ```NodePort```:  предоставляет доступ к Service по IP-адресу и статичному порту.  
 - ```Load Balancer```: предоставляет доступ к Service извне с помощью балансировщика нагрузки облачного провайдера.  
 - ```ExternalName```: сопоставляет Service с содержимым externalName поля (foo.bar.example.com, ), возвращая CNAME запись с ее значением. Проксирование не настроено.  
 
 ## 3. Pod
 **Pod** - предоставляет доступ к портам и взаимодействует с внутренними и внешними «сущностями» по средствам Endpoint и/или Endpoint Slices.  
 Network policy позволяет контролировать входящий и исходящий трафик подов.
 
 - **Endpoint** - содержит информацию об IP-адресах, портах на которые обычно ссылается служба, чтобы определить, на какие поды можно отправлять трафик.

 - **Endpoint Slices** - EndpointSlice API Kubernetes позволяет отслеживать конечные точки сети в кластере Kubernetes. EndpointSlices предлагает более масштабируемую и расширяемую альтернативу Endpoints.  
Cодержит ссылки на набор конечных точек сети. Управление службами автоматически создает EndpointSlices для любой службы Kubernetes, имеющей селектор.

- **Network policy** - позволяет вносить в белый список вхоящий и исходящий трафик в Pods. 
  - Контролирует поток трафика на уровне IP-адреса или порта (уровень 3 или 4 OSI).
  - Указывает, как pod разрешено взаимодействовать с различными сетевыми «сущностями».

---

<img src="https://github.com/AYaskuld/Kubernetes/blob/af0c173c8e30a62f56c8bf3889e808b7c793a630/images/k8s_network_objects.jpg" width="1000" height="600" >