<div align="center">
<H1>Kubernetes Objects</H1>
</div>
<br>


## 1. Nodes (ноды, узлы)
Это физические или виртуальные машины, на которых развертываются и запускаются контейнеры с приложениями. Совокупность нод образует кластер Kubernetes.

1. Master (мастер-нода) — узел, управляющий всем кластером.
2. Worker (рабочие ноды) — узлы, на которых работают контейнеры.

## 2. Pods (Поды)
Это абстрактный объект Kubernetes, представляющий собой «обертку» для одного или группы контейнеров. Контейнеры в поде запускаются и работают вместе, имеют общие сетевые ресурсы и хранилище. Kubernetes не управляет контейнерами напрямую, он собирает их в поды и работает с ими.  
***Pod - пространство, где развертываются контейнеры. Небольшой ресурс K8s, содержащий N контейнеров.***   

Виды контейнеров в Pod:   
 - Init containers - базовые контейнеры, которые запускаются перед основными контейнерами приложений в Pods. Контейнеры инициализации могут содержать утилиты или сценарии установки, отсутствующие в образе приложения.
 - Container - контейнер с основным или второстепенным приложением.

## 3. Controllers

**1) Daemon Set (набор «демонов»).** Представляет собой совокупность «демонов» (фоновых программ, работающих без взаимодействия с пользователем) и отвечает за запуск одной реплики выбранного пода на каждом отдельном узле. То есть по мере добавления узлов в кластер добавляются и поды.

**2) Job** - контроллер, отвечающий за однократный запуск выбранного пода и завершающий его работу  

**3) CronJob** - разновидность Job, запускающая группу заданий по заданному расписанию.

**4) Stateful Set** - контоллер, используемый для управления приложениями с отслеживанием состояния. 

**5) Deployment** - предоставляет Kubernetes инструкции по изменению или созданию экземпляров Pods, содержащего контейнеризованное приложение. Управляет репликами.(создает, удаляет, обновляет)

**6) ReplicaSet** - Описывает и управляет работой нескольких подов на кластере. Чем больше таких реплик, тем выше устойчивость системы к отказам и лучше масштабируются приложения. 

## 4) Services (сервисы)  

Сервисы объединяют поды в логическую группу и определяют политику доступа к ним. По функционалу они напоминают маршрутизатор и балансировщик нагрузки между подами.

---
## Autoscalers

***Horizontal Pod Autoscaler*** - масштабирует Pods на основе различных метрик.  
Горизонтальное масштабирование означает, что в ответ на увеличение нагрузки развертывается больше Pods. Если Pods больше, чем нагрузки, то соответственно количество подов уменьшается.  
Грубо говоря, HPA будет увеличивать и уменьшать количество реплик (путем обновления развертывания), чтобы поддерживать среднюю загрузку ЦП во всех модулях на уровне 50%. Затем Deployment обновляет ReplicaSet — это часть того, как все Deployments работают в Kubernetes, — а затем ReplicaSet либо добавляет, либо удаляет Pod в зависимости от изменения своего файла  

***ReplicationController (устаревший)***  
ReplicationController гарантирует , что указанное количество реплик модуля работает одновременно. Другими словами, ReplicationController гарантирует, что модуль или набор модулей всегда будут доступны.  
Если модулей слишком много, ReplicationController завершает работу с дополнительными модулями. Если их слишком мало, ReplicationController запускает дополнительные модули. В отличие от модулей, созданных вручную, модули, поддерживаемые ReplicationController, автоматически заменяются в случае сбоя, удаления или прекращения работы.

---

<img src="https://github.com/AYaskuld/Kubernetes/blob/0b5bc95ad5c1a604683cd53deebe629edeb8f61e/images/k8s_objects.png" width="800" height="600" >