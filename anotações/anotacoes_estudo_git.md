# Git

### Conceito

Versionamento é o Controle de versões diferentes de um documento.

Sistemas de versionamento são importantes para manter os registros  de modificação, gerencia as versões e podem ser centralizados ou distribuídos. 

O git é um sistema de versionamento distribuido onde cada cópia do repositório contem o histórico completo de todas as alterações.

### Objetos no Git

O git tem três tipos básicos de objetos, que são responsáveis pelo versionamento do nosso core:

Blobs - Bloco básico de composição

Trees - Armazenam blobs e commits

Commits -

### Rastreamento no Git

Os arquivos no diretório gerenciado pelo git podem estar em dois estados, untracked (não rastreados) quando o git não sabe da existencia deles ou tracked (rastreados) quando são adicionados através do comando “git add”.

Quando os arquivos estão tracked eles podem estar em três estados:

- Staged - Quando add o arquivo no git ele sai do estado de untracked para staged, que é quando ele esta pronto esperando um commit.
- Unmodified - Quando o commit é dado o git grava uma imagem dos arquivos (no repositório local) e eles vão para o estado Unmodified.
- Modified - Quando editamos os arquivos eles vão para o estado modified e ao darmos o “git add” eles vão novamente para staged aguardando um commit.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9aa4824f-99d8-45ac-9360-9b9def07929a/Untitled.png)

Podemos verificar o status desse arquivos com o comando:

```yaml
git status
```

### Ambientes no Git

No git temos dois ambientes que é o repositório local e o repositório remoto.

- Repositório local - Onde são armazenados os commits localmente.
- Repositório remoto - Para onde são enviados os commits locais. Ex: github, bitbucket, etc.

### Commit

Cada commit ele guarda um snapshot de todos os arquivos.

A cada commit é gerado uma nova versão do projeto.  

```jsx
git commit
```

### Commits atômicos

Estruturação de commits

Devemos ter commits organizados para que você mesmo ou outras pessoas possam entender bem tudo que foi feito. O ideal é que um commit contenha inicio, meio e fim de tudo relativo a uma tarefa especifica e não vários commits quebrados. Por exemplo: se houver uma correção no menu que foi feita em 2 etapas é ideal que as duas estejam em um so commit e não em dois commits separados. 

A estrutura de um commit é dividida em:

- Assunto: Curto e compreensível, até 50 caracteres, não terminar em ponto, Escrito de forma imperativa (Falando uma ação). Ex: Adiciona a funcionalidade X.
- Corpo: Adicione detalhes ao commit, tente quebrar a linha em 75 caracteres, Explique tudo, Use markdown.
- Rodapé: Referencie assuntos relacionados.

conventional commits - Especificação para um commit legível. 

### Primeiros comandos no Git

Comando init para iniciar o git repositório, assim o git poderá começar a gerenciar e versionar o nosso código. Ele cria um diretório oculto .git dentro da pasta onde armazenará todo o controle.

```yaml
git init 
```

Para adicionar os arquivos ao git podemos usar o git add passando um arquivo ou pasta ou * para tudo.

```yaml
git add *
```

Depois damos o commit, que fará o “snapshot” dos arquivos. E gerará uma versão.

```yaml
git commit -m "commit inicial" 
```

Para termos certeza que estamos usando a branch certa usamos o comando:

```yaml
git branch -M main
```

Devemos entao add a origem remota que receberá nosso commit. Para o git saber para onde queremos manda-lo, vamos vincular o endereço a uma variavél (que será “origin” nesse exemplo).

```yaml
git remote add origin https://github.com/andersonluix/teste.git
```

Podemos listar as origens remotas que temos cadastradas com o comando:

```yaml
git remote -v
```

Agora podemos enviar o commit para um repositório remoto. Com o comando “git push” passando a variável de destino setada anteriormente.

```yaml
git push -u origin main
```

### Git ignore

Podemos usar o arquivo .gitignore para dizer ao git quais arquivos/padrões de arquivos devem ser ignorados. Arquivos que não queremos versionar.

