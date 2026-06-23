
# 🏆 Sistema de Gerenciamento da Copa do Mundo FIFA 2026

## 📖 Descrição do Projeto

Este projeto consiste na modelagem de um banco de dados relacional para gerenciamento das informações da Copa do Mundo FIFA 2026.

O sistema foi projetado para armazenar dados relacionados aos países participantes, grupos, seleções, jogadores, funcionários técnicos, árbitros, estádios, jogos, resultados e classificação do torneio.

A modelagem segue os princípios de normalização de banco de dados, garantindo integridade, organização e redução de redundâncias.

---

# 🎯 Objetivos

- Cadastrar países participantes.
- Organizar seleções em grupos.
- Gerenciar jogadores das seleções.
- Gerenciar comissões técnicas e funcionários.
- Registrar árbitros.
- Controlar estádios e cidades-sede.
- Agendar partidas.
- Registrar resultados dos jogos.
- Gerar classificações das equipes.

---

# 📊 Modelo Entidade-Relacionamento (MER)

```mermaid
erDiagram

    PESSOA {
        int id_pessoa PK
        string nome
        string cpf
        date data_nascimento
        string nacionalidade
    }

    PAIS {
        int id_pais PK
        string nome_pais
        string continente
    }

    GRUPO {
        int id_grupo PK
        string nome_grupo
    }

    TIME {
        int id_time PK
        string nome_time
        int id_pais FK
        int id_grupo FK
    }

    JOGADOR {
        int id_pessoa PK
        int numero_camisa
        string posicao
        int id_time FK
    }

    FUNCIONARIO {
        int id_pessoa PK
        string cargo
        decimal salario
        int id_time FK
    }

    ARBITRO {
        int id_pessoa PK
        string categoria
    }

    ESTADIO {
        int id_estadio PK
        string nome_estadio
        string cidade
        int capacidade
        int id_pais FK
    }

    JOGO {
        int id_jogo PK
        date data_jogo
        time hora_jogo
        string fase
        int id_arbitro FK
        int id_estadio FK
        int time_casa FK
        int time_visitante FK
    }

    RESULTADO {
        int id_resultado PK
        int gols_time_casa
        int gols_time_visitante
        int id_jogo FK
    }

    CLASSIFICACAO {
        int id_classificacao PK
        int id_time FK
        int pontos
        int vitorias
        int empates
        int derrotas
        int saldo_gols
    }

    PESSOA ||--o| JOGADOR : especializacao
    PESSOA ||--o| FUNCIONARIO : especializacao
    PESSOA ||--o| ARBITRO : especializacao

    PAIS ||--o{ TIME : possui
    PAIS ||--o{ ESTADIO : possui

    GRUPO ||--o{ TIME : contem

    TIME ||--o{ JOGADOR : possui
    TIME ||--o{ FUNCIONARIO : possui
    TIME ||--|| CLASSIFICACAO : classificado

    ESTADIO ||--o{ JOGO : recebe

    TIME ||--o{ JOGO : time_casa
    TIME ||--o{ JOGO : time_visitante

    ARBITRO ||--o{ JOGO : arbitra

    JOGO ||--|| RESULTADO : gera
```

## ✅ Normalização

- 1FN: Atendida
- 2FN: Atendida
- 3FN: Atendida
- BCNF: Atendida
- 4FN: Atendida
- 5FN: Atendida

## 🚀 Tecnologias

- PostgreSQL
- pgAdmin
- DBeaver
- Mermaid
- GitHub

## 📌 Conclusão

Modelo de banco de dados desenvolvido para a Copa do Mundo FIFA 2026, contemplando países, grupos, seleções, jogadores, funcionários, árbitros, estádios, jogos, resultados e classificação, seguindo boas práticas de modelagem e normalização.
