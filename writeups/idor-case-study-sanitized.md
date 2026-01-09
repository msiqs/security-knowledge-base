# IDOR Case Study (Sanitized)

```mermaid
graph TD
    %% Definição dos Nós (Atores e Sistemas)
    Attacker[Atacante (Logado como ID: 999)]
    VictimResource(Recurso da Vítima (Ex: Fatura ID: 101))
    WebApp{Aplicação Web Vulnerável}
    AuthCheck{1. Verifica Sessão (Autenticação)}
    PermCheck{2. Verifica Permissão (Autorização)}
    DB[(Banco de Dados)]

    %% O Fluxo do Ataque
    Attacker -->|GET /fatura/101 (ID da Vítima)| WebApp
    WebApp --> AuthCheck

    %% O caminho normal que a aplicação faz
    AuthCheck -->|Usuário 999 Logado? SIM| PermCheck

    %% O PONTO DA FALHA: A aplicação pula a verificação de permissão
    PermCheck -.-> |FALHA: Verificação Inexistente ou Quebrada!| DB

    %% O Resultado
    DB -->|Retorna Fatura 101| WebApp
    WebApp -->|Vazamento de Dados Sensíveis| Attacker

    %% Estilizando o ponto da falha em vermelho para destaque
    classDef fail fill:#ffb3b3,stroke:#ff0000,stroke-width:2px,color:#000;
    class PermCheck fail;
```
