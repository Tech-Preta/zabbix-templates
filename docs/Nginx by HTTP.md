# Monitoramento Nginx by HTTP

Este documento fornece informações sobre o monitoramento do Nginx no host `zbx-zabbix-zabbix-web` usando o Zabbix.

## Configuração do Host

- **Nome do Host:** `zbx-zabbix-zabbix-web`
- **Template Utilizado:** `Nginx by HTTP`
- **Grupo de Hosts:** `Zabbix servers`
- **Interface:** `Agent`
- **DNS name:** `zbx-zabbix-zabbix-web.my-zabbix.svc.cluster.local`

## Macros Configuradas

- `{$NGINX.DROP_RATE.MAX.WARN}`: 1
- `{$NGINX.RESPONSE_TIME.MAX.WARN}`: 30
- `{$NGINX.STUB_STATUS.PATH}`: basic_status
- `{$NGINX.STUB_STATUS.PORT}`: 80
- `{$NGINX.STUB_STATUS.SCHEME}`: http

## Métricas Habilitadas

1. **Nginx by HTTP: Nginx: Get stub status page:**
   - Coleta informações do arquivo stub do Nginx no caminho `basic_status`.

2. **Nginx: Service status:**
   - Monitora o status geral do serviço Nginx.

3. **Nginx: Service response time:**
   - Mede o tempo de resposta do serviço Nginx.

## Configuração Adicional

- **Alertas:**
  - Configurou alertas com base nas seguintes macros:
    - Drop rate máximo: 1
    - Tempo de resposta máximo: 30



## Verificação

- Certifique-se de que o host `zbx-zabbix-zabbix-web` está ativo.
- Monitore o painel do Zabbix para garantir a coleta de métricas.

## Referências

- Consulte a [documentação oficial do Zabbix](https://www.zabbix.com/documentation/current/pt/manual/config/items/itemtypes/http) para obter informações adicionais e suporte.

