# GitHub Actions SAST Template

Modelo mínimo de GitHub Actions para executar análise estática de código com o Semgrep.

## Ciclo de desenvolvimento com DevSecOps

### Representação simplificada

```mermaid
flowchart LR
    P[Planejamento (Plan)] --> D[Desenvolvimento (Code)]
    D --> B[Construção (Build)]
    B --> S[Análise estática (SAST)]
    B --> C[Análise de dependências (SCA)]
    S --> T[Testes funcionais (Test)]
    C --> T
    T --> A[Aplicação em execução]
    A --> X[Análise dinâmica (DAST)]
    X --> R[Liberação (Release)]
    R --> I[Implantação (Deployment)]
    I --> O[Operação (Operate)]
    O --> M[Monitoramento (Monitor)]
    M --> P
```

DevSecOps integra a segurança ao longo do ciclo. O SAST, o SCA e o DAST são verificações que podem ser incorporadas em diferentes etapas. Este repositório automatiza somente o SAST. SCA e DAST aparecem no diagrama para contextualizar o processo.

**Liberação (Release)** é preparar e aprovar uma versão para entrega. **Implantação (Deployment)** é disponibilizar essa versão em um ambiente. **Operação (Operate)** acompanha o software em uso, enquanto **Monitoramento (Monitor)** observa seu comportamento e fornece sinais para os próximos ajustes.

## O que cada parte do workflow faz

- `name` Define o nome exibido na aba Actions.
- `on` Executa o workflow em um `push`, em um `pull_request` ou manualmente por `workflow_dispatch`.
- `permissions` Limita a permissão do token a leitura do conteúdo do repositório.
- `jobs.semgrep` Define o trabalho de análise realizado pelo Semgrep.
- `runs-on` Seleciona o runner Ubuntu hospedado pelo GitHub.
- `container.image` Executa as etapas dentro da imagem oficial do Semgrep.
- `actions/checkout@v7` Disponibiliza os arquivos do repositório no runner.
- `semgrep scan --config auto .` Analisa o código do diretório atual usando regras selecionadas automaticamente pelo Semgrep.

Uma execução concluída com sucesso indica que o workflow terminou. Os achados precisam ser revisados e validados pela equipe.

