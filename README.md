# PHP Standard Recommendation (PSR)

_**Framework Interoperability Group (FIG)**_, formado por um grupo composto por representantes de grandes projetos PHP (CakePHP, Doctrine, Zend Framework, etc.). O objetivo desse grupo é criar padrões que todos esses projetos citados possam adotar. Tais padrões podem ser adotados em nossos projetos e são grandes os benefícios que alcançamos ao utilizá-los, tais como: código legível; facilidade de dar manutenção; interoperabilidade (componentes de um framework ou pessoa podem ser facilmente integrados em outro).

Em meio às diversas PSRs existentes, utilizando a PSR-1 e PSR-2 já teremos grandes benefícios se aplicados os padrões que ambas propõem. Sugiro que você a partir de agora comece a aplicar estes padrões e assim escreva códigos mais legíveis e elegantes. Pense no seu código como um livro no qual você é o autor. Um código bem feito traz benefícios para todos, incluindo você e sua equipe.

Fonte: [PSRs](https://www.php-fig.org/psr/)

<hr>

# PSR-PEC

Este manual tem o objetivo de centralizar alguns procedimentos que os programadores irão utilizar durante o desenvolvimento da plataforma. Este manual esta voltado para desenvolvimento com o FRAMEWORK LARAVEL.

Para auxiliar a nomeação dos recursos de acordo com as PSRs, desenvolvemos a ferramenta [Tool Extension](https://gitlab.com/Agency777/utilities) disponível no repositório **Utilities**. Veja o [tutorial](https://gitlab.com/Agency777/utilities/-/blob/master/tool-extension/tutorial/Tutorial-Tool-Extension.webm) para auxilio ao uso.


## PSR-PEC-1 :: NOMEAÇÕES

- **Nomeação:** Sejam elas variáveis, nome de classes, controllers, models, etc. Para tudo o que o usuário não vê neste projeto deverá ser nomeado na **língua Inglesa**. Portanto, utilize um tradutor como o Google Translator, caso precise.

- **Estilo:** Utilizaremos sempre o camelCase: **primeiraDefinicaoMinusculaSeguidaDeDemaisEmMaiusculo**

<hr>

## PSR-PEC-2 :: ROTAS

- **Grupos:** Para cada categoria a ser desenvolvida é criado um grupo de rotas.

- **Middleware Web:** São apenas para rotas que não utilizam auth (sem a necessidade de log).
```
Route::group(['middleware' => ['web']], function () { //outras rotas });
```

- **Moddleare Auth:** são apenas para rotas que utilizam login e precisa ter uma sessão criada para uso de demais rotas.
```
Route::group(['middleware' => ['auth']], function () { //outras rotas });
```

**Demais rotas seguem o padrão:**
```
Route::get()->name()
```

**Exemplo:**
```
Route::group(['middleware' => ['auth']], function () {
      Route::get()->name();
      Route::post()->name();
      Route::put()->name();
...
});
```

**Definição das nomenclaturas das rotas:**

- **new/model:** rota de criação (CREATE);
- **edit/model:** rota de edição (UPDATE);
- **delete/model:** rota de remoção (DELETE);
- **view/model:** rota de visualização ou chamada de uma blade (READ);

**O nome para as rotas segue a definição:** _recurso.http.nome_da_rota_

**Por exemplo:**
```
Route::get('view/users','UserController@readUser')->name('user.get.view');
```

<hr>

## PSR-PEC-2 :: CONTROLLERS

Para o desenvolvimento das controllers utilizamos o comando que já integra as dependências necessárias.
```
php artisan make:controller nome_da_controller
```
A localidade das controllers é padrão: App\Http\Controllers

- **Nomeação das Controller:** Sempre que possível estarão definidas em algum lugar como uma UML, porém, para fins de conhecimento quando necessário deixá-la o mais próximo possível do que deva fazer (Clean Code). Exemplo:

- **Ação:** cozinhar um ovo
- **Nome da controller:** EggController. O nome do recurso deve ser seguido do nome 'controller': egg é o recurso, seguido do nome Controller. Esta definição não é camel case.
- **Nome do método a mesma teoria:** cookAnEgg()

<hr>

## PSR-PEC-2 :: MODELS

Para desenvolvimento das models utilizamos comumente os comandos:
```
php artisan make:model nome_da_model
```
A localização das models é padrão do Larave 8: App\Models

<hr>

## PSR-PEC-2 :: RESOURCE

 - **VIEWs:** Será criado um diretório com o mesmo nome do recurso. Dentro dele a chamada das blades. Por exemplo:

- **Recurso:** user
- **Diretório:** view/user

Dentro de cada diretório do recurso, teremos um nome para a blade que deve seguir a ordem:
```
recurso-nome_da_rota.blade.php
```

**Como por exemplo:**

- **Recurso:** user
- **Rota:** new/user
- **Nome da blade:** view/user/user-new.blade.php
