# FOPS-32_coursework
## Курсовой проект на профессии «DevOps-инженер с нуля»
### Установка и подготовка Terraform
Скачиваю и распаковываю последнюю стабильную версию на сентябрь 2025 г., с сайта: https://hashicorp-releases.yandexcloud.net/terraform/
```bash
wget https://hashicorp-releases.yandexcloud.net/terraform/1.13.0/terraform_1.13.0_linux_amd64.zip
zcat terraform_1.13.0_linux_amd64.zip > terraform_coursework
chmod 744 terraform_coursework
mv terraform_coursework /usr/local/bin/
terraform_coursework -version
```
![alt text](Pictures/Pic2.jpg)
