### Домашнее задание к занятию «Продвинутые методы работы с Terraform» Сергей Баранов

### Цели задания

1. Научиться использовать модули.
2. Отработать операции state.
3. Закрепить пройденный материал.


### Чек-лист готовности к домашнему заданию

1. Зарегистрирован аккаунт в Yandex Cloud. Использован промокод на грант.
2. Установлен инструмент Yandex CLI.
3. Исходный код для выполнения задания расположен в директории [**04/src**](https://github.com/netology-code/ter-homeworks/tree/main/04/src).
4. Любые ВМ, использованные при выполнении задания, должны быть прерываемыми, для экономии средств.

------
### Внимание!! Обязательно предоставляем на проверку получившийся код в виде ссылки на ваш github-репозиторий!
------

### Задание 1

1. Возьмите из [демонстрации к лекции готовый код](https://github.com/netology-code/ter-homeworks/tree/main/04/demonstration1) для создания ВМ с помощью remote-модуля.
2. Создайте одну ВМ, используя этот модуль. В файле cloud-init.yml необходимо использовать переменную для ssh-ключа вместо хардкода. Передайте ssh-ключ в функцию template_file в блоке vars ={} .
Воспользуйтесь [**примером**](https://grantorchard.com/dynamic-cloudinit-content-with-terraform-file-templates/). Обратите внимание, что ssh-authorized-keys принимает в себя список, а не строку.
3. Добавьте в файл cloud-init.yml установку nginx.
4. Предоставьте скриншот подключения к консоли и вывод команды ```sudo nginx -t```.

![monitoring](https://github.com/12sergey12/Terraform_04/blob/main/images/ls.7.04-1.1.png)



------


### Задание 2

1. Напишите локальный модуль vpc, который будет создавать 2 ресурса: **одну** сеть и **одну** подсеть в зоне, объявленной при вызове модуля, например: ```ru-central1-a```.
2. Вы должны передать в модуль переменные с названием сети, zone и v4_cidr_blocks.
3. Модуль должен возвращать в root module с помощью output информацию о yandex_vpc_subnet. Пришлите скриншот информации из terraform console о своем модуле. Пример: > module.vpc_dev  
4. Замените ресурсы yandex_vpc_network и yandex_vpc_subnet созданным модулем. Не забудьте передать необходимые параметры сети из модуля vpc в модуль с виртуальной машиной.
5. Откройте terraform console и предоставьте скриншот содержимого модуля. Пример: > module.vpc_dev.
6. Сгенерируйте документацию к модулю с помощью terraform-docs.    
 
Пример вызова

```
module "vpc_dev" {
  source       = "./vpc"
  env_name     = "develop"
  zone = "ru-central1-a"
  cidr = "10.0.1.0/24"
}
```

![monitoring](https://github.com/12sergey12/Terraform_04/blob/main/images/ls.7.04-2.0.png)


 ------------------------------------------------
 ## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >=0.13 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_template"></a> [template](#provider\_template) | 2.2.0 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_test-vm"></a> [test-vm](#module\_test-vm) | git::https://github.com/udjin10/yandex_compute_instance.git | main |
| <a name="module_vpc"></a> [vpc](#module\_vpc) | ./vpc | n/a |

## Resources

| Name | Type |
|------|------|
| [template_file.userdata](https://registry.terraform.io/providers/hashicorp/template/latest/docs/data-sources/file) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_cloud_id"></a> [cloud\_id](#input\_cloud\_id) | https://cloud.yandex.ru/docs/resource-manager/operations/cloud/get-id | `string` | n/a | yes |
| <a name="input_default_cidr"></a> [default\_cidr](#input\_default\_cidr) | https://cloud.yandex.ru/docs/vpc/operations/subnet-create | `list(string)` | <pre>[<br>  "10.0.1.0/24"<br>]</pre> | no |
| <a name="input_default_zone"></a> [default\_zone](#input\_default\_zone) | https://cloud.yandex.ru/docs/overview/concepts/geo-scope | `string` | `"ru-central1-a"` | no |
| <a name="input_folder_id"></a> [folder\_id](#input\_folder\_id) | https://cloud.yandex.ru/docs/resource-manager/operations/folder/get-id | `string` | n/a | yes |
| <a name="input_token"></a> [token](#input\_token) | OAuth-token; https://cloud.yandex.ru/docs/iam/concepts/authorization/oauth-token | `string` | n/a | yes |
| <a name="input_vm_db_name"></a> [vm\_db\_name](#input\_vm\_db\_name) | example vm\_db\_ prefix | `string` | `"netology-develop-platform-db"` | no |
| <a name="input_vm_web_name"></a> [vm\_web\_name](#input\_vm\_web\_name) | example vm\_web\_ prefix | `string` | `"netology-develop-platform-web"` | no |
| <a name="input_vms_ssh_root_key"></a> [vms\_ssh\_root\_key](#input\_vms\_ssh\_root\_key) | ssh-keygen -t ed25519 | `string` | `"your_ssh_ed25519_key"` | no |
| <a name="input_vpc_name"></a> [vpc\_name](#input\_vpc\_name) | VPC network&subnet name | `string` | `"develop"` | no |

## Outputs


| Name | Description |
|------|-------------|
| <a name="output_external_ip_address"></a> [external\_ip\_address](#output\_external\_ip\_address) | n/a |


 ------------------------------------------


### Задание 3

1. Выведите список ресурсов в стейте.
2. Полностью удалите из стейта модуль vpc.
3. Полностью удалите из стейта модуль vm.
4. Импортируйте всё обратно. Проверьте terraform plan. Изменений быть не должно.
Приложите список выполненных команд и скриншоты процессы.

Cписок выполненных команд и вывод:

```
root@baranovsa:/home/baranovsa/terafforn-dom/ter-homeworks/04/terraf_1#  terraform state list
data.template_file.userdata
module.test-vm.data.yandex_compute_image.my_image
module.test-vm.yandex_compute_instance.vm[0]
module.vpc.yandex_vpc_network.net_name
module.vpc.yandex_vpc_subnet.subnet_name
root@baranovsa:/home/baranovsa/terafforn-dom/ter-homeworks/04/terraf_1# terraform state show module.vpc.yandex_vpc_network.net_name
# module.vpc.yandex_vpc_network.net_name:
resource "yandex_vpc_network" "net_name" {
	created_at            	= "2023-10-04T12:36:02Z"
	default_security_group_id = "enpiu3s8qlnk3cbf4mfp"
	folder_id             	= "b1gi8mor51pqsp67s6t9"
	id                    	= "enppagknnso6l1lp1gut"
	labels                	= {}
	name                  	= "develop"
	subnet_ids            	= [
    	"e9b0p36lnp2i1k7dpipn",
	]
}
root@baranovsa:/home/baranovsa/terafforn-dom/ter-homeworks/04/terraf_1#
root@baranovsa:/home/baranovsa/terafforn-dom/ter-homeworks/04/terraf_1#
root@baranovsa:/home/baranovsa/terafforn-dom/ter-homeworks/04/terraf_1# terraform state show module.vpc.yandex_vpc_subnet.subnet_name
# module.vpc.yandex_vpc_subnet.subnet_name:
resource "yandex_vpc_subnet" "subnet_name" {
	created_at 	= "2023-10-04T12:36:06Z"
	folder_id  	= "b1gi8mor51pqsp67s6t9"
	id         	= "e9b0p36lnp2i1k7dpipn"
	labels     	= {}
	name       	= "develop-ru-central1-a"
	network_id 	= "enppagknnso6l1lp1gut"
	v4_cidr_blocks = [
    	"10.0.1.0/24",
	]
	v6_cidr_blocks = []
	zone       	= "ru-central1-a"
}
root@baranovsa:/home/baranovsa/terafforn-dom/ter-homeworks/04/terraf_1#
root@baranovsa:/home/baranovsa/terafforn-dom/ter-homeworks/04/terraf_1#
root@baranovsa:/home/baranovsa/terafforn-dom/ter-homeworks/04/terraf_1# terraform state rm 'module.vpc'
Removed module.vpc.yandex_vpc_network.net_name
Removed module.vpc.yandex_vpc_subnet.subnet_name
Successfully removed 2 resource instance(s).
root@baranovsa:/home/baranovsa/terafforn-dom/ter-homeworks/04/terraf_1#
root@baranovsa:/home/baranovsa/terafforn-dom/ter-homeworks/04/terraf_1#
root@baranovsa:/home/baranovsa/terafforn-dom/ter-homeworks/04/terraf_1# terraform import module.vpc.yandex_vpc_network.net_name enppagknnso6l1lp1gut
module.vpc.yandex_vpc_network.net_name: Importing from ID "enppagknnso6l1lp1gut"...
module.vpc.yandex_vpc_network.net_name: Import prepared!
  Prepared yandex_vpc_network for import
module.test-vm.data.yandex_compute_image.my_image: Reading...
module.vpc.yandex_vpc_network.net_name: Refreshing state... [id=enppagknnso6l1lp1gut]
data.template_file.userdata: Reading...
data.template_file.userdata: Read complete after 0s [id=6defa6ccdf491d3e1f7e364227ec45825336c5d05bd589345a3f49af103099e6]
module.test-vm.data.yandex_compute_image.my_image: Read complete after 3s [id=fd8ecgtorub9r4609man]

Import successful!

The resources that were imported are shown above. These resources are now in
your Terraform state and will henceforth be managed by Terraform.

root@baranovsa:/home/baranovsa/terafforn-dom/ter-homeworks/04/terraf_1#

root@baranovsa:/home/baranovsa/terafforn-dom/ter-homeworks/04/terraf_1# terraform import module.vpc.yandex_vpc_subnet.subnet_name e9b0p36lnp2i1k7dpipn
data.template_file.userdata: Reading...
data.template_file.userdata: Read complete after 0s [id=6defa6ccdf491d3e1f7e364227ec45825336c5d05bd589345a3f49af103099e6]
module.vpc.yandex_vpc_subnet.subnet_name: Importing from ID "e9b0p36lnp2i1k7dpipn"...
module.test-vm.data.yandex_compute_image.my_image: Reading...
module.vpc.yandex_vpc_subnet.subnet_name: Import prepared!
  Prepared yandex_vpc_subnet for import
module.vpc.yandex_vpc_subnet.subnet_name: Refreshing state... [id=e9b0p36lnp2i1k7dpipn]
module.test-vm.data.yandex_compute_image.my_image: Read complete after 3s [id=fd8ecgtorub9r4609man]

Import successful!

The resources that were imported are shown above. These resources are now in
your Terraform state and will henceforth be managed by Terraform.

root@baranovsa:/home/baranovsa/terafforn-dom/ter-homeworks/04/terraf_1#
root@baranovsa:/home/baranovsa/terafforn-dom/ter-homeworks/04/terraf_1#
root@baranovsa:/home/baranovsa/terafforn-dom/ter-homeworks/04/terraf_1# terraform plan
data.template_file.userdata: Reading...
data.template_file.userdata: Read complete after 0s [id=6defa6ccdf491d3e1f7e364227ec45825336c5d05bd589345a3f49af103099e6]
module.test-vm.data.yandex_compute_image.my_image: Reading...
module.vpc.yandex_vpc_network.net_name: Refreshing state... [id=enppagknnso6l1lp1gut]
module.test-vm.data.yandex_compute_image.my_image: Read complete after 3s [id=fd8ecgtorub9r4609man]
module.vpc.yandex_vpc_subnet.subnet_name: Refreshing state... [id=e9b0p36lnp2i1k7dpipn]
module.test-vm.yandex_compute_instance.vm[0]: Refreshing state... [id=fhmhmjofjt29ri86pe0i]

No changes. Your infrastructure matches the configuration.

Terraform has compared your real infrastructure against your configuration and found no differences,
so no changes are needed.
root@baranovsa:/home/baranovsa/terafforn-dom/ter-homeworks/04/terraf_1#
```



### Задание 4*

1. Измените модуль vpc так, чтобы он мог создать подсети во всех зонах доступности, переданных в переменной типа list(object) при вызове модуля.  
  
Пример вызова
```
module "vpc_prod" {
  source       = "./vpc"
  env_name     = "production"
  subnets = [
    { zone = "ru-central1-a", cidr = "10.0.1.0/24" },
    { zone = "ru-central1-b", cidr = "10.0.2.0/24" },
    { zone = "ru-central1-c", cidr = "10.0.3.0/24" },
  ]
}

module "vpc_dev" {
  source       = "./vpc"
  env_name     = "develop"
  subnets = [
    { zone = "ru-central1-a", cidr = "10.0.1.0/24" },
  ]
}
```

Предоставьте код, план выполнения, результат из консоли YC.

### Задание 5*

1. Напишите модуль для создания кластера managed БД Mysql в Yandex Cloud с одним или тремя хостами в зависимости от переменной HA=true или HA=false. Используйте ресурс yandex_mdb_mysql_cluster: передайте имя кластера и id сети.
2. Напишите модуль для создания базы данных и пользователя в уже существующем кластере managed БД Mysql. Используйте ресурсы yandex_mdb_mysql_database и yandex_mdb_mysql_user: передайте имя базы данных, имя пользователя и id кластера при вызове модуля.
3. Используя оба модуля, создайте кластер example из одного хоста, а затем добавьте в него БД test и пользователя app. Затем измените переменную и превратите сингл хост в кластер из 2-х серверов.
4. Предоставьте план выполнения и по возможности результат. Сразу же удаляйте созданные ресурсы, так как кластер может стоить очень дорого. Используйте минимальную конфигурацию.

### Задание 6*

1. Разверните у себя локально vault, используя docker-compose.yml в проекте.
2. Для входа в web-интерфейс и авторизации terraform в vault используйте токен "education".
3. Создайте новый секрет по пути http://127.0.0.1:8200/ui/vault/secrets/secret/create
Path: example  
secret data key: test 
secret data value: congrats!  
4. Считайте этот секрет с помощью terraform и выведите его в output по примеру:
```
provider "vault" {
 address = "http://<IP_ADDRESS>:<PORT_NUMBER>"
 skip_tls_verify = true
 token = "education"
}
data "vault_generic_secret" "vault_example"{
 path = "secret/example"
}

output "vault_example" {
 value = "${nonsensitive(data.vault_generic_secret.vault_example.data)}"
} 

Можно обратиться не к словарю, а конкретному ключу:
terraform console: >nonsensitive(data.vault_generic_secret.vault_example.data.<имя ключа в секрете>)
```
5. Попробуйте самостоятельно разобраться в документации и записать новый секрет в vault с помощью terraform. 


### Правила приёма работы

В своём git-репозитории создайте новую ветку terraform-04, закоммитьте в эту ветку свой финальный код проекта. Ответы на задания и необходимые скриншоты оформите в md-файле в ветке terraform-04.

В качестве результата прикрепите ссылку на ветку terraform-04 в вашем репозитории.

**Важно.** Удалите все созданные ресурсы.

### Критерии оценки

Зачёт ставится, если:

* выполнены все задания,
* ответы даны в развёрнутой форме,
* приложены соответствующие скриншоты и файлы проекта,
* в выполненных заданиях нет противоречий и нарушения логики.

На доработку работу отправят, если:

* задание выполнено частично или не выполнено вообще,
* в логике выполнения заданий есть противоречия и существенные недостатки. 
