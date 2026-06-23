🏆 Sistema de Gerenciamento da Copa do Mundo FIFA 2026
📖 Descrição do Projeto

Este projeto consiste na modelagem de um banco de dados relacional para gerenciamento das informações da Copa do Mundo FIFA 2026.

O sistema foi projetado para armazenar dados relacionados aos países participantes, grupos, seleções, jogadores, funcionários técnicos, árbitros, estádios, jogos, resultados e classificação do torneio.

A modelagem segue os princípios de normalização de banco de dados, garantindo integridade, organização e redução de redundâncias.

🎯 Objetivos

O banco de dados permite:

Cadastrar países participantes.
Organizar seleções em grupos.
Gerenciar jogadores das seleções.
Gerenciar comissões técnicas e funcionários.
Registrar árbitros.
Controlar estádios e cidades-sede.
Agendar partidas.
Registrar resultados dos jogos.
Gerar classificações das equipes.
🏗️ Modelo Conceitual
Entidades Principais
Pessoa

Representa qualquer indivíduo cadastrado no sistema.

Jogador

Especialização de Pessoa responsável por representar atletas das seleções.

Funcionário

Especialização de Pessoa responsável por representar membros da comissão técnica e demais funcionários.

Árbitro

Especialização de Pessoa responsável pela arbitragem das partidas.

País

Representa os países participantes e também os países-sede da competição.

Grupo

Representa os grupos da fase inicial do torneio.

Time

Representa as seleções nacionais participantes.

Estádio

Representa os locais onde as partidas serão realizadas.

Jogo

Representa cada partida disputada.

Resultado

Armazena o placar oficial de cada partida.

Classificação

Armazena o desempenho das seleções durante a competição.

📊 Modelo Entidade-Relacionamento (MER)

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


🔗 Relacionamentos
Entidade 1	Relacionamento	Entidade 2
País	Possui	Time
País	Possui	Estádio
Grupo	Contém	Time
Time	Possui	Jogador
Time	Possui	Funcionário
Árbitro	Arbitra	Jogo
Estádio	Recebe	Jogo
Jogo	Gera	Resultado
Time	Possui	Classificação
📋 Regras de Negócio
RN01

Cada seleção pertence a apenas um grupo.

RN02

Cada jogador pertence a apenas uma seleção.

RN03

Cada funcionário pertence a apenas uma seleção.

RN04

Cada jogo possui exatamente um árbitro principal.

RN05

Cada jogo ocorre em apenas um estádio.

RN06

Cada jogo possui um time mandante e um visitante.

RN07

Cada resultado está associado a apenas um jogo.

RN08

Um estádio pertence a um país.

RN09

Uma seleção representa exatamente um país.

RN10

Uma pessoa pode ser Jogador, Funcionário ou Árbitro.

🗃️ Normalização

O modelo foi analisado segundo as formas normais:

Primeira Forma Normal (1FN)

✅ Atendida

Todos os atributos armazenam valores atômicos.

Segunda Forma Normal (2FN)

✅ Atendida

Todas as tabelas utilizam chaves primárias simples.

Terceira Forma Normal (3FN)

✅ Atendida

Não existem dependências transitivas entre atributos não-chave.

BCNF

✅ Atendida

Todas as dependências funcionais possuem determinantes candidatos a chave.

Quarta Forma Normal (4FN)

✅ Atendida

Não existem dependências multivaloradas.

Quinta Forma Normal (5FN)

✅ Atendida

As relações encontram-se adequadamente decompostas.

⚙️ Tecnologias Recomendadas
PostgreSQL
pgAdmin
DBeaver
Mermaid ER Diagram
GitHub
📁 Estrutura do Projeto
copa-do-mundo-2026/
│
├── README.md
├── scripts/
│   ├── create_tables.sql
│   ├── inserts.sql
│   └── views.sql
│
├── diagrams/
│   └── modelo-mermaid.md
│
└── docs/
    └── documentacao.pdf
🚀 Conclusão

Este projeto apresenta uma modelagem consistente para gerenciamento da Copa do Mundo FIFA 2026, contemplando as principais entidades e relacionamentos envolvidos na competição. O modelo foi estruturado com foco em integridade dos dados, facilidade de manutenção e aderência às boas práticas de modelagem relacional, servindo como uma base sólida para implementação em PostgreSQL ou outros SGBDs relacionais.
