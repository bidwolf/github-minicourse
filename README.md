# github-minicourse
Um mini curso para melhor entender o que é o git e o github

## Principais comandos utilizados
Existem inúmeros comandos que você pode e vai utilizar dentro do git durante sua trajetória como desenvolvedor, mas aqui vou listar alguns dos mais comuns que você com certeza vai precisar na maioria dos projetos.

### Criar um repositório git

Para criar um repositório dentro do git você pode executar o comando `git init` dentro da pasta em que você pretende versionar
O comando criará uma pasta oculta .git que contém informações sobre o seu repositório.

### Adicionar configurações e metadados ao git

Para efetuar commits, não é obrigatório o uso de um nome ou email do usuário, mas para utilizar o github é, então para simplificar, vamos fazer isso no começo:

`git config --global user.name:<seu nome>`
`git config --global user.mail:<seuemail@email.com>`

> Existem muitas outras configurações adicionais que você pode querer fazer, e inclusive pode fazer configurações apenas localmente.

### Listar alterações no working directory

Para ver as alterações feitas no working directory você pode executar o comando `git status` que verifica é capaz de descrever se os arquivos foram:

- criados
- modificados
- deletados

> para ver a diferença entre uma versão ou outra de um arquivo você pode usar o comando `git diff`

### Adicionar alterações / remover alterações para a staging Area

As alterações, adições ou exclusões feitas dentro da working directory podem ser preparadas para serem commitadas dentro da stagging Area. A staging area não cria um ponto no histórico, e as alterações podem ser removidas da staging area de diferentes formas.

#### Adicionando
- `git add <diretório_do_arquivo>`: Adiciona tudo que estiver nesse diretório (pode ser uma pasta, ou um arquivo em específico)
- `git add .` : Adiciona todos os arquivos contidos no diretório atual
- `git add -A`: Adiciona todas as alterações da working tree

#### Removendo
- `git reset --soft`: Remove apenas as adições de arquivos novos mantendo as modificações adicionadas, e não apaga os arquivos removidos da staging area 
- `git reset --mixed`: Remove adições e alterações da staging area mas também não apaga os arquivos ou as alterações
- `git reset --hard`: Remove todas as alterações e adições e torna a working directory exatamente igual ao que era anteriormente.

### Criando/revertendo commits

#### Criando commits
- `git commit -m "<mensagem do commit>"`: Cria um commit utilizando apenas as alterações previamente adicionadas.
- `git commit -am "<mensagem do commit"`: Cria um commit adicionando todas as modificações às alterações previamente adicionadas.
#### Revertendo commits criados
- `git revert <hash-do-commit>`: cria um commit que reverte alterações de um commit específico
- `git reset HEAD~1`: Esse comando não cria um commit, e ele apenas desfaz o commit, entretanto as alterações feitas por ele continuam na working directory
- `git commit --amend`: Adiciona alterações ao último commit sem criar um novo commit.
- `git revert -n <hash-do-commit>`: Reverte um commit específico, mas sem criar um novo commit de reversão.
- `git reset --hard HEAD`: Remove todas as alterações e adições e torna a working directory exatamente igual ao que era anteriormente.

### Branches

#### Criando novas branches
As branches são como diferentes linhas do tempo nos repositórios git, uma branch pode ser derivada de outra, e essas branches podem ser unidas em uma linha do tempo em comum.

A branch padrão normalmente utilizada é a branch main (ou master, dependendo da versão, e configuração).
Para cruar uma branch você pode executar o comando `git branch <nome-da-branch>`, para criar uma branch nova no repositório a partir da sua branch atual.

Existem outros comandos que podem ser utilizados como por exemplo:
- `git checkout -b <nome-da-branch>`: cria uma branch e automaticamente muda para ela.
- `git switch -c <nome-da-branch>`: faz o mesmo que git checkout -b.

#### Listando branchs

Para listar as branchs existentes você pode executar o comando `git branch` ou `git branch -l` para listar todas as branchs disponíveis.

#### Mudando de uma branch para outra

O comando para mudar de branch é o `git checkout <nome-da-branch>` que simplesmente muda para a branch mencionada. Uma alternativa é o comando `git switch` que faz praticamente a mesma coisa.

#### Mesclando branches

O comando que mescla branches é o comando `git merge <nome-da-branch`, que mescla a branch atual com a branch mencionada.

#### Conflitos

Uma branch pode ter conflito com outra quando se efetua o merge, e sempre que isso ocorre, deve ser feita uma avaliação da forma com que o conflito deva ser resolvido. O git é capaz de resolver conflitos automaticamente quando não existem alterações que afetam um mesmo ponto, mas caso contrário o conflito deve ser resolvido manualmente, decidindo a estratégia utilizada, como mesclar alterações (tenta usar as duas alterações em conjunto), ou aceitar exclusivamente uma delas.

#### Excluindo branches

As duas principais formas de excluir uma branch é basicamente utilizar o comando `git branch -d` para deletar uma branch de forma segura (a branch já sofreu merge), ou `git branch -D` para deletar de forma não segura (não sofreu merge).

### Repositório remoto

Se você clonou o repositório, essa etapa não é necessária, mas caso contrário você deve adicionar uma referência ao seu repositório remoto, e o comando para fazer isso é `git remote add <nome-da-referencia> <link do repositório remoto>`

Caso queira saber qual a url atual do seu repositório remoto basta utilizar `git remote get-url <nome-da-referencia>`.
> Se você clonou o repositório o nome da referência por padrão será `origin`.

#### Capturando branches remotas no repositório local

Você pode criar branchs diretamente no repositório remoto, e uma vez que tenha feito isso, você pode, dentro do repositório local, utilizar as referências dessa branch através do comando `git fetch <nome-da-referencia> <nome da branch>`.

### Carregando informações do repositório remoto

Um atalho para manter sua branch local atualizada em relação a uma branch remota é o comando `git pull <nome-da-referencia> <nome-da-branch>`.

Se você executar esse comando, o repositório atual efetuará o merge da branch remota especificada, e caso sua branch já esteja atualizada, você provavelmente deve ver a mensagem, "*your branch is already updated*" ou algo assim.

### Salvando informações diretamente no repositório remoto

Se dá pra carregar, tem que dar pra salvar, e a sua intuição está correta, se você entende um pouco de inglês, você já deve presumir que se o comando que puxa informações do repositório remoto para o repositório local é o comando `git pull`.

Então o comando que empurra alterações do repositório local para o repositório remoto é o comando `git push`.
Você pode executar esse comando com `git push <nome-da-referencia><nome-da-branch>`, ou meu favorito : `git push origin HEAD`.
