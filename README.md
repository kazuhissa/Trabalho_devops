Tabalho de Devops Log

Nome: Gabriel Kazuhissa Aizawa Lucio - RA: 250447

Resumo do Projeto

Este repositório reúne a implementação prática de esteiras de Integração Contínua (CI) e Entrega Contínua (CD) desenvolvidas com GitHub Actions para a disciplina de DevOps. O objetivo principal é demonstrar a automação de processos essenciais do ciclo de vida de desenvolvimento de software, abrangendo desde a validação básica de código até a geração de documentação de histórico e a distribuição de pacotes de release.

Arquitetura dos Workflows

A estrutura de automação está organizada no diretório .github/workflows/ e é composta por três fluxos independentes:

Validação de CI (hello.yml)

Disparado a cada push ou pull request direcionado à branch main. O job executa um ambiente virtual Ubuntu para realizar o checkout do código e validar se a esteira principal de testes e integração está operacional.

Geração de Changelog (changelog.yml)

Executado automaticamente após atualizações na branch main. O script coleta as mensagens dos commits mais recentes e compila o histórico formatado diretamente no arquivo CHANGELOG.md na raiz do projeto, mantendo a documentação técnica sempre atualizada.

Empacotamento e Publicação de Release (release-package.yml)

Acionado quando uma nova tag de versão (no padrão v*) é enviada ao repositório ou por disparo manual via interface do GitHub Actions. A rotina gera um arquivo comprimido .zip contendo o código da versão correspondente e faz o upload do pacote diretamente nos Assets da Release no GitHub via CLI.
