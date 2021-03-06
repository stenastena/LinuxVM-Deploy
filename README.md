#### Каталог VmDeploy
##### Развертывание виртуальной машины Linux в  Azure по шаблону в формате JSON

1.1)	Deploy.ps1 - Скрипт развертывания (Powershell) . Перед запуском скрипта, надо залогиниться из Powershell в вашей подписке Azure. Команда для логина стоит первой в скрипте, но закомментирована. 
Ее необходимо скопировать в среду исполнения PowerShell и запустить. 
В появившемся всплывающем окне необходимо ввести свои учетные данные в подписку Azure.
В этом файле необходимо указать свои пути к расположению шаблонов azuredeploy.json и azuredeploy.parameters.json 

1.2)    vmdeploy.azcli - Скрипт развертывания (Azure CLI) . Перед запуском скрипта, надо залогиниться из командной строки bash в вашей подписке Azure. Команда для логина стоит первой в скрипте, но закомментирована. 
Ее необходимо скопировать в среду исполнения (Командная строка Azure CLI) и запустить. 
В появившемся запросе необходимо ввести свои учетные данные в подписку Azure.
В этом файле необходимо указать свои пути к расположению шаблонов azuredeploy.json и azuredeploy.parameters.json

Для развертывания виртуальной машины, можно использовать любой из скриптов: Deploy.ps1 для среды исполнения Powershell, или vmdeploy.azcli для среды исполнения Azure CLI. 

2)	azuredeploy.json – Основной шаблон с конфигурацией виртуальной машины

3)	azuredeploy.parameters.json – Дополнительный шаблон в который вынесены наиболее часто меняемые параметры. 
В этом файле надо разместить публичный ключ, по которому будете логиниться в виртуальную машину.
   
Отдельные комментарии см. в скрипте развертывания Deploy.ps1

---

#### Каталог VmDelete
##### Удаление ранее развернутой виртуальной машины

Пример запуска скрипта:
```
DeleteVm.ps1 -VmName Имя_виртуальной_машины -RgName Имя_ресурсной_группы 
```
Если имя ресурсной группы не указано, по умолчанию принимается rgTechno (можно поменять внутри скрипта)

---

#### Каталог AzureKubernetesService
##### Создание кластера Azure Kubernetes Service (AKS)


Скрипт запуска - AKSDeploy.azcli
Запускаем из командной строки (на скрипт необходимо выдать права на исполнение). 
Предварительно должен быть установлен Azure CLI 2.0
Все параметры задаются внутри скрипта, см. комментарии.
Используется общая сеть для кластера AKS и отдельно стоящих виртуальных машин.
Виртуальная сеть при развертывании  кластера AKS не создается.
Предполагается, что ДО развертывания кластера AKS была создана виртуальная сеть (Vnet).
Сеть создается во время развертывания виртуальных машин скриптом Deploy.ps1 из каталога VmDeploy.
Т.о. последовательность такая:
1) Запускаем скрипт Deploy.ps1 из каталога VmDeploy. Помимо развертывания виртуальной машины создается общая сеть для виртуальных машин и кластера AKS;
2) Запускаем скрипт AKSDeploy.azcli из каталога AzureKubernetesService. В параметрах развертывания кластера (внутри скрипта), помимо прочего указываем имя сети и ресурсную группу где она расположена.

---

#### Каталог AzureFileShare
##### Создание файлового ресурса Azure Files


Скрипт запуска - FileShare.azcli
Запускаем из командной строки (на скрипт необходимо выдать права на исполнение). 
Предварительно должен быть установлен Azure CLI 2.0
Все параметры задаются внутри скрипта, см. комментарии
