# Tarefa4-Lab

##  COMP0463 Laboratório de Redes de Computadores - Turma 02

### Dannilo de Souza Costa
### 202000012669
### PDFormat - Uma aplicação de edição e formatação de arquivos texto e pdf
### ---------------------------------------------------------------------------------------------------------------------------

#### Como disponibilizar uma página HTML num container Docker no Laboratório Elan?

#### 1º Passo: Acessar o servidor do Elan
##### O container docker com sua página HTML será hospedado no servidor do Elan. Assim, o passo inicial a tomar é se conectar ao servidor. Para tanto, utilizaremos a ferramenta de acesso remoto Putty (https://www.putty.org/). Com o Putty já instalado em sua máquina, execute-o e preencha os campos "Host Name (or IP Address)" e "Port" com os valores 200.17.141.82 e 3333, em respectivo. O primeiro deles se refere ao IP público do servidor e o último à porta a qual ele atende.
##### Em seguida, clique em Open. Será aberta uma janela requisitando suas credenciais. No primeiro acesso, o login é o seu usuário do SIGAA e a senha a sua matrícula. No entanto, após o login, será requisitado a alteração dessa senha por uma padrão, essa será usada nas próximas sessões.


#### 2º Passo: Criar um conteiner Docker
##### Para criar o container execute o seguinte comando:
```bash
docker create -p <porta externa>:<porta interna> -it -v html:/var/www/html --name <nome_do_conteiner> python
```
##### Substitua os valores demarcados entre < > pelo número da porta externa, a qual será usada aplicação em Cedro, pelo número de porta interna, a qual será utiliizada dentro do conteiner e o nome do conteiner, respectivamente.
##### O comando deve ser algo parecido com isso:
```bash
docker create -p 14412:12144 -it -v html:/var/www/html --name webDannilo2 python
```

##### Importante: Certifique-se de que o número da porta externa e o nome do conteiner a serem utilizados não estão em uso. Ao executar o comando, se nenhum erro for retornado, não houve conflitos do nome ou número de porta com os demais conteineres.
##### Dica! Utilize o mesmo número para as portas interna e externa para evitar confusão 😅

#### 3º Passo: Iniciar o conteiner
##### Para iniciar o conteiner recém criado execute:
```bash
docker start <nome_do_conteiner>
```

#### 4º Passo: Verificar se o conteiner está em execução
##### Execute o comando a seguir e verifique se conteiner foi devidamente iniciado:
```bash
docker ps
```

#### 5º Passo: Acessar o conteiner
##### Para acessar o conteiner rode o seguite comando:
```bash
docker exec -it <nome_do_conteiner> /bin/bash
```
##### Após a execução desse comando, você estará dentro do docker. Dentro dele você realizará um clone do repositório do github que hospeda a página Web.

#### 6º Passo: Clonar repositório
##### Uma vez criado o repositório no github com o arquivo HTML. Clicando em Code, na opção HTTPS, copie o link e execute no terminal do conteiner:
```bash
git clone <link>
```

#### 7º Passo: Copiar o arquivo HTML
##### Após o passo 6, haverá, no diretório corrente, uma pasta de mesmo nome do repositório do github. O comando ls retornará o conteúdo presente no diretório atual e, certamente, o nome da pasta do repositório. O comando cd <folder> acessará a diretorio folder.
##### Você listar o conteúdo do diretório atual da seguinte forma:
```bash
ls
```
##### Você pode acessar a pasta utilizando o seguinte comando:
```bash
cd <nome_do_diretorio>
```
##### Copie o arquivo HTML para o diretório var/www/html:
```bash
cp <nome_do_arquivo.html> ../../../../var/www/html/
```

#### 8º Passo: Persistir o conteiner
##### Para salvar as alterações realizadas no conteiner execute o seguinte comando:
```bash
docker commit -a “<autor_da_modificacao>” -m “<nome_da_modificacao>” <nome_do_conteiner> <nome_do_repositorio>:<versao>
```
##### Substitua <autor_da_modificacao> pelo nome do responsável pela modificação. Nomeia a modificação substituindo o valor <nome_da_modificacao>. Dê também um nome ao repositório. O nome do repositório não deve conter letras maiúsculas. Por fim, o número da versão do conteiner, alterando a chave <versao>. Mantenha as aspas!
  
#### Pronto! O seu conteiner está salvo, armazenando sua página HTML e executando no Cedro, no laboratório Elan
  
  
