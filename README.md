<p align="left">
<span> • </span>
    <span>
        Português
    </span>
    <span> • </span>
    <a href="README_en.md">
        English
    </a>
</p>

# Propósito
A intenção deste repositório é possibilitar que qualquer pessoa tenha seu próprio servidor [Electrum](https://github.com/spesmilo/electrum), usando [Electrs](https://github.com/romanz/electrs ) e [Docker](https://www.docker.com/) de maneira rápida e fácil.

## Introdução rápida
Uma carteira Electrum geralmente se conecta a um servidor público vinculado a um nó de Bitcoin para realizar ações na rede, com seu próprio servidor electrum conectado ao seu próprio nó, você acaba se tornando completamente auto-soberano sobre suas ações na rede Bitcoin.

## Você precisa ter
- [Nó Bitcoin](https://github.com/bitcoin/bitcoin)
- [Docker](https://www.docker.com/)
- [Git](https://git-scm.com/)

## Rodando
Execute:
```
curl -sSL https://raw.githubusercontent.com/MoonDusk1996/docker_electrs/master/quick_start.sh | bash
```

Isso irá baixar esse repositório no diretorio no qual você executou esse script e criará uma imagem docker do electrs. Após terminar de criar a imagem, edite o arquivo de configuração `electrs.conf` em `./docker_electrs/docker_electrs/electrs_data` . Você deverá editar os campos "auth", "daemon_rpc_addr" e daemon_p2p_addr" conforme seu nó Bitcoin, após editar, salve o arquivo e suba seu contêiner de testes executando o seguinte comando:

```
docker run --rm -v <./caminho_para_electrs_data>:/electrs electrs:latest
```

O comando acima subira o seu container de testes, se suas configurações em `electrs.conf` estiverem corretas nenhum erro será retornado, caso contrário seu container será parado instantaneamente.
Depois de ter certeza de que suas configurações estão corretas, poderá parar de executar o container de testes com `Ctrl + c` e iniciar o container que ficará ativo de fato com:

```
docker run -v <./caminho_para_electrs_data>:/electrs -p 127.0.0.1:50001:50001 -d --restart=unless-stopped --name electrum-server electrs:latest
```

Após isso seu contêiner estará em execução, contudo pode ser que leve algumas horas para ele sincronizar completamente com seu nó de Bitcoin. Você pode ver o status do processo executando:

```
docker logs -f electrum-server
```

Nota: Você pode adicionar qualquer diretório para armazenar o banco de dados electrs, desde que tenha um `electrs.conf` lá.
