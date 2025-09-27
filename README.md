# FOPS-32_coursework
## Курсовой проект на профессии «DevOps-инженер с нуля»
### Установка и подготовка Terraform
Скачиваю и распаковываю последнюю стабильную версию на сентябрь 2025 г., с сайта: https://hashicorp-releases.yandexcloud.net/terraform/
```bash
wget https://hashicorp-releases.yandexcloud.net/terraform/1.13.0/terraform_1.13.0_linux_amd64.zip
zcat terraform_1.13.0_linux_amd64.zip > terraform
chmod 744 terraform
mv terraform /usr/local/bin/
terraform -version
```
![alt text](Pictures/Pic2.jpg)

Создаю файл ```.terraformrc``` и добавляю блок с источником, из которого будет устанавливаться провайдер.
```bash
sudo nano ~/.terraformrc
```
```bash
provider_installation {
  network_mirror {
    url = "https://terraform-mirror.yandexcloud.net/"
    include = ["registry.terraform.io/*/*"]
  }
  direct {
    exclude = ["registry.terraform.io/*/*"]
  }
}
```
![alt text](Pictures/Pic1.jpg)

Для файла с метаданными, ```meta.yaml```, необходим публичный SSH-ключ для доступа к ВМ. Для Yandex Cloud рекомендуется использовать алгоритм Ed25519. Ссылка: https://cloud.yandex.ru/ru/docs/glossary/ssh-keygen
```bash
ssh-keygen -t ed25519
```
![alt text](Pictures/Pic3.jpg)

Создаю файл meta.yaml с данными пользователя на создаваемые ВМ.
```sudo nano ~/meta.yaml```
```bash
#cloud-config
 users:
  - name: shcherbatykh
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-ed25519
```
![alt text](Pictures/Pic4.jpg)

Создаю playbook Terraform c блоком провайдера.
```sudo nano ~/main.tf```
```bash
terraform {
  required_providers {
    yandex = {
      source = "yandex-cloud/yandex"
    }
  }
}
```
![alt text](Pictures/Pic5.jpg)

Инициализирую провайдера ```terraform init```

![alt text](Pictures/Pic6.jpg)

