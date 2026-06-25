# Algar Serasa API — CRMB2B-94

## O que faz
API MuleSoft que intermedia a consulta Serasa para o Salesforce.
O Salesforce chama esta API via Named Credential, e esta API chama a Serasa real.

## Contrato
```
GET /api/serasa/v1/consulta/{cnpj}

Response 200:
{
  "razaoSocial": "...",
  "nomeFantasia": "...",
  "situacaoCnpj": "ATIVA",
  "dataFundacao": "1998-01-15",
  "codigoCnaeFiscal": "6110803",
  "codigoNaturezaJuridica": "2062",
  "inscricaoEstadual": "...",
  "ufRegistroIe": "MG",
  "situacaoRegistroIe": "HABILITADA",
  "porte": "GRANDE",
  "endereco": { "logradouro", "numero", "bairro", "cidade", "uf", "cep" }
}

Response 404: CNPJ nao encontrado
Response 504: Timeout Serasa
```

## Deploy CloudHub
```bash
mvn deploy -DmuleDeploy -Danypoint.username=albertobneto -Danypoint.password=***
```

## Configuracao
Editar `src/main/resources/application.properties`:
- `serasa.host` / `serasa.basePath` / `serasa.apiKey` — endpoint real Serasa
- Para mock: apontar para `mcp-sf-provisioning-462dd29c2455.herokuapp.com`

## Apos deploy no CloudHub
No Salesforce, alterar Named Credential `MuleSoft_Serasa`:
- URL: `https://algar-serasa-api.cloudhub.io/api/serasa/v1/consulta/`
