<!DOCTYPE html>
<html lang="pt-br">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fake API REST</title>
    <style>
        body {
            font-family: sans-serif;
            font-size: 16px;
        }
        
        a {
            color: blue;
            text-decoration: none;
        }
        
        a:hover {
            color: red;
            text-decoration: underline;
        }
        
        a[href="#topo"] {
            font-size: 1rem;
            font-weight: normal;
            position: relative;
            text-decoration: none;
            display: inline-block;
            padding: .1rem .3rem;
            background: #ddd;
            border-radius: .2rem;
            margin-left: .5rem;
        }
        
        h2 {
            margin-top: 2.5rem;
        }
        
        h3 {
            margin-top: 2rem;
        }
        
        h4 {
            margin-top: 1.5rem;
        }
        
        pre {
            margin-left: 2rem;
            background: #eee;
            padding: .5rem;
            display: table;
            font-size: 90%;
            color: #444;
        }
        
        blockquote {
            font-style: italic;
        }
    </style>
</head>

<body>

    <h1 id="topo">Fake API REST em Node.js</h1>
    <p>API REST fake para teste de aplicativos CRUD que consomem APIs.</p>
    <h2 id="indice">Índice <a href="#topo">&uarr;</a></h2>
    <ul>
        <li><a href="#instalando">Instalando</a></li>
        <li><a href="#exemplos">Exemplos</a></li>
        <ul>
            <li><a href="#post">post()</a></li>
            <ul>
                <li><a href="#post_request">Requisição</a></li>
                <li><a href="#post_response_ok">Resposta bem sucedida</a></li>
                <li><a href="#post_response_fail">Resposta de falha</a></li>
            </ul>
            <li><a href="#get">get()</a></li>
            <ul>
                <li><a href="#get_request">Requisição</a></li>
                <li><a href="#get_response_ok">Resposta bem sucedida</a></li>
                <li><a href="#get_response_fail">Resposta de falha</a></li>
            </ul>
            <li><a href="#put">put()</a></li>
            <ul>
                <li><a href="#put_request">Requisição</a></li>
                <li><a href="#put_response_ok">Resposta bem sucedida</a></li>
                <li><a href="#put_response_fail">Resposta de falha</a></li>
            </ul>
            <li><a href="#delete">delete()</a></li>
            <ul>
                <li><a href="#delete_request">Requisição</a></li>
                <li><a href="#delete_response_ok">Resposta bem sucedida</a></li>
                <li><a href="#delete_response_fail">Resposta de falha</a></li>
            </ul>
        </ul>
        <li><a href="#testes">Testes</a></li>
    </ul>

    <h2 id="instalando">Instalando <a href="#topo">&uarr;</a></h2>
    <ol>
        <li>Verifique se o Node.js e o NPM estão instalados;</li>
        <li>Clone o repositório;</li>
        <li>Acesse o diretório onde o repositório foi clonado;</li>
        <li>Instale as dependencias, comandando:</li>
        <pre>npm install --save</pre>
        <li>Rode o servidor, comandando:</li>
        <pre>node index.js</pre>
    </ol>

    <h2 id="exemplos">Exemplos <a href="#topo">&uarr;</a></h2>
    <p>A API suporta registros com o seguintes dados:</p>
    <ul>
        <li><code>id : [Integer]</code></li>
        <li><code>name : [String]</code></li>
        <li><code>email : [String]</code></li>
        <li><code>status : [Integer]</code></li>
    </ul>

    <h3 id="post">post() <a href="#topo">&uarr;</a></h3>
    <p>Use o método post() para inserir novos registros.</p>
    <h4 id="post_request">Requisição <a href="#topo">&uarr;</a></h4>
    <pre>http://localhost:8888/api?name=Joca da Silva&email=joca@silva.com&status=1</pre>
    <h4 id="post_response_ok">Resposta bem sucedida <a href="#topo">&uarr;</a></h4>
    <pre>{
    "status": "sucess",
    "result": "Record successfully added"
}</pre>
    <h4 id="post_response_fail">Resposta de falha <a href="#topo">&uarr;</a></h4>
    <pre>{
    "status": "fail",
    "result": "ERROR_MESSAGE"
}</pre>
    <blockquote><code>ERROR_MESSAGE</code> varia conforme o erro obtido.</blockquote>

    <h3 id="get">get() <a href="#topo">&uarr;</a></h3>
    <p>Use o método get() para listar os registros.</p>
    <h4 id="get_request">Requisição <a href="#topo">&uarr;</a></h4>
    <p>Para listar todos os registros:</p>
    <pre>http://localhost:8888/api</pre> ou
    <pre>http://localhost:8888/api?id=0</pre>
    <p>Para listar um registro específico, por exemplo, o registro com `id = 5`:</p>
    <pre>http://localhost:8888/api?id=5</pre>
    <h4 id="get_response_ok">Resposta bem sucedida <a href="#topo">&uarr;</a></h4>
    <p>Caso não encontre o(s) registro(s):</p>
    <pre>{
    "result": "No records found"
}</pre>
    <p>Se encontrar o(s) registro(s):</p>
    <pre>{
    "status": "sucess",
    "result": [
        {
            "name": "Setembrino Trocatapas",
            "email": "set@brino.com",
            "status": "1",
            "id": 1
        },
        {
            "name": "Dilermano",
            "email": "diler@mano.com",
            "status": "1",
            "id": 2
        },
        ...
    ]
}</pre>
    <h4 id="get_response_fail">Resposta de falha <a href="#topo">&uarr;</a></h4>
    <pre>{
    "status": "fail",
    "result": "ERROR_MESSAGE"
} </pre>
    <blockquote><code>ERROR_MESSAGE</code> varia conforme o erro obtido.</blockquote>

    <h3 id="put">put() <a href="#topo">&uarr;</a></h3>
    <p>Para inserir ou atualizar um registro existente.</p>
    <h3 id="put_request">Requisição <a href="#topo">&uarr;</a></h3>
    <pre>http://localhost:8888/api?id=1&name=Joca da Silva&email=joca@silva.com&status=0</pre>
    <h3 id="put_response_ok">Resposta bem sucedida <a href="#topo">&uarr;</a></h3>
    <pre>{
    "status": "sucess",
    "result": "Record successfully edited"
}</pre>
    <h3 id="put_response_fail">Resposta de falha <a href="#topo">&uarr;</a></h3>
    <pre>{
    "status": "fail",
    "result": "ERROR_MESSAGE"
}</pre>
    <blockquote><code>ERROR_MESSAGE</code> varia conforme o erro obtido.</blockquote>

    <h3 id="delete">delete() <a href="#topo">&uarr;</a></h3>
    <p>Para remover um registro.</p>
    <h4 id="delete_request">Requisição <a href="#topo">&uarr;</a></h4>
    <pre>http://localhost:8888/api?id=1</pre>
    <h4 id="delete_response_ok">Resposta bem sucedida <a href="#topo">&uarr;</a></h4>
    <pre>{
    "status": "sucess",
    "result": "Record deleted successfully"
}</pre>
    <h4 id="delete_response_fail">Resposta de falha <a href="#topo">&uarr;</a></h4>
    <pre>{
    "status": "fail",
    "result": "ERROR_MESSAGE"
}</pre>
    <blockquote><code>ERROR_MESSAGE</code> varia conforme o erro obtido.</blockquote>

    <h2 id="testes">Testes <a href="#topo">&uarr;</a></h2>
    <p>Use o <a href="https://www.postman.com/downloads/" target="_blank">Postman</a> para testar o funcionamento da aplicação.</p>

</body>

</html>