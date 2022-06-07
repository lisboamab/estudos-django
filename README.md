# Django

## Repositório desse Notion:

[GitHub - lisboamab/estudos-django: meus estudos em django](https://github.com/lisboamab/estudos-django.git)

## O que é Django?

Django é um framework da linguagem de programação Python. Ele tem como objetivo utilizar Python no back-end de aplicações WEB.

O Django é baseado em projetos e apps. Os apps Django são inseridos dentro dos projetos para funcionar. Um exemplo de app é um carrinho de compras e um exemplo de projeto é o e-commerce todo, que é formado por vários apps Django.

O Django usa um modelo projeto MTV:

- Model: Mapeamento do banco de dados para o projeto;
- Template: Páginas para visualização de dados. Normalmente, é aqui que fica o HTML que será renderizado nos navegadores;
- View: Lógica de negócio. É aqui que determinamos o que irá acontecer em nosso projeto. É equivalente ao controller do padrão MVC

Os comandos para inicializar um projeto e um app Django são:

`django-admin startproject nomeDoProjeto <caminho do projeto>`

`django-admin startapp nomeDoProjeto <caminho do app>`

Caso o caminho do projeto ou app não sejam definidos o django-admin vai criar o mesmo dentro do repositorio onde foi invocado.

![Estrutura de um projeto Django](imgMD/Untitled.png)

Estrutura de um projeto Django

![Estrutura de um app Django](imgMD/Untitled%201.png)

Estrutura de um app Django

Nas imagens acima podemos observar as estruturas de um projeto e um app Django respectivamente.

### `settings.py`

Existem muitos arquivos a serem explorados mas, vamos iniciar com o arquivo `settings.py` em especial, vamos observar a variável `DEBUG = True` .

O `DEBUG = True` significa dizer que os erros que ocorrerem vão ser impressos na tela. É muito importante mudar essa variável para `False` quando for colocar o projeto para produção.

### `views.py`

Quando o `DEBUG = False` o Django busca no arquivo `views.py` o conteúdo a ser exibido na pagina. Para ser mais especifico, ele procura uma função que retorne um arquivo `index.html`.

Uma função no arquivo `views.py` se parece com:

```python
def index(request):
		return render(request, ‘index.html’)
```

As views podem ser acessadas quando existem rotas que acessam elas via arquivo `urls.py` .

### `urls.py`

É um arquivo padrão do projeto Django, esse arquivo não é criado no app Django, embora seja o mais indicado em projetos maiores.

É necessário importar aqui as funções criadas no arquivo `views.py` da seguinte forma:

```python
from <nomeDaAplicacao>.views import index, contato, login
```

Também é necessário adicionar as funções na lista `urlpatterns` que é quem vai dizer para o Django quais rotas criar.

Por padrão a lista já vem com a rota admin já criada.
No exemplo abaixo foi criado apenas as rotas para as funções `index` e `contato` .

```python
urlpatterns = [
	path('admin/', admin.site.urls),
	path('', index),
	path('contato', contato),
]
```

No codigo abaixo vamos importar a função `include` para utilizarmos o `urls.py` a partir dos apps.

```python
from django.urls import path, include

urlpatterns = [
	path('admin/', admin.site.urls),
	path('', include('<caminho do arquivo urls.py no app>'),
]
```

Agora basta criar um arquivo `urls.py` na pasta do app, importar a função path e o arquivo `views.py` do app e pronto.

## Templates

Templates no Django nada mais são que os arquivos HTML do projeto. É aquilo que o Django da de resposta para o navegador quando é requisitado o arquivo daquela determinada rota, definida lá no arquivo `[urls.py](http://urls.py)` que executa a função declarada lá no `views.py`.

Temos que adicionar o caminho do template lá no arquivo `settings.py` dentro do dicionário da variável `TEMPLATES`, na chave `DIRS`. Como podemos ver na imagem abaixo.

![Untitled](imgMD/Untitled%202.png)

 Outra configuração beeem importante é adicionar os seus apps na variável `INSTALLED_APPS` também no arquivo `settings.py` como é possível observar no print abaixo. 

![Untitled](imgMD/Untitled%203.png)

Sem isso, o Django não vai conseguir reconhecer a pasta `templates` e você vai receber um erro como: `django.template.exceptions.TemplateDoesNotExist: index.html`. Então, para que isso não aconteça, **não esqueça de adicionar seu app no `INSTALLED_APPS` OK?**

## `models.py`

models são objetos que gerenciam dados em Django. A partir dos modelos definidos, o Django cria tabelas quando conectado ao banco de dados.

É necessário que a classe que vai modelar os dados herde de `models.Model` o objeto models possui diversos metodos mas, os que vamos utilizar por enquanto são os: `CharField` `DecimalField` e o `IntegerField`. Que trabalham respectivamente com string, float e inteiros.