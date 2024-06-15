# Guia de Configuração e Uso do Git

comandos do curso:



```bash
# Configurando o Git
git config --global user.name 'Seu Nome'                # Define o nome do usuário para commits
git config --global user.email 'seu@email.com'          # Define o e-mail do usuário para commits

# Criando Arquivos
echo "Conteúdo do arquivo" > nome_do_arquivo.txt        # Cria um arquivo com conteúdo
touch nome_do_arquivo.txt                               # Cria um arquivo vazio
cat > nome_do_arquivo.txt                               # Cria um arquivo vazio

# Mudando o Status de um Arquivo
git add [arquivo]                                       # Adiciona um arquivo específico para o stage
git add .                                               # Adiciona todos os arquivos modificados para o stage
git rm --cached [arquivo]                               # Remove arquivo da stage area
git restore --staged [arquivo]                          # Remove arquivo modificado da stage area
git restore --staged .                                  # Remove todos os arquivos modificados da stage area
git commit -m 'Mensagem'                                # Cria um commit com mensagem
git commit -am 'Mensagem'                               # Adiciona todos os arquivos modificados e faz commit com mensagem

# Recuperar um Ponto do Histórico
git reset --soft HEAD~                                  # Volta um commit mantendo alterações no diretório de trabalho
git reset --hard HEAD~                                  # Volta um commit removendo todas as alterações
git reset --soft [hash]                                 # Volta para um commit específico mantendo alterações
git reset --hard [hash]                                 # Volta para um commit específico removendo alterações
git log --pretty=oneline -p -2                          # Mostra os últimos dois commits com diferenças detalhadas
git checkout HEAD~2                                     # Volta 2 commits
git checkout HEAD~~                                     # Volta 2 commits
git checkout main                                       # Volta para a branch padrão
git log --pretty=oneline                                # Mostra onde o HEAD está apontando

# Trabalhando com Branches
git branch                                              # Lista branches disponíveis
git checkout -b [nome]                                  # Cria e muda para uma nova branch
git checkout -b [nova] [antiga]                         # Cria nova branch a partir de uma antiga
git checkout [nome]                                     # Muda para uma branch específica
git branch -d [nome]                                    # Deleta uma branch
git merge [branch]                                      # Faz merge de uma branch na atual
git log --pretty=oneline --graph                        # Mostra o histórico com gráfico

# Usando o Rebase
git rebase [branch]                                     # Rebase da branch atual em outra
git log --pretty=oneline --graph                        # Visualização do histórico

# Aliases para Comandos
git config --global alias.CAM 'commit -am'              # Cria alias global para commit -am
git tag -a [tag] -m [mensagem]                          # Cria uma tag anotada
git tag                                                 # Lista todas as tags
git remote add origin https://github.com/SeuUsuario/SeuRepositorio.git  # Adiciona um repositório remoto
git push origin main                                    # Envia alterações para o repositório remoto
git pull origin main                                    # Baixa alterações do repositório remoto
git push origin main --tags                             # Envia tags para o repositório remoto

# Configurando SSH para GitHub
ssh-keygen -t rsa -b 4096 -C "seu@email.com"            # Gera uma chave SSH
ls ~/.ssh                                               # Lista chaves SSH
cat ~/.ssh/id_rsa.pub    

#Criaiado repositorio git via comando
echo "# empty" >> README.md                             # Adiciona um cabeçalho vazio ao arquivo README.md
git init                                               # Inicializa um repositório Git local
git add README.md                                      # Adiciona o arquivo README.md ao stage area
git commit -m "first commit"                           # Cria o primeiro commit com a mensagem "first commit"
git branch -M main                                     # Renomeia a branch para 'main'

#adicionado origen e carregando mundancas
git remote add origin https://github.com/LdeAlejandro/empty.git   # Adiciona o repositório remoto chamado 'origin'
git push -u origin main                                # Envia o commit inicial para o branch 'main' do repositório remoto 'origin'



                               # Exibe chave pública SSH
```



## Configurando o Git

Antes de começar a usar o Git, precisamos definir quem somos. Isso é feito configurando nosso nome e e-mail globalmente. Isso garante que todas as suas futuras alterações sejam atribuídas corretamente.

```bash
git config --global user.name 'Seu Nome'                # Define o nome do usuário que será associado aos commits
git config --global user.email 'seu@email.com'          # Define o e-mail do usuário que será associado aos commits
```

## Criando Arquivos

### Criar um arquivo e adicionar conteúdo:
```bash
echo "Conteúdo do arquivo" > nome_do_arquivo.txt        # Cria um arquivo chamado nome_do_arquivo.txt e adiciona a linha "Conteúdo do arquivo" a ele
```

### Criar um arquivo vazio:
```bash
touch nome_do_arquivo.txt                               # Cria um arquivo vazio chamado nome_do_arquivo.txt
```

### Criar um arquivo com múltiplas linhas de conteúdo:
```bash
cat > nome_do_arquivo.txt << EOL
Primeira linha do arquivo
Segunda linha do arquivo
Terceira linha do arquivo
EOL                                                    # Cria um arquivo chamado nome_do_arquivo.txt e adiciona várias linhas de conteúdo
```

## Mudando o Status de um Arquivo

### Adicionar um arquivo para o Stage:
```bash
git add [arquivo]                                       # Adiciona um arquivo específico para a área de stage
git add .                                               # Adiciona todos os arquivos modificados para a área de stage
```

