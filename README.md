Exemplos de clientes para RB Sphinx HMAC ZF2 API
================================================

Todos os exemplos utilizam a classe RB\Sphinx\Hmac\Zend\Client\HMACHttpClient.
Essa classe estende a Zend\Http\Client acrescentando a autenticação HMAC, sem modificar demais recursos.
Se está habituado a utilizar a Zend\Http\Client não terá problemas ao utilizar a HMACHttpClient.


### Autenticação via URI
------------------------

A autenticação mais simples para o cliente, que consiste na assinatura apenas da URI. E por essa simplicidade, nenhuma outra informação é autenticada. Todos os dados nevem constar na URI para que estejam autenticados. Dados POST, por exemplo, não estão seguros com esse método. Esse método também não é seguro contra ataques de repetição e por isso não deve ser usado para autenticar transações sensíveis a esse tipo de ataque.

A resposta enviada pelo servidor é autenticada via HEADER na resposta (como em todos os casos).


### Autenticação via HEADER (sem sessão)
----------------------------------------

Nesse modo, um HEADER HTTP é acrescentado à requisição para fazer autenticação do método (GET, POST, PUT, ...), da URI e do corpo da requisição (content). Isso inclui campos enviados via POST, arquivos e quaisquer outros dados. Mas esse método também não é seguro contra ataques de repetição.

A resposta enviada pelo servidor é autenticada via HEADER na resposta.


### Autenticação via HEADER (com sessão)
----------------------------------------

Esse modo é similar à autenticação com HEADER. A diferença está no fato de que é preciso primeiro iniciar a sessão de comunicação por HMAC. Essa sessão utiliza um contador de mensagens para garantir a ordem de processamento dessas mensagens e evitar ataques de repetição.

O início de sessão se dá por uma requisição com dois HEADER's HTTP, sem corpo na requisição (content vazio), com mesma URI e método da primeira requisição a ser enviada ao servidor/API. O servidor responderá um HEADER para confirmar o início da sessão HMAC. A partir desse ponto as requisições serão autenticadas com apenas um HEADER HMAC.

A resposta enviada pelo servidor é autenticada via HEADER na resposta.


