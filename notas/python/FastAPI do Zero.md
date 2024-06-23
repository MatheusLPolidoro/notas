---
sticker: lucide//fast-forward
---
[FastAPI do Zero! - FastAPI do Zero (dunossauro.com)](https://fastapidozero.dunossauro.com/)

1. **Configurando um ambiente de desenvolvimento para FastAPI**: começaremos do absoluto zero, criando e configurando nosso ambiente de desenvolvimento.
    
2. **Primeiros Passos com FastAPI e TDD**: após configurar o ambiente, mergulharemos na estrutura básica de um projeto FastAPI e faremos uma introdução detalhada ao Test Driven Development (TDD).
    
3. **Modelagem de Dados com Pydantic e SQLAlchemy**: aprenderemos a criar e manipular modelos de dados utilizando Pydantic e SQLAlchemy, dois recursos que levam a eficiência do FastAPI a outro nível.
    
4. **Autenticação e Autorização em FastAPI**: construiremos um sistema de autenticação completo, para proteger nossas rotas e garantir que apenas usuários autenticados tenham acesso a certos dados.
    
5. **Testando sua Aplicação FastAPI**: faremos uma introdução detalhada aos testes de aplicação FastAPI, utilizando as bibliotecas pytest e coverage.
    
6. **Dockerizando e Fazendo Deploy de sua Aplicação FastAPI**: por fim, aprenderemos como "dockerizar" nossa aplicação FastAPI e fazer seu deploy utilizando Fly.io.

## Arquivo de configuração ( *pyproject.toml* )

```
[tool.poetry]
name = "fast-zero"
version = "0.1.0"
description = ""
authors = ["MatheusLPolidoro <mattpolidoro4@gmail.com>"]
readme = "README.md"
  
[tool.poetry.dependencies]
python = "3.12.*"
fastapi = "^0.111.0"

[tool.poetry.group.dev.dependencies]
ruff = "^0.4.10"
pytest = "^8.2.2"
pytest-cov = "^5.0.0"
taskipy = "^1.13.0"

[tool.ruff]
line-length = 79
extend-exclude = ['migrations']

[tool.ruff.lint]
preview = true
select = ['I', 'F', 'E', 'W', 'PL', 'PT']
  
[tool.ruff.format]
preview = true
quote-style = 'single'

[tool.pytest.ini_options]
pythonpath = "."
addopts = '-p no:warnings'

[tool.taskipy.tasks]
run = 'fastapi dev fast_zero/app.py'
pre_test = 'task lint'
test = 'pytest --cov=fast_zero -vv'
post_test = 'coverage html'
lint = 'ruff check . && ruff check . --diff'
format = 'ruff check . --fix && ruff format .'

[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"
```

## CÓDIGOS DE RESPOSTA

No mundo das requisições usando o protocolo HTTP, além da resposta obtida quando nos comunicamos com o servidor, também recebemos um código de resposta (_status code_). Os códigos são formas de mostrar ao cliente como o servidor lidou com a sua requisição. Os códigos são divididos em classes e as classes são distribuídas por centenas:

- 1xx: informativo — utilizada para enviar informações para o cliente de que sua requisição foi recebida e está sendo processada.
- 2xx: sucesso — Indica que a requisição foi bem-sucedida (por exemplo, 200 OK, 201 Created).
- 3xx: redirecionamento — Informa que mais ações são necessárias para completar a requisição (por exemplo, 301 Moved Permanently, 302 Found).
- 4xx: erro no **cliente** — Significa que houve um erro na requisição feita pelo cliente (por exemplo, 400 Bad Request, 404 Not Found).
- 5xx: erro no **servidor** — Indica um erro no servidor ao processar a requisição válida do cliente (por exemplo, 500 Internal Server Error, 503 Service Unavailable).

> Para mais informações a cerca do _status code_ acesse a documentação do [iana](https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml)

Sempre que fazemos uma requisição, obtemos um código de resposta. Por exemplo, em nosso arquivo de teste, quando efetuamos a requisição, fazemos a checagem para ver se recebemos um código de sucesso, o código `200 OK`
## Contratos em APIs JSON

Quando falamos sobre o compartilhamento de JSON entre cliente e servidor, é crucial estabelecer um entendimento mútuo sobre a estrutura dos dados que serão trocados. A este entendimento, denominamos **_schema_**, que atua como um contrato definindo a forma e o conteúdo dos dados trafegados.

O ***schema*** de uma API desempenha um papel fundamental ao assegurar que ambos, cliente e servidor, estejam alinhados quanto à estrutura dos dados. Este "contrato" especifica:

- Campos de Dados Esperados: quais campos são esperados na mensagem JSON, incluindo nomes de campos e tipos de dados (como strings, números, booleanos).
- Restrições Adicionais: como validações para tamanhos de strings, formatos de números e outros tipos de validação de dados.
- Estrutura de Objetos Aninhados: como os objetos são estruturados dentro do JSON, incluindo arrays e sub-objetos.

```json
{
  "type": "object",
  "properties": {
    "message": {
      "type": "string"
    }
  },
  "required": ["message"]
}
```