### Remover um arquivo do Stage:
```bash
git rm --cached [arquivo]                               # Remove um arquivo da área de stage, mas mantém o arquivo no diretório de trabalho
git restore --staged [arquivo]                          # Remove um arquivo modificado da área de stage
git restore --staged .                                  # Remove todos os arquivos modificados da área de stage
```

### Commitar/Enviar o Stage:
```bash
git commit -m 'Mensagem'                                # Cria um commit com uma mensagem descritiva fornecida pelo usuário
git commit -am 'Mensagem'                               # Adiciona todos os arquivos modificados e cria um commit com uma mensagem descritiva
```

## Recuperar um Ponto do Histórico

### Voltando 1 commit:
```bash
git reset --soft HEAD~                                  # Volta um commit, mantendo as alterações no diretório de trabalho (as alterações ficam no estado de 'unstaged')
git reset --hard HEAD~                                  # Volta um commit, removendo todas as alterações no diretório de trabalho e na área de stage (volta exatamente para o snapshot do commit anterior)
```

### Voltando para um commit específico:
```bash
git reset --soft [hash]                                 # Volta para um commit específico, identificado pelo hash, mantendo as alterações no diretório de trabalho
git reset --hard [hash]                                 # Volta para um commit específico, identificado pelo hash, removendo todas as alterações no diretório de trabalho e na área de stage
```

### Ver diferenças antes de resetar:
```bash
git log --pretty=oneline -p -2                          # Mostra os dois últimos commits com as diferenças detalhadas (patches) entre eles
```

## O que é o HEAD?

O HEAD está sempre apontando para o commit que estamos usando. Podemos navegar entre commits utilizando o HEAD.

### Exemplo de navegação:
```bash
git checkout HEAD~2                                     # Volta 2 commits a partir do commit atual
git checkout HEAD~~                                     # Volta 2 commits a partir do commit atual (equivalente ao comando anterior)
git checkout main                                       # Volta para a branch padrão (geralmente master ou main)
```

### Ver onde o HEAD está apontando:
```bash
git log --pretty=oneline                                # Mostra o log dos commits em uma linha, indicando onde o HEAD está apontando
```

## Trabalhando com Branches

### Ver branches:
```bash
git branch                                              # Lista todas as branches disponíveis
```

### Criar uma nova branch:
```bash
git checkout -b [nome]                                  # Cria e muda para uma nova branch chamada [nome]
git checkout -b [nova] [antiga]                         # Cria uma nova branch [nova] a partir da branch [antiga] e muda para ela
```

### Mudar para outra branch:
```bash
git checkout [nome]                                     # Muda para a branch chamada [nome]
```

### Apagar um branch:
```bash
git branch -d [nome]                                    # Apaga a branch chamada [nome] (não pode estar na branch que está sendo apagada)
```

## Merge e Rebase

### Usando o merge:
```bash
git merge [branch]                                      # Faz merge da branch [branch] na branch atual
```

### Visualizar merge:
```bash
git log --pretty=oneline --graph                        # Mostra o log dos commits em uma linha com uma representação gráfica do histórico de commits (útil para visualizar merges)
```

### Usando o rebase:
```bash
git rebase [branch]                                     # Rebase a branch atual na branch [branch]
```

### Dica para visualizar o log:
```bash
git log --pretty=oneline --graph                        # Mostra o log dos commits em uma linha com uma representação gráfica do histórico de commits
```

## Alias para Comandos

Para economizar digitação, podemos criar alias para comandos repetitivos.

### Exemplos:
```bash
git config --global alias.CAM 'commit -am'              # Cria um alias global chamado CAM para o comando commit -am
git config alias.logpg 'log --pretty=oneline --graph'   # Cria um alias local chamado logpg para o comando log --pretty=oneline --graph
```

## Trabalhando com Tags

### Criar uma tag:
```bash
git tag -a [tag] -m [mensagem]                          # Cria uma tag anotada chamada [tag] com a mensagem [mensagem]
```

### Ver tags:
```bash
git tag                                                 # Lista todas as tags
```

## Trabalhando com Repositórios Remotos

### Adicionar um repositório remoto:
```bash
git remote add origin https://github.com/SeuUsuario/SeuRepositorio.git  # Adiciona um repositório remoto chamado origin com a URL especificada
```

### Enviar atualizações para o repositório remoto:
```bash
git push origin main                                    # Envia as alterações da branch main para o repositório remoto origin
```

### Baixar atualizações do repositório remoto:
```bash
git pull origin main                                    # Baixa e mescla as alterações da branch main do repositório remoto origin com a branch atual
```

### Enviar tags para o repositório remoto:
```bash
git push origin main --tags                             # Envia as tags para o repositório remoto origin
```

## Configurar SSH para GitHub

### Criar uma chave SSH:
```bash
ssh-keygen -t rsa -b 4096 -C "seu@email.com"            # Gera uma nova chave SSH com 4096 bits usando o e-mail fornecido (necessário usar o e-mail do GitHub)
```

### Verificar chaves SSH:
```bash
ls ~/.ssh                                               # Lista as chaves SSH no diretório .ssh
```

### Exibir a chave pública:
```bash
cat ~/.ssh/id_rsa.pub                                   # Mostra o conteúdo da chave pública SSH, que pode ser adicionada ao GitHub para autenticação
```

Para mais detalhes, consulte a [documentação oficial do Git](https://git-scm.com/docs).
