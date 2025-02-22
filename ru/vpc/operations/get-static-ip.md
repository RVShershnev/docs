# Зарезервировать статический публичный IP-адрес

Вы можете зарезервировать публичный статический IP-адрес, чтобы потом использовать его для доступа к облачным ресурсам.

{% note info %}

Обратите внимание на [правила тарификации](../pricing.md#prices-public-ip) неактивных статических публичных адресов.

{% endnote %}

{% list tabs %}

- Консоль управления

   1. В [консоли управления]({{ link-console-main }}) перейдите на страницу каталога, в котором нужно зарезервировать адрес.
   1. В списке сервисов выберите **{{ ui-key.yacloud.iam.folder.dashboard.label_vpc }}**.
   1. На панели слева выберите ![image](../../_assets/vpc/ip-addresses.svg) **{{ ui-key.yacloud.vpc.switch_addresses }}**.
   1. Нажмите **{{ ui-key.yacloud.vpc.addresses.button_create }}**.
   1. В открывшемся окне:
       * В поле **{{ ui-key.yacloud.vpc.addresses.popup-create_field_zone }}** выберите зону доступности, в которой нужно зарезервировать адрес.
       * (опционально) В блоке **{{ ui-key.yacloud.vpc.addresses.popup-create_field_advanced }}** включите опции **{{ ui-key.yacloud.vpc.addresses.popup-create_field_ddos-protection-provider }}** и **{{ ui-key.yacloud.vpc.addresses.popup-create_field_deletion-protection }}**.
   1. Нажмите **{{ ui-key.yacloud.vpc.addresses.popup-create_button_create }}**.
  
- CLI

   {% include [include](../../_includes/cli-install.md) %}

   {% include [default-catalogue](../../_includes/default-catalogue.md) %}

   1. Просмотрите описание команды CLI для резервирования адреса:

      ```bash
      yc vpc address create --help
      ```

   1. Зарезервируйте адрес, указав зону доступности:

      ```bash
      yc vpc address create --external-ipv4 zone={{ region-id }}-a
      ```

      Результат:

      ```bash
      id: e9b6un9gkso6stdh6b3p
      folder_id: b1g7gvsi89m34pipa3ke
      created_at: "2021-01-19T17:52:42Z"
      external_ipv4_address:
        address: 178.154.253.52
        zone_id: {{ region-id }}-a
        requirements: {}
      reserved: true
      ```

      Статический публичный IP-адрес зарезервирован.

- API

  Чтобы зарезервировать статический публичный IP-адрес, воспользуйтесь методом REST API [create](../api-ref/Address/create.md) для ресурса [Address](../api-ref/Address/index.md) или вызовом gRPC API [AddressService/Create](../api-ref/grpc/address_service.md#Create).

- {{ TF }}

  {% include [terraform-definition](../../_tutorials/terraform-definition.md) %}

  Если у вас ещё нет {{ TF }}, [установите его и настройте провайдер {{ yandex-cloud }}](../../tutorials/infrastructure-management/terraform-quickstart.md#install-terraform).

  1. Опишите в конфигурационном файле параметры ресурсов, которые необходимо создать:

     * `name` — имя статического публичного IP-адреса. Формат имени:

          {% include [name-format](../../_includes/name-format.md) %}

     * `external_ipv4_address` — описание ipv4-адреса:
        * `zone_id` — [зона доступности](../../overview/concepts/geo-scope.md).

     Пример структуры конфигурационного файла:

     ```hcl
     resource "yandex_vpc_address" "addr" {
       name = "<имя статического публичного IP-адреса>"
       external_ipv4_address {
         zone_id = "<зона доступности>"
       }
     }
     ```

     Более подробную информацию о параметрах ресурса `yandex_vpc_address` в {{ TF }} см. в [документации провайдера]({{ tf-provider-link }}/vpc_address).

  1. Проверьте корректность конфигурационных файлов.

     1. В командной строке перейдите в папку, где вы создали конфигурационный файл.
     1. Выполните проверку с помощью команды:

        ```
        terraform plan
        ```

     Если конфигурация описана верно, в терминале отобразится список создаваемых ресурсов и их параметров. Если в конфигурации есть ошибки, {{ TF }} на них укажет. 

  1. Разверните облачные ресурсы.

     1. Если в конфигурации нет ошибок, выполните команду:

        ```
        terraform apply
        ```

     1. Подтвердите создание ресурсов: введите в терминал слово `yes` и нажмите **Enter**.

        После этого в указанном каталоге будут созданы все требуемые ресурсы. Проверить появление ресурсов и их настройки можно в [консоли управления]({{ link-console-main }}) или с помощью команды [CLI](../../cli/quickstart.md):

        ```
        yc vpc address list
        ```

{% endlist %}
