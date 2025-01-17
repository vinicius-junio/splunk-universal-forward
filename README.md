# Universal Forwarder

## Índice

- [Introdução](#introdução)
- [Configuração Splunk](#configuração-splunk)
- [Download Universal Forwarder](#download-universal-forwarder)
- [Instalação Universal Forwarder](#instalação-universal-forwarder)
- [Configuração Integridade Universal Forwarder](#configuração-integridade-universal-forwarder)
- [Configuração Universal Forwarder para o Indexador](#configuração-universal-forwarder-para-o-indexador)

  
## Introdução
<div align = "justify">
  O Universal Forwarder é um componente leve da plataforma Splunk que coleta dados de várias fontes e os envia para um servidor Splunk (como um Splunk Indexer ou Splunk Cloud) para processamento e análise. Ele é usado para coletar logs, métricas e outros dados de forma eficiente e segura, permitindo a centralização e correlação de dados para monitoramento, análise e visualização. É especialmente útil em ambientes distribuídos onde é necessário coletar dados de múltiplos servidores e dispositivos.
</div>
<br>
<p align="center">
  <img src="universal_forwarder/universal_forwarder.png" alt="Splunk Index">
</p>


## Configuração Splunk

  O primeiro passo é configurar a porta de escuta do Splunk.<br>
  1. Acessar o Splunk Enterprise / Cloud como Administrador.
  2. Clicar em Settings -> Forwarding and receiving.
  3. Em "Receive Data", clicar em "Add new".
  4. Ao abrir o "Configure receiving", adicionar a porta TCP de escuta que o indexador deve escutar.<br><br>

  Após configuração da porta tcp de escuta, podemos configurar um index, pois se o envio dos logs forem feito para porta sem um index, ele vai ir direto para o index "main".<br>
  1. Na console clique em "Settings" -> "Indexes" -> "New Index".
  

## Download Universal Forwarder

  O primeiro passo é realizar o Download do Universal Forwarder.<br>
  1. Abrir o site do [Splunk](https://www.splunk.com/) e realizar o login na conta. Caso não possuir, você deve realizar o cadastro.
  2. Ao realizar o login clique em "Download page".
  3. No "Universal Forwarder", clique em Download.
  4. Selecione a versão do Universal Forwarder que deseja instalar e clique em Download Now, ou copie o link do WGET caso preferir.

## Instalação Universal Forwarder

  Como exemplo estamos utilizando um Oracle Linux com a versão 5.x+ kernel Linux distributions.<br>
  1. Como boa prática vamos descompactar o arquivo .tgz no diretório /opt do Linux.

```
  cd /opt
  sudo tar xvzf <package_universal_forwarder>
```
  2. Ir para o diretorio /bin onde podemos executar o comando executável "splunk".
```
  cd /opt/splunkforwarder/bin
```
  3. Executar comando de instalação.
```
  ./splunk start --accept-license
```

IMPORTANTE:  Defina o username e password para acesso ao Agent.<br>
 
## Configuração Integridade Universal Forwarder

  Para evitar perda de dados, o agent do Universal Forwarder deve ser iniciado sempre que o servidor for reinicializado, então podemos usar o comando:
```
  sudo su
  ./splunk enable boot-start
  exit
```

## Configuração Universal Forwarder para o Indexador

  Agora vamos configurar o Universal Forwarder para enviar os dados ao indexador receptor.
```
  ./splunk add forward-server <ip>:<port>

  Obs: Vai solicitar o username e senha definido durante a instalação.
```

  Agora precisamos informar ao Universal Forwarder quais dados enviar ao indexador.<br><br>
  O comando "add monitor" é usado para informar ao Universal Forwarder quais dados gostaria de enviar.<br><br>
  Neste exemplo todos logs da pasta /log-forwarder sera encaminhado para o Splunk.
```
  ./splunk add monitor  /opt/log/log-forwarder -index <index_criado_splunk>

  Obs: User e Password definido durante a instalação.
```
<br>
Após isso os logs já serão encaminhados para o index configurado.

<br>
<br>