Exemplo, quando trabalhamos com IDEs e temos arquivos que não desejamos versionar, podemos adiciona-los. No caso do uso de um projeto com Mavem, queremos ignorar a pasta target. Podemos então criar o arquivo .gitignore:

```jsx
vim .gitignore
```

Dentro dele podemos colocar o nome da pasta a ser ignorada

```jsx
#Pasta a ser ignorada Maven
target/
```

Após isso vamos adicionar o arquivo .gitignore ao nosso projeto e comita-lo.

```jsx
git add .gitignore
git commit -m "Adiciona o gitignore com exclusao da target"
```

### Conflitos no Git

Merge Conflit

Quando tentamos enviar um commit e a nossa versão dos arquivos está mais desatualizada que a versão que já consta no repositório remoto dará erro pq não temos as atualizações que estão lá.

Para resolver este problema precisamos puxar os arquivos do repositório remoto depois, com a versão atual, fazermos nossas modificações e dai enviarmos o novo commit.

Para puxar os arquivos do diretório remoto usamos o comando *git pull*, passando a variável que contém o endereço do repositório e de qual branch queremos puxar.

```yaml
git pull origin main
```

Se o arquivo que foi atualizado for o mesmo que nós atualizamos, o git vai exibir um alerta **CONFLICT (content): Merge conflict in nome_do_arquivo**. 

O git vai criar marcações no arquivo mostrando as duas alterações e você deve decidir quais ficam, remover as marcações do git, dar um git add novamente, dar um novo commit e então o push.

Exemplo de arquivo marcado pelo git. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/87fff320-a0d4-49a8-9f59-a076b39d86eb/Untitled.png)

Como ficou:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/277eb1d0-1bfa-4936-b1c3-263abdcef330/Untitled.png)

Fazemos o git add no arquivo corrigido.

```yaml
git add arquivo.txt
```

Fazemos um novo commit.

```yaml
git commit -m “resolve conflito”
```

E agora podemos empurrar todo o commit para o github.

```yaml
git push origin main
```

### Branch no Git

Branch no Git também são incrivelmente leves. Eles são simplesmente referências a um commit específico e nada mais. São uma bifurcação do trabalho atual onde podemos trabalhar em paralelo a “produção”.

Por enquanto, só lembre que um ramo diz essencialmente "Quero incluir o trabalho deste commit e de todos os seus ancestrais".

Podemos gerar novas branchs a partir de uma branch original.

```jsx
git branch [nome]
```

Se estivermos usando uma branch e quisermos mudar o nome dela. Este comando muda o nome da branch que estamos no momento!!!

```jsx
git branch -m [novonome]
```

Para renomear um branch a partir de outra branch usamos o comando passando o nome da branch que queremos mudar e o novo nome.

```jsx
git branch -m [nome] [novonome]
```

Para deletar uma branch:

```jsx
git branch -d [nome]
```

Podemos ver quais brachs temos com o comando:

```jsx
git branch
```

Podemos marcar essa branch como ativa para que ela receba os novos commits. Mudar pra outra branch:

```jsx
git checkout [nome]
```

### Comando stash e seus subcomandos.

Ao no covimentarmos entre branchs com o comando “checkout” alguns arquivos que ainda não foram comitados são “levados” de uma branch para outra e caso seja dado um “git add *” eles irão ser adicionados na branch “errada”. 

O stash ele serve como uma “caixinha” que podemos deixar os arquivos para que essa “sujeira” não nos acompanhe ao trocar de branch.

Obs: Os arquivos para irem pro stash tem que estar em estado de stage, ou seja, devemos dar um “git add” neles.

Portanto para adicionar os arquivos ao stash, primeiro de um git add.

```jsx
git add [arquivo]
```

Podemos criar vários stash e é interessante salvar uma mensagem de contexto para esse stash. Com o comando abaixo os arquivo já serão incluidos no stash

```jsx
git stash save "Arquivos iniciais mudanca login"
```

Para listar os stash

```jsx
git stash list
```

