
# Monitoramento de Banco de Dados no Kubernetes com Zabbix

Este repositório contém informações e configurações para monitorar bancos de dados em ambientes Kubernetes usando o Zabbix. O monitoramento é realizado através de um item de verificação simples utilizando a chave `net.tcp.service[{$PROTOCOL},{$HOST},{$PORT}]`, onde as macros `{$HOST}`, `{$PORT}` e `{$PROTOCOL}` são utilizadas dinamicamente para obter informações do ambiente Kubernetes.
## Pré-requisitos
- Um ambiente Kubernetes em execução.
- Um servidor Zabbix configurado e acessível para o ambiente Kubernetes.
- Um agente Zabbix instalado no namespace que hospeda o banco de dados.
## Estrutura do Projeto

O projeto está organizado da seguinte maneira:


```lua
zbx/
|   |-- templates/
|       |-- psql-service.yaml

 
O diretório `zbx/templates/` agora contém os arquivos de modelos específicos do Zabbix. Certifique-se de ajustar as referências e configurações no seu ambiente de acordo com essa estrutura atualizada.


1. Faça o download e importe o template:

```bash
cd ~/templates/psql-service.yaml
```

## Personalização

### Criando do zero um monitoramento simples
- Na console do Zabbix vá para Configuration > create host - utilize como interface o Agent, escolha como conexão o DNS e em DNS name iremos usar o DNS interno do Kubernetes  <namespace>.<service-name>svc.cluster.local.

- Adicione as macros {$PROTOCOL}, {$HOST} e {$PORT} para serem usadas dinâmicamente pelo nosso item.

- Depois de possuir o host cadastrado com as informações necessárias, iremos criar o nosso item. Clique em items > create item > em type selecione simple check, em key adicione net.tcp.service[{$PROTOCOL},{$HOST},{$PORT}], defina o intervalo de verificação e adicione ao host. 

- Volte ao host e clique em trigger > create trigger, dê um nome a sua trigger, utilizei PSQL service is down on {HOST.NAME}, escolha o nível de severidade e construa a sua expressão, utilizei:

```
max(/zbx-zabbix-postgresql/net.tcp.service[{$PROTOCOL},{$HOST},{$PORT}],#3)=0
```

## Por que monitorar a porta do banco?

A monitoração da porta permite verificar se o serviço do PostgreSQL está em execução e disponível. Caso a porta não esteja acessível, serei alertada do problema na minha stack de monitoramento no ambiente Kubernetes, me permitindo atuar rapidamente para solução do problema. 


## Bônus

- Crie uma Action para ser notificado sobre um problema no seu banco de dados. Em Configuration > Actions > Trigger Actions. Dê um nome para sua trigger > escolha o tipo, no meu caso utilizei Trigger severity com operator is greater than or equals e severidade High.

- Em operações personalize o alerta, escolha o usuário responsável por enviar o alerta e o tipo de alerta. Certifique-se de ter um media type configurado. No meu caso, utilizei o e-mail.

## Observações
- Certifique-se de que o servidor Zabbix esteja configurado para aceitar conexões dos agentes nos pods do Kubernetes. 
- O item de verificação utiliza a chave `net.tcp.service[{$PROTOCOL},{$HOST},{$PORT}]`, e as macros são dinamicamente preenchidas com informações do Kubernetes.
