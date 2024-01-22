# Repositório de Templates Zabbix

Bem-vindo ao repositório de templates Zabbix! Este repositório contém uma coleção de templates construíprontos para uso no Zabbix, uma plataforma de monitoramento de código aberto amplamente utilizada.
## Como usar 
1. **Clone o Repositório:** 

```bash
git clone https://github.com/Tech-Preta/zabbix-templates.git
``` 
2. **Importe os Templates:** 
- Acesse a interface web do Zabbix.
- Navegue até "Configuração" > "Modelos". 
- Clique em "Importar" e selecione o arquivo do template desejado no diretório `templates/`. 
3. **Configuração Adicional:** 
- Alguns templates podem exigir configurações adicionais, como macros ou associação a hosts específicos. Consulte a documentação associada a cada template para obter instruções detalhadas. 
4. **Contribuições:** 
- Se você desenvolveu um novo template ou fez melhorias em um existente, ficaríamos felizes em receber suas contribuições! Abra um novo problema para discussão antes de enviar um pull request.
## Estrutura do Repositório 
- `templates/`: Contém os arquivos dos templates Zabbix. 
- `docs/`: Documentação adicional ou instruções específicas para alguns templates. 
## Lista de Templates 
1. **Template de API**  
- `templates/api_poke_template.yaml` 
2. **Template de Volumes Persistentes no Kubernetes**  
- `templates/persistent-volumes.yaml` 
3. **Template de Nginx (HTTP)**  
- `templates/nginx_by_http.yaml` 
4. **Template de Monitoramento web**  
- `templates/monitoring-web.yaml` 
5. **Template de Postgres Service**  
- `templates/psql-service.yaml`
## Notas Importantes
- Certifique-se de ajustar as configurações de cada template conforme necessário para o seu ambiente.

Esperamos que esses templates facilitem a implementação e o gerenciamento de monitoramento em seu ambiente Zabbix. Se encontrar problemas ou tiver sugestões de melhoria, não hesite em entrar em contato!

**Aproveite o monitoramento eficiente com o Zabbix!**
