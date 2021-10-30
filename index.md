# Tutorial de como utilizar SSH para repositorios git no ambiente Windows

# Gerar chave SSH
1 - Primeiro passo será criar a chave SSH para isso abra o console do gitbash e execute o seguinte comando:

```
ssh-keygen -t rsa -b 4096
```

2 - Definir o caminho e nome da chave que será criada.
Por padrão a chave criada é no diretorio `c/Users/seuusuario/.ssh/` com o nome `id_rsa` 

```
Enter file in which to save the key (/c/Users/seuusuario/.ssh/id_rsa):  
```

- Caso for utilizar o caminho e arquivo padrão basta apertar enter. (não será necessário realizar o passo X)
 - Caso for utilizar outro caminho informar um diretorio existente e um nome para o arquivo Ex.:  c:/sshdir/chavessh `(será obrigatório realizar o passo X)`

 3 - Caso queira obrigar digitar uma senha toda vez quer for utilizar a chave ssh deve ser informado a senha desejada nesse momento caso contrário pressione enter.

 `Obs.: a senha será solicitada em todo comando (git clone, git fetch, git pull , git merge)`

 ```
 Enter passphrase (empty for no passphrase):
 ``` 

4 - Confirmar senha 
```
Enter same passphrase again:
```

5 - Resultado Experado
```
user@computername MINGW32 /bin
$ ssh-keygen -t rsa -b 4096
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/user/.ssh/id_rsa): c:/sshdir/chavessh
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in c:/sshdir/chavessh
Your public key has been saved in c:/sshdir/chavessh.pub
The key fingerprint is:
SHA256:y1sE52rH1OAY7WtZO9PCQ3gnd0neIOaIyn9/zNyL4ZE user@computername
The key's randomart image is:
+---[RSA 4096]----+
|                 |
|         .       |
|        o + o .. |
|         X B .o.o|
|        S O B ooo|
|     . o * B *.. |
|      o = B BE.. |
|       o =. .=O .|
|        o. ..+ ..|
+----[SHA256]-----+
```

6 - Acesse o diretorio onde foi criada a chave, você irá perceber que foram criado dois arquivos (chavessh e chavessh.pub)

### `NUNCA COMPARTILHE SUA CHAVESSH, SÓ COMPARTILHE A CHAVESSH.PUB`

```
user@computername MINGW32 /bin
$ cd c:/sshdir

user@computername MINGW32 /c/sshdir
$ ls
chavessh  chavessh.pub
```


## Copiar conteúdo da Chave Publica (.pub)  para o GitHub

7 - Copiar o conteúdo do arquivo .pub
- [via bash]:  utilize o comando `cat` para exibir o conteudo e em seguida selecione e prescione ctrl+c
```
user@computername MINGW32 /c/sshdir
$ cat chavessh.pub
ssh-rsa BLaBlaBlaBlablablablaBlaBlaBLaBlaBlaBlablablablaBlaBlaBLaBlaBlaBlablablablaBlaBlaBLaBlaBlaBlablablablaBlaBlaBLaBlaBlaBlablablablaBlaBlaBLaBlaBlaBlablablablaBlaBlaBLaBlaBlaBlablablablaBlaBlaBLaBlaBlaBlablablablaBlaBlaBLaBlaBlaBlablablablaBlaBla== user@computername
```

- [via Editor] Abra o arquivo criado com a extensão .pub no seu editor favorito(Notepad, VSCode, Notepad++) e copie o conteúdo todo.

8 - Acesse sua conta no github.com.br  e em seguida entre no link https://github.com/settings/keys

 - Clique no botão __[New SSH key]__
 - Adicione um `title` para a chave. Ex.: Chave Computador ou Chave Notebook Dell
 - Cole o conteúdo da chave.pub dentro do TextArea do campo Key
 - Clique no botão __[Add SSH key]__

 9 - Configurar a chave criada como sendo padrão para o servidor github (esse passo somente é necessário caso você tiver alterado o nome padrão da chave e/ou diretorio (passo 2))
- Acessar a pasta do seu usuário no windows (c:\Users\seuusuario\.ssh) 
- criar um arquivo sem extensão com o nome `config` e salvar o seguinte conteúdo no arquivo:

```
Host github.com
    Hostname github.com
    IdentityFile /C/sshdir/chavessh
    IdentitiesOnly yes 
```
*no campo IdentityFile alterar para o diretorio e arquivo onde foi criado sua chave*


10 - Tentar clonar um repositório utilizando o SSH no github
- Executar o comando git clone utilizando SSH
Ex.: 
```
git clone git@github.com:zonete/windowstutorialssh.github.io.git
```

obs.: Caso tenha definido uma senha no passo 3, a mesma será solicitada.

Resultado Esperado
```
user@computername MINGW32 /c/sshdir
$ git clone git@github.com:zonete/windowstutorialssh.github.io.git
Cloning into 'windowstutorialssh.github.io'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
```



