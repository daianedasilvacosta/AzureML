# automl-microsoft-azure
- Experimentos de aprendizagem e regressão automatizados passo a passo usando o Azure Machine Learning.
- Feito desafio de projeto no Bootcamp Microsoft Azure AI Fundamentals Na [Dio.me](https://www.dio.me/) com [Documentação](https://aka.ms/ai900-auto-ml).
<br>

## Passo 1
- Criar uma conta no [https://azure.microsoft.com/pt-br/free].
- O cadastro é criado quando clicar nesse botão "Experimentar gratuitamente" (É preciso dizer um número de cartão de crédito).

![Screenshot_1](https://github.com/daianedasilvacosta/AzureML/assets/78669491/9e65c1d6-750d-4045-ac85-7d041625b8a9)
<br>

## Passo 2
- Entrar na plataforma do [Portal Azure](https://portal.azure.com).
- Pesquisar por "Azure Machine Learning" nesse campo de pesquisa selecionar Azure Machine Learning.

![Screenshot_2](https://github.com/daianedasilvacosta/AzureML/assets/78669491/8b43ab63-3915-4610-928f-3c2dd47389de)
<br>

## Passo 3
- Apertar em "Criar", para criar um Novo workspace.

![passo3](https://github.com/daianedasilvacosta/AzureML/assets/78669491/0be8686d-f1d4-4e94-9c23-29ba167f9f82)
<br>

## Passo 4
- Criar um novo "resource group", criar um "nome", a "região", e Apertar o botão "Examinar + criar".

![passo4](https://github.com/daianedasilvacosta/AzureML/assets/78669491/4b85fa0b-8ac0-481c-9230-6343c456b8af)

- Depois espere até que a validação ser aprovada, e então Apertar o botão "criar".
<br>

## Passo 5
- A implantação está em andamento e depois de finalizar o deploy pode apertar o botão de "ir para o recurso".

![Screenshot_5](https://github.com/daianedasilvacosta/AzureML/assets/78669491/e7644772-7fd3-4de4-96f7-932705cb54c0)
<br>

## Passo 6
- O diretório do workspace é então aberto.
- Posso visualizar todos os workspaces existentes, Apertando em "Todos os Espaços de Trabalho".

![passo6](https://github.com/daianedasilvacosta/AzureML/assets/78669491/97bc338c-0372-4aee-8fbc-f14631ba2468)

## Passo 7
- O workspace escolhido é aberto. Aperte no ambiente "ML automatizado" e Apertar em criar um "Novo trabalho de ML automatizado".

![passo7](https://github.com/daianedasilvacosta/AzureML/assets/78669491/8c748e02-cfcc-4faa-8af2-da71b8e0ba97)
<br>

- Swagger do serviço implantado

## Códigos
<details exit>
  <summary> Entrada </summary>
  
 ```
 {
   "Inputs": { 
     "data": [
       {
         "day": 1,
         "mnth": 1,   
         "year": 2022,
         "season": 2,
         "holiday": 0,
         "weekday": 1,
         "workingday": 1,
         "weathersit": 2, 
         "temp": 0.3, 
         "atemp": 0.3,
         "hum": 0.3,
         "windspeed": 0.3 
       }
     ]    
   },   
   "GlobalParameters": 1.0
 }

```
</details>

<details exit>
  <summary> Resultado</summary>
  
 ```
{
  "Results": [
    389.336520171
  ]
}

```
</details>

<details exit>
  <summary> Swagger URI</summary>
  
 ```
// http://fae0ce06-e8d3-48de-aa8e-838946f98dbd.eastus.azurecontainer.io/swagger.json

swagger: '2.0'
info:
  title: products
  description: API specification for the Azure Machine Learning service products
  version: '2.0'
schemes:
  - https
consumes:
  - application/json
produces:
  - application/json
securityDefinitions:
  Bearer:
    type: apiKey
    name: Authorization
    in: header
    description: 'For example: Token Bearer abc123'
paths:
  /:
    get:
      operationId: ServiceHealthCheck
      description: Simple health check endpoint to ensure the service is up at any given point.
      responses:
        '200':
          description: If the service is operational, this response will be returned with the content.
          schema:
            type: string
          examples:
            application/json: Healthy
        default:
          description: The service failed to execute due to an error.
          schema:
            $ref: '#/definitions/ErrorResponse'
  /score:
    post:
      operationId: RunMLService
      description: Run web service's model and get the prediction output
      security:
        - Bearer: []
      parameters:
        - name: serviceInputPayload
          in: body
          description: If the service is operational, this response will be returned with the content
          schema:
            $ref: '#/definitions/ServiceInput'
      responses:
        '200':
          description: The service processed the input correctly and provided a result prediction, if applicable.
          schema:
            $ref: '#/definitions/ServiceOutput'
        default:
          description: The service failed to execute due to an error.
          schema:
            $ref: '#/definitions/ErrorResponse'
definitions:
  ServiceInput:
    type: object
    properties:
      Inputs:
        type: object
        required:
          - data
        properties:
          data:
            type: array
            items:
              type: object
              required:
                - day
                - mnth
                - year
              properties:
                day:
                  type: integer
                  format: int64
                mnth:
                  type: integer
                  format: int64
                year:
                  type: integer
                  format: int64
            format: pandas.DataFrame:records
      GlobalParameters:
        type: number
        format: double
    example:
      Inputs:
        data:
          - day: 0
            mnth: 0
            year: 0
      GlobalParameters: 1
  ServiceOutput:
    type: object
    required:
      - Results
    properties:
      Results:
        type: array
        items:
          type: integer
          format: int64
        format: numpy.ndarray
    example:
      Results:
        - 0
  ErrorResponse:
    type: object
    properties:
      message:
        type: string

```
# AzureML