Para tirar os arquivos do stash e voltar a trabalhar com eles, devemos dar o comando abaixo passando o index do stach(podemos ver o index de cada stash com o comando “git stach list”).

```jsx
git stash pop 0
```

Para apagar os stashs. 

Obs: Os arquivos dentro do stash serão apagados junto!!!! 

```jsx
git stash clear
```

### Merge

Combinar o trabalho de duas branchs diferentes usamos o merge.

O merge do Git cria um commit especial que possui dois pais únicos. Um commit com dois pais essencialmente significa "Quero incluir todo o trabalho deste pai aqui com o daquele outro pai ali, e com o do conjunto de todos os seus ancestrais.

Aqui nós temos dois ramos; cada um tem um commit que é único. Isso significa que nenhum ramo inclui o conjunto do "trabalho" que foi realizado no repositório. Neste caso a branch main esta como ativa e vamos dar o comando para ela juntar à branch “bugFix”. 

```jsx
git merge bugFix
```

Obs: Damos o merge chamando a branch que não está ativa.

No fim a branch main incorpora as alteração que existiam na branch bugFix e então fica atualizada. Conforme imagem abaixo.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/73bb3f79-30f8-4ab0-8723-c0d5cec5145b/Untitled.png)

### Rebase no Git

A segunda forma de combinar trabalho entre ramos é o *rebase*. O rebase essencialmente pega um conjunto de commits, "copia" os mesmos, e os despeja em outro lugar.

Isso pode parecer confuso, mas a vantagem do rebase é que ele pode ser usado para construir uma sequência mais bonita e linear de commits. O registro de commits (história do repositório) ficará muito mais limpa se for utilizado apenas rebase em vez de merge.

Quando usamos o rebase para mover o bugFix diretamente dentro do main, ele se junta ao main parecendo que esses dois recursos foram desenvolvidos sequencialmente, quando na realidade foram feitos em paralelo.

O comando se da chamando a branch que nao está ativa, e a ativa que desce na sequencia.

