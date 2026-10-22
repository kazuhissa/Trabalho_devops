Tabalho de Devops Log

Nome: Gabriel Kazuhissa Aizawa Lucio - RA: 250447

Visão Geral do Projeto

Este repositório reúne a implementação prática de esteiras de Integração Contínua (CI) e Entrega Contínua (CD) desenvolvidas com GitHub Actions para a disciplina de DevOps. O objetivo do projeto é automatizar processos essenciais do ciclo de vida de desenvolvimento de software, eliminando tarefas manuais como a validação de código, a geração de documentação do histórico de alterações e o empacotamento de versões para distribuição.

Funcionamento das Actions e Workflows

As automações estão organizadas no diretório .github/workflows/ e executam as seguintes rotinas:

Validação de CI (hello.yml)
Este workflow é acionado automaticamente a cada evento de push ou pull request direcionado à branch main. Ele aloca um ambiente virtual Ubuntu limpo, realiza o checkout do código e executa uma validação básica para garantir que a esteira de Integração Contínua está ativa e pronta para testes.

Geração Automática de Changelog (changelog.yml)
Executado após cada push confirmado na branch main. O fluxo utiliza comandos do Git para extrair os commits e atualizações recentes do repositório, formatando e escrevendo o histórico diretamente no arquivo CHANGELOG.md localizado na raiz do projeto através do robô github-actions[bot].

Empacotamento e Distribuição de Releases (release-package.yml)
Disparado no envio de uma nova tag de versão (no padrão v*) ou por execução manual via interface (workflow_dispatch). A automação seleciona a versão especificada, compacta o código-fonte em um arquivo no formato .zip e utiliza a interface de linha de comando do GitHub para anexar o pacote aos Assets da Release correspondente.
