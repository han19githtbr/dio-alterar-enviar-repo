

git config: permite definir variáveis de configuração do nosso git

Quando queremos inserir o mesmo nome, o mesmo email para todos os repositórios que 
vamos criar no nosso usuário, vamos armazenar isso no global 

nome (para configurar o nome)
-->git config --global user.name "handy"


e-mail (para configurar o e-mail)
-->git config --global user.email "milliance23@gmail.com"


Para retornar o nome
-->git config user.name  : handy


Para retornar o email
-->git config user.email  : milliance23@gmail.com  


Para retornar o nome da nossa branch padrão que está configurada
-->git config init.defaultBranch  :  master


Para alterar o nome da branch "master" para "main"
-->git config --global init.defaultBranch main  :  altera o nome da branch para main


Para retornar todas as configurações globais
-->git config --global --list


gerar um token no github(um dos motivos)
-->suporte para autenticação com password foi removido no ano...


Como gerar um token? (passo a passo) e não salvar o token por motivos de segurança
-- Clicar no perfil no canto superior direito e ir em settings
-- Developer settings
-- Clicar em Personal access tokens
-- Clicar em Tokens (classic)
-- Clicar em Generate new token e depois escolher Generate new token (classic)
-- Coloca senha da conta do GitHub
-- Em Note, colocar um nome(para que serve o token)
-- Escolher um tempo de expiração do Token (30 dias por exemplo)
-- Select scopes(benefícios do uso do token, limitando o escopo)
   --> escolher repo(por exemplo)
-- Depois clicar em generate token 
-- Depois vai generar o código de acesso ao nosso token
-- Depois voltar no Git Bash
   --> refazer o git clone e colocar o código de autenticação 

------------------------------------------------------------------------     --------------------------------------------------------------


Para fazer outro clone ou outra operação que precise de autenticação
e para não precisar gerar um token a todo momento, podemos salvar esses
credenciais na nossa máquina, fazendo:

primeira possibilidade: Se você compartilha a sua máquina com outra pessoa 
e não deseja que o credencial fique salvo.

git config credential.helper cache


segunda possibilidade: Se você quiser deixar salvo permanentemente, e só você que 
utiliza.

git config --global credential.helper store

e depois tentar clonar novamente


Para mostrar onde a configuração git config store está armazenada
git config --global --show-origin credential.helper  


Para mostrar o conteúdo do arquivo no caso chamado gitconfig, fazemos:
cat .gitconfig


--------------------------------------------------------     -------------------------------------------------------------------


Autenticação via Chave SSH

-- Clicar no perfil no canto superior direito e ir em settings
-- Clicar em SSH and GPG keys


passo 1:  ls -al ~/.ssh  para ver se as chaves SSH existentes estão presentes.

passo 2:  ssh-keygen -t rsa -b 4096 -C "milliance23@gmail.com"

passo 3:  botar uma frase secreta no Git Bash, como senha: hangitgit

passo 4:  eval "$(ssh-agent -s)" ---> gerou: Agent pid 404

passo 5: adicionar a nossa chave privada ao ssh-agent ---> ssh-add ~/.ssh/id_ed25519

passo 6: clicar em New SSH key  
	--> key type: Authentication Key

passo 7: procurar as chaves públicas e privadas
	--> cd ~/.ssh
	--> ls

passo 8: exibir o conteúdo da chave pública: cat id_rsa.pub

	--> Quando gerar, colocar o conteúdo em "key"



---------------------------------------------------------------------------    ----------------------------------------------------------------

mkdir repo-local:  cria uma pasta chamada repo-local

cd .git  ---> (GIT_DIR!)

cat nome_do_arquivo  ---> exibe o conteúdo do arquivo


clonar uma branch específica:  git clone URL --branch nomedabranch --single-branch


git status ---> mostra o status da nossa árvore de trabalho

touch README.md ---> cria um arquivo README.md 

editor readme ---> https://readme.so/pt/editor

adicionar um arquivo ---> git add nome do arquivo
		     ---> exemplo: git add README.md

salvar as alterações ---> git commit -m "commit inicial"

mostrar o commit que fizemos, quem fez e o hash(identidade) do commit ---> git log


O git não reconhece pastas e diretórios vazios

---> Para o git reconhecer uma pasta, temos que inserir algum arquivo nela

---> Por exemplo: touch resumos/resumo-aula1.md


Pedir para o git ignorar a pasta "resumos" ---> echo resumos/ > .gitignore

Remover a pasta "resumos" dentro de gitignore --> echo > .gitignore

Como o git consegue reconhecer um diretório --> com o .gitkeep(touch nomepasta/.gitkeep)

Inserir todos arquivos de uma vez: git add .(adicionar arquivos na nossa área de preparação)



---------------------------------------------------- Desfazendo alterações no Repositório local ------------------------------------------------------

Quando damos um git init na pasta errada e queremos remover o versionamento dela

---> Para isso basta excluir o diretório .git e executar esse comando: rm -rf .git

Restaurar o que apagamos em um arquivo: git restore nome do arquivo (ex: git restore README.md)

Alterar o nome do nosso último commit ---> git commit --amend -m "adicionar todos os arquivos no repo"

Desfazer o último commit e ir para um commit anterior

---> git reset --soft 5efd4cf0ea7c5b770161bc26c1dbb2c4bfa1d827
     Pegar aqueles arquivos que estavam nos commits posteriores ao que a gente indicou ali com o hash 	
     E adicionar esses arquivos na nossa área de preparação	

---> git reset -- mixed hash
     Comportamento padrão do git reset. O mixed pegou os arquivos que estavam nos commits posteriores
     ao que a gente tinha indicado e adicionou eles na nossa árvore de trabalho, indicando como Untracked files(arquivos que o git ainda não conhece)


---> git reset --hard 5efd4cf0ea7c5b770161bc26c1dbb2c4bfa1d827 
     Ignora os arquivos que estavam no commit anterior e desfez eles 

---> git reflog:  Mostra um histórico mais detalhado da alterações que fizemos 


---> git reset resumos/aula-01.md (coloca aula-01.md em Untracked files)

---> git restore --staged resumos/aula-02.md : remover aula-02.md da nossa área de preparação 