```jsx
git rebase main
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/65b0c77f-a019-468f-99a9-ba0d61554506/Untitled.png)

Após isso podemos mudar para a branch “main” (git checkout main) e executar o rebase novamente (git rebase bugFix). Como o main era um ancestral dobugFix, o git simplesmente moveu a referência do ramo main para frente na história.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cd193be4-b91f-4e1a-a349-135ab4a37eed/Untitled.png)

## Movendo-se no git

HEAD - É uma tag no git que aponta para o último commit valido em uma branch. É um nome simbólico para o commit atualmente ativo.

Geralmente o head fica anexado a uma branch. Soltar o HEAD siginifica anexa-lo a um commit ao invés de uma branch.

Quando damos o comando abaixo o head é anexado ao commit

```jsx
git checkout [hash_do_commit]
```

### Referências relativas

Especificar commits pelo hash não é a sempre o mais conveniente, e é por isso que o Git suporta referências relativas. 
Elas são fantásticas!

Com referências relativas, você pode começar a partir de um ponto fácil de lembrar (como o ramo `bugFix` ou o `HEAD`) e referenciar a partir dali.

Commits relativos são poderosos, mas vamos introduzir apenas dois tipos simples aqui:

- Mover para cima um commit por vez com `^`
- Mover para cima um número de vezes com `~<num>`

Vamos dar uma olhada no operador circunflexo (^) primeiro. Cada vez que você adicioná-lo a um nome de referência, você está dizendo ao Git para encontrar o pai do commit especificado.

Então, dizer `main^` é equivalente a "o primeiro pai do `main`". `main^^` é o avô (ancestral de segunda geração) do `main`

Também podemos usar o head como parte de uma referência relativa. Ex:

```jsx
git checkout HEAD^ 
```

Vamos dar uma olhada no operador til (~). Um número pode ser passado (opcionalmente) após o operador til, especificando o número de ancestrais que você deseja subir. Ex:

```jsx
git checkout HEAD~4
```

Uma das situações mais comuns na qual eu uso referências relativas é quando quero trocar ramos de lugar. Você pode redefinir diretamente o commit para o qual um ramo aponta com a opção `-f`
. Desta forma, o seguinte comando move (a força) o ramo main 3 ancestrais acima do HEAD. (O main que sobe.)

```jsx
git branch -f main HEAD~3
```

### **Revertendo Mudanças no Git**

Primeiramente devemos observar que num cenário real com repositório remoto, quando resetamos o commit e tentamos o push dará erro os arquivos estarão diferentes, portanto será preciso fazer o pull novamente deixar tudo como queremos e depois fazer o push.

Seguindo…

Há duas maneiras principais de desfazer mudanças no Git -- uma delas é usando `git reset`, e a outra é usando `git revert`.

O git reset/revert usam o hash do commit como referência ou a tag Head. Usam as referências relativas ensinadas anteriormente.

RESET

O comando `git reset` reverte mudanças movendo para trás no tempo (para um commit mais antigo) a referência do ramo. Desta forma, você pode pensar nessa operação como uma "reescrita do histórico"; o `git reset` vai mover o ramo para trás como se o commit nunca tivesse existido. EX:

```jsx
git reset HEAD~1
```

Quando damos o comando acima ele assume por padrão o parâmetro —hard.

O parâmetro —hard apaga o commit e APAGA os arquivos que entraram nesse commit!!!!

Outros parâmetros do reset:

O parametro —soft faz o reset e move o status dos arquivos que entraram nesse commit para stage.

```jsx
git reset --soft HEAD^
```

O parâmetro —mixed apaga o commit e muda os status dos arquivos que entraram nesse commit para unstaged.

```jsx
git reset --mixed HEAD~1
```

REVERT

Embora o reset funcione muito bem em ramos locais no seu próprio computador, o método utilizado de "reescrever o histórico" não funciona com ramos remotos que outras pessoas estejam usando. Para reverter mudanças e conseguir *compartilhar* essas mudanças com os outros, precisamos usar o `git revert`

Obs: O git revert não tem flags. Ele cria outro commit desfazendo as coisas até chegar no formato do commit anterior.

```jsx
git revert HEAD
```

### **Git Cherry-pick**

Trata-se de uma forma bastante direta de dizer que você gostaria de copiar uma série de commits abaixo do seu local atual (`HEAD`).

Neste exemplo copiamos os commits C2 e C4 para o main que estava no C5 e recebeu logo abaixo.

```jsx
git cherry-pick C2 C4
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e3abe32a-b0bb-4e8f-a906-554a008223b2/Untitled.png)

### **Rebase Interativo do Git**

O cherry-pick é ótimo quando você sabe de antemão quais commits você quer (*e* você sabe os hashes correspondentes) -- é difícil bater a simplicidade que ele oferece.

Mas e quando você não sabe quais commits você quer? Felizmente o git pode te ajudar nesta situação também! Podemos usar o rebase interativo para isso -- trata-se da melhor forma de rever uma série de commits sobre os quais você está prestes a fazer um rebase.

O rebase interativo é simplesmente o comando `rebase` com a opção `-i`.

Se você incluir essa opção, o git abrirá um arquivo para mostrar quais commits estão prestes a serem copiados abaixo do alvo do rebase. Ele também mostra os hashes e as mensagens dos commits, o que é ótimo para ter noção do que é o que.

```jsx
git rebase -i main~5
```

Aqui está uma situação de acontece frequentemente com desenvolvedores: Estou tentando encontrar um bug, mas ele é escorregadio. Para auxiliar meu trabalho de detetive, eu coloco alguns 
comandos de debug e prints.

Todos esses comandos de debug e mensagens estão em seus próprios ramos. Finalmente eu encontro o bug, corrijo, e me regozijo!

O único problema é que agora eu preciso devolver o meu `bugFix` ao ramo `main`. Se eu simplesmente der um fast-forward no `main`, então o `main` terminará contendo todos os comandos de debug, o que é indesejável. Deve existir alguma outra forma...

Precisamos  dizer ao git para copiar somente um dos commits. Esta situação é 
exatamente a mesma dos níveis anteriores a respeito de como mover trabalho -- podemos usar os mesmos comandos:

