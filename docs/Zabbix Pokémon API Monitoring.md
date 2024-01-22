# Zabbix Pokémon API Monitoring 

## 1. **Cadastro do Host:** 
- Abra a interface do Zabbix e vá para a seção de "Configuration" (Configuração).
- Selecione "Hosts" (Hosts) e clique em "Create Host" (Criar Host). Name: pokeapi
- Preencha os detalhes básicos do host, como nome, grupos de hosts e interfaces.

- Name: pokeapi
- Interfaces: agent
- Host groups: POKEMON


## 2. **Criação do Item:** 
- Após criar o host, vá para a seção "Items" (Itens) no menu de configuração.
- Clique em "Create Item" (Criar Item) para adicionar um novo item.
- Preencha com as seguintes informações: 

- Name: List Pokemons
- Type: HTTP agent
- Key: pokemon.list.key
- Type of information: text
- URL: https://pokeapi.co/api/v2/pokemon
- Query fields:  
- Timeout: 15s
- Request body: 
```
{"body":{"count":1292,"next":"https://pokeapi.co/api/v2/pokemon?offset=20&limit=20","previous":null,"results":[{"name":"bulbasaur","url":"https://pokeapi.co/api/v2/pokemon/1/"},{"name":"ivysaur","url":"https://pokeapi.co/api/v2/pokemon/2/"},{"name":"venusaur","url":"https://pokeapi.co/api/v2/pokemon/3/"},{"name":"charmander","url":"https://pokeapi.co/api/v2/pokemon/4/"},{"name":"charmeleon","url":"https://pokeapi.co/api/v2/pokemon/5/"},{"name":"charizard","url":"https://pokeapi.co/api/v2/pokemon/6/"},{"name":"squirtle","url":"https://pokeapi.co/api/v2/pokemon/7/"},{"name":"wartortle","url":"https://pokeapi.co/api/v2/pokemon/8/"},{"name":"blastoise","url":"https://pokeapi.co/api/v2/pokemon/9/"},{"name":"caterpie","url":"https://pokeapi.co/api/v2/pokemon/10/"},{"name":"metapod","url":"https://pokeapi.co/api/v2/pokemon/11/"},{"name":"butterfree","url":"https://pokeapi.co/api/v2/pokemon/12/"},{"name":"weedle","url":"https://pokeapi.co/api/v2/pokemon/13/"},{"name":"kakuna","url":"https://pokeapi.co/api/v2/pokemon/14/"},{"name":"beedrill","url":"https://pokeapi.co/api/v2/pokemon/15/"},{"name":"pidgey","url":"https://pokeapi.co/api/v2/pokemon/16/"},{"name":"pidgeotto","url":"https://pokeapi.co/api/v2/pokemon/17/"},{"name":"pidgeot","url":"https://pokeapi.co/api/v2/pokemon/18/"},{"name":"rattata","url":"https://pokeapi.co/api/v2/pokemon/19/"},{"name":"raticate","url":"https://pokeapi.co/api/v2/pokemon/20/"}]}}

```
- Required status codes: 200
- Update interval: 15s

- Configure os parâmetros específicos, como URL da API e parâmetros de autenticação, se necessário. 

## 3. **Criação da Discovery Rule:** 
- Vá para a seção "Discovery" (Descoberta) no menu de configuração.
- Clique em "Create Discovery Rule" (Criar Regra de Descoberta).
### Configuração da regra de descoberta:

   - Name: Descobrindo pokémons
   - Type: HTTP agent
   - Key: pokemon.discovery.key
   - URL: https://pokeapi.co/api/v2/pokemon
   -  Query fields: name:name value:bulbasaur e assim por diante.
   - Timeout: 3s
   - Request body, JSON Data:
```{
    "body": {
        "count": 1292,
        "next": "https://pokeapi.co/api/v2/pokemon?offset=20&limit=20",
        "previous": null,
        "results": [
            {
                "name": "bulbasaur",
                "url": "https://pokeapi.co/api/v2/pokemon/1/"
            },
            {
                "name": "ivysaur",
                "url": "https://pokeapi.co/api/v2/pokemon/2/"
            },
            {
                "name": "venusaur",
                "url": "https://pokeapi.co/api/v2/pokemon/3/"
            },
            {
                "name": "charmander",
                "url": "https://pokeapi.co/api/v2/pokemon/4/"
            },
            {
                "name": "charmeleon",
                "url": "https://pokeapi.co/api/v2/pokemon/5/"
            },
            {
                "name": "charizard",
                "url": "https://pokeapi.co/api/v2/pokemon/6/"
            },
            {
                "name": "squirtle",
                "url": "https://pokeapi.co/api/v2/pokemon/7/"
            },
            {
                "name": "wartortle",
                "url": "https://pokeapi.co/api/v2/pokemon/8/"
            },
            {
                "name": "blastoise",
                "url": "https://pokeapi.co/api/v2/pokemon/9/"
            },
            {
                "name": "caterpie",
                "url": "https://pokeapi.co/api/v2/pokemon/10/"
            },
            {
                "name": "metapod",
                "url": "https://pokeapi.co/api/v2/pokemon/11/"
            },
            {
                "name": "butterfree",
                "url": "https://pokeapi.co/api/v2/pokemon/12/"
            },
            {
                "name": "weedle",
                "url": "https://pokeapi.co/api/v2/pokemon/13/"
            },
            {
                "name": "kakuna",
                "url": "https://pokeapi.co/api/v2/pokemon/14/"
            },
            {
                "name": "beedrill",
                "url": "https://pokeapi.co/api/v2/pokemon/15/"
            },
            {
                "name": "pidgey",
                "url": "https://pokeapi.co/api/v2/pokemon/16/"
            },
            {
                "name": "pidgeotto",
                "url": "https://pokeapi.co/api/v2/pokemon/17/"
            },
            {
                "name": "pidgeot",
                "url": "https://pokeapi.co/api/v2/pokemon/18/"
            },
            {
                "name": "rattata",
                "url": "https://pokeapi.co/api/v2/pokemon/19/"
            },
            {
                "name": "raticate",
                "url": "https://pokeapi.co/api/v2/pokemon/20/"
            }
        ]
    }
}
```
   - Retrieve mode: Body
   - Update interval: 15s
   - Keep lost resources period: 30d

### Preprocessing
   - Preprocessing steps
     - Name: JSONPath
     - Parameters: $.results


### LLD Macros
     - {#NAME}: $.name
     - {#URL}: $.url




## 4. **Host Prototype:** 
- Ainda na seção "Discovery", clique em "Create Host Prototype" (Criar Protótipo de Host).
- Configure os detalhes do protótipo de host, como nome, grupos de host e interfaces.
     - Name: {#NAME}
     - Host groups: POKEMON
     - Interfaces:
        - Custom
        - DNS Name: {#URL}



Esses são passos gerais e você precisará adaptá-los com base nas características específicas da API dos Pokémon e nas informações que deseja monitorar. 