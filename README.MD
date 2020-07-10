#### cat ~/.gitconfig

```
[core]
	autocrlf = input
	safecrlf = warn
	editor = vim

[alias]
  co = checkout
  ci = commit
  st = status
  br = branch
  hist = log --pretty=format:\"%h %ad | %s%d [%an]\" --graph --date=short
  type = cat-file -t
  dump = cat-file -p

[filter "lfs"]
	process = git-lfs filter-process
	required = true
	clean = git-lfs clean -- %f
	smudge = git-lfs smudge -- %f
[user]
	name = Marlon Authority
	email = 15050029+marlonauthority@users.noreply.github.com
[help]
	autocorrect = 1
[color]
	ui = true

```

## Sincronizando 
Para atualizar seu repositório local com a mais nova versão, execute:
```
git pull
```

## MERGE
> Está atualizando sua branch pegando as coisas do master?
```
git pull --rebase
```
> Terminou sua feature no branch e quer jogar para o master?
```
git merge 
```


## Revert
Use revert para reverter ultimo commit
```
git revert HASH
```

## RESET
use reset para reverter um commit
__--soft__ que vai voltar o commit mas mantera as alteracões feitas dos arquivos.

__--hard__ resetará tudo ao estado original.

```
git reset --hard HASH
```

__Use revert para o master e reset para branchs__ 


## Corrigindo a ultima mensagem do commit
```
git commit --amend
```

### Cherry-pick
é possivel pegar um commit especifico de um outro branch
```
git cherry-pick HASH
```

### Comintando trechos especificos.
```
git add -p
```


## Juntando commits com Squash
squash significa juntar os ultimos commits
```
 git rebase -i HEAD~2
```
Alterar na tela interativa de **pick** para **squash**.

Na segunda tela voce altera a mensagem.
Obs: o HEAD~2 ali estou dizendo os dois ultimos commits


## Corrigindo conflitos
Se por acaso voce fez commits locais e na hora de enviar git push origin der conflito, voce pode fazer o seguinte.
```
git pull origin master --rebase
```
Isto fara com que os commits locais e remoto fiquem em ordem, ai sim podendo fazer um push origin.


### Vendo o histórico de ponteiros
```
git reflog
```

### Contribuindo 
1 - Primeiro, faço um fork do projeto.

2 - Depois, um clone do meu repositório no Github em sua máquina:


```
$ git clone https://github.com/marlonauthority/git-github-real-life-example.git

```

3 - Neste ponto, você tem um remoto chamado "origin". Então, adicione outro, chamado "upstream", que aponte para o original:
```
$ git remote add upstream https://github.com/marlonauthority/git-github-real-life-example.git
```

4 - De tempos em tempos, sincronize:
```
$ git checkout master
$ git fetch upstream
$ git rebase upstream/master
```

5 - Após fazer o rebase acima, meu master local fica exatamente igual ao master do upstream, precisando apenas atualizar a versão do github:
```
$ git push origin master
```

Eu tenho o costume de trabalhar apenas em tópicos (ie: a cada nova feature, um novo branch). Quando eu acabo o trabalho, envio este branch para o github:
```
git branch -d funcionalidade_x
git push origin funcionalidade_x
```

Então, do próprio github, eu faço um Pull Request dos commits no branch ao master do upstream. Meu master nunca recebe diretamente meus commits, o que facilita na sincronização, já que considero o master como um ponto de início para qualquer nova feature. Quando os commits do meu branch forem aceitos em upstream/master, eles chegam no meu master na próxima sincronização.