- `git rebase -i`
- `git cherry-pick`

Para alcançar o objetivo.

## Tags no Git

As tags do Git marcam de forma (relativamente) permanente certos commits como se fossem "pedras de kilometragem"("milestones") em uma estrada, e você pode referenciá-las exatamente como faz com ramos. 

Uma forma de marcar pontos históricos do projeto.

```jsx
git tag V1 C4
```

Esse comando vai marcar uma tag “V1” no commit de hash “C4”

## Git Describe

Devido ao fato de as tags servirem como "âncoras" tão boas no código, o Git tem um comando para *descrever* onde você está com relação à "âncora" (tag) mais próxima. Esse comando é chamado `git describe`!

O git describe é chamado da seguinte forma:

`git describe <ref>`

Onde `<ref>` é qualquer coisa que o git possa resolver como uma referência a um commit. Se você não especificar o ref, o Git usa simplesmente o commit atual (`HEAD`).

A saída do comando é mais ou menos assim: `<tag>_<numCommits>_g<hash>`

Onde `tag` é a tag ancestral mais próxima no histórico, `numCommits` é o número de commits de distância da tag, e `<hash>` é o hash do commit sendo descrito.

### Logs

O log no git se trata basicamente do histórico do que foi feito no repositório.

Podemos realizar um clone de um repositório e analisa-lo.

Comando para ver log

```jsx
git log
```

Podemos ver o log somente de uma pasta especifica.

```jsx
git log [nomepasta]
```

Podemos ver o log somente de um arquivo especifico.

```jsx
git log [nomearquivo]
```

Podemos ver o log somente de uma branch especifica.

```jsx
git log [nomebranch]
```

Temos também um Ferramenta para visualizar logs git no Windows (github Descktop, Gitk) e no linux (gitkraken). 

### Fork/Pull request

Um fork é uma cópia de um resitório de outra pessoa para o seu repositório para que você possa trabalhar naquela solução como bem entender e depois enviar aquela melhoria para o dono original com um pull request.

pull request é uma solicitação de pull que fazemos quando queremos enviar um pull para uma conta de outra pessoa. Geralmente quando não temos permissão para aquele repositório. Este pull pode ser aceito ou não.

O fork deixa o repositório copiado com a referencia do original, facilitando o pull resquest.

Se quisermos então trabalhar num repositório da empresa/outro e fazer nossas alterações e depois solicitar o envio devemos:

1. Fazer o fork do diretório da conta do outro.
2. Fazer o pull para nossa máquina.
3. Criar uma branch específica para que o autor possa baixar e testar seu pull request antes de aceitar.
4. Fazer as alterações desejadas.
5. Após fazermos as alterações, podemos então fazer o git add, o git commit e git push para nossa conta. 
6. Após feito isso o github já vai entender que vc fez uma alteração e sugerir o pull request para o diretório do dono, ao loga no seu github no repositório basta clicar no botão pull request lá e o git hub irá faze-lo.

Obs: Esta não é uma maneira muito boa de se trabalhar em equipe. Falaremos abaixo sobre isso com permissões, organização de times, etc.

### Permissões/Colaboradores

Podemos dar permissões para pessoas que estejam trabalhando comigo em um projeto. 

1. No github, dentro do repositório, no menu settings→ manage access → botão invite collaborator.

Quando o calaborador aceitar ele já poderá fazer o clone do repositório, alterar, comitar e enviar(push) diretamente para o repotório sem problema nenhum.

### Aliases

Podemos criar alias para os comando git. Para não precisar digitar o comando inteiro.

Com o comando git config passando o alias.[nome] [comando].

Vamos fazer um exemplo criando o alias ‘s’ para o ‘status’

```jsx
git config --global alias.s status
```

Dessa forma ao darmos o comando “git s” será igual ao comando “git status”

Para retirar o comando basta usar —unset

```jsx
git config --global --unset alias.s
```

Para listar as configurações usamos o comando:

```jsx
git config --global --list
```
