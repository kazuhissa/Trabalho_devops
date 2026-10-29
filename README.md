Trabalho de DevOps - Log

Nome: Gabriel Kazuhissa Aizawa Lucio - RA: 250447

Visão Geral do Projeto

Este repositório reúne a implementação prática de esteiras de Integração Contínua (CI) e Entrega Contínua (CD) desenvolvidas com GitHub Actions para a disciplina de DevOps. O objetivo do projeto é automatizar processos essenciais do ciclo de vida de desenvolvimento de software, eliminando tarefas manuais como a validação de código, a geração de documentação do histórico de alterações e o empacotamento de versões para distribuição.

Funcionamento das Actions e Workflows

As automações estão organizadas no diretório .github/workflows/ e executam as seguintes rotinas:

Validação de CI (hello.yml)
Este workflow é acionado automaticamente a cada evento de push ou pull request direcionado à branch main. Ele aloca um ambiente virtual Ubuntu limpo, realiza o checkout do código e executa uma validação básica para garantir que a esteira de Integração Contínua está ativa e pronta para testes.

Geração Automática de Changelog (changelog.yml)
Este workflow é responsável por criar e atualizar automaticamente o arquivo CHANGELOG.md com o histórico dos últimos commits do projeto sempre que ocorre uma alteração na branch principal.

Gerar o arquivo CHANGELOG.md

- name: Generate CHANGELOG.md
  run: |
    echo "# Histórico de Alterações (Changelog)" > CHANGELOG.md
    echo "" >> CHANGELOG.md
    echo "## Commits Recentes" >> CHANGELOG.md
    git log --pretty=format:"* %s (%h)" -n 20 >> CHANGELOG.md
  
Nesta etapa, eu uso o comando echo para criar o arquivo CHANGELOG.md e escrever o título inicial dele. Em seguida, eu uso o comando git log para buscar os ultimos 20 commits do repositório, pegando apenas o título da mensagem e o código resumido do commit e tudo isso é formatado em uma lista e salvo dentro do arquivo.

Salvar e enviar o arquivo para o repositório

- name: Commit and push CHANGELOG.md
  run: |
    git config --global user.name "github-actions[bot]"
    git config --global user.email "github-actions[bot]@users.noreply.github.com"
    git add CHANGELOG.md
    git diff --quiet && git diff --staged --quiet || git commit -m "docs: update CHANGELOG.md [skip ci]"
    git push
  
Como o arquivo foi gerado dentro da máquina do GitHub, preciso salvar essa alteração de volta no projeto. Primeiro eu configuro o Git com o nome e e-mail do robô do GitHub Actions. Depois, adiciono o arquivo CHANGELOG.md na fila do Git. O script verifica se houve alguma mudança real no arquivo e, se houver, cria um commit automático e faz o push para o repositório. O termo [skip ci] serve para evitar que esse commit crie um loop infinito de execuções.

Empacotamento e Distribuição de Releases (release-package.yml)
Esta Action é responsável por empacotar o projeto em um arquivo .zip e anexá-lo automaticamente na aba de Releases do GitHub.

Como o fluxo funciona:

Gatilhos: O processo roda automaticamente quando eu publico uma nova versão (tag como v1.0.0) ou quando eu executo o fluxo manualmente na aba Actions.

Definição da Tag: O script identifica se a versão veio de um clique manual ou do push de uma tag do Git para saber qual código baixar.

Baixar o Código: O fluxo faz o checkout dos arquivos exatamente no ponto da versão selecionada.

Gerar o Pacote ZIP: Utiliza o comando git archive para compactar o código em um arquivo no formato Trabalho_devops-v1.0.0.zip.

Upload para a Release: Com a ferramenta do próprio GitHub (gh release) e o token da Action, o arquivo .zip é enviado e publicado diretamente na página de Release daquela versão.
