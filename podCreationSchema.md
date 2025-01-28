1. Создание replicaset.
2. Запись в etcd.
3. Controller manager, запрос на создание пода.
4. Шедулер назначает под на ноду.
5. Далее Kubelet создает под при помощи cri.
6. Kubelet обновляет статус пода.
![изображение](https://github.com/user-attachments/assets/619498db-ac15-4152-bc62-32bfc973fc3c)
