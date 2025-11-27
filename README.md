Modelo de agente FastAPI LangGraph
Um modelo FastAPI pronto para produção para a criação de aplicações de agentes de IA com integração LangGraph. Este modelo fornece uma base sólida para a construção de serviços de agentes de IA escaláveis, seguros e de fácil manutenção.

🌟 Recursos
Arquitetura pronta para produção

FastAPI para endpoints de API assíncronos de alto desempenho com otimização uvloop
Integração do LangGraph para fluxos de trabalho de agentes de IA com persistência de estado.
Langfuse para observabilidade e monitoramento de LLM
Registro estruturado com formatação específica do ambiente e contexto de solicitação.
Limitação de taxa com regras configuráveis ​​por endpoint
PostgreSQL com pgvector para persistência de dados e armazenamento vetorial.
Suporte para Docker e Docker Compose
Métricas do Prometheus e painéis do Grafana para monitoramento
Recursos de IA e LLM

Memória de longo prazo com mem0ai e pgvector para armazenamento de memória semântica
Serviço LLM com lógica de repetição automática usando tenacidade
Suporte a vários modelos LLM (GPT-4o, GPT-4o-mini, GPT-5, GPT-5-mini, GPT-5-nano)
Transmissão de respostas para interações de chat em tempo real
Capacidades de chamada de ferramentas e execução de funções
Segurança

Autenticação baseada em JWT
Gestão de sessões
sanitização de entrada
Configuração CORS
Proteção de limitação de taxa
Experiência do desenvolvedor

Configuração específica do ambiente com carregamento automático de arquivos .env
Sistema de registro abrangente com vinculação de contexto
Estrutura de projeto clara seguindo as melhores práticas
Dicas de digitação ao longo do texto para melhor suporte do IDE
Configuração de desenvolvimento local simplificada com comandos Makefile.
Lógica de repetição automática com recuo exponencial para resiliência
Estrutura de Avaliação do Modelo

Avaliação automatizada de resultados de modelos com base em métricas
Integração com Langfuse para análise de traços
Relatórios JSON detalhados com métricas de sucesso/falha
Interface de linha de comando interativa
Métricas de avaliação personalizáveis
🚀 Início Rápido
Pré-requisitos
Python 3.13+
PostgreSQL ( consulte Configuração do banco de dados )
Docker e Docker Compose (opcional)
Configuração do ambiente
Clone o repositório:
git clone <repository-url>
cd <project-directory>
Criar e ativar um ambiente virtual:
uv sync
Copie o arquivo de ambiente de exemplo:
cp .env.example .env.[development|staging|production] # e.g. .env.development
Atualize o .envarquivo com sua configuração (consulte .env.examplepara referência).
Configuração do banco de dados
Crie um banco de dados PostgreSQL (por exemplo, Supabase ou PostgreSQL local).
Atualize as configurações de conexão do banco de dados no seu .envarquivo:
POSTGRES_HOST=db
POSTGRES_PORT=5432
POSTGRES_DB=cool_db
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
Você não precisa criar as tabelas manualmente, o ORM cuidará disso para você. Mas, caso encontre algum problema, execute o schemas.sqlarquivo para criar as tabelas manualmente.
Executando o aplicativo
Desenvolvimento Local
Instalar dependências:
uv sync
Execute o aplicativo:
make [dev|staging|prod] # e.g. make dev
Acesse a interface do Swagger:
http://localhost:8000/docs
Usando o Docker
Crie e execute com Docker Compose:
make docker-build-env ENV=[development|staging|production] # e.g. make docker-build-env ENV=development
make docker-run-env ENV=[development|staging|production] # e.g. make docker-run-env ENV=development
Acesse a pilha de monitoramento:
# Prometheus metrics
http://localhost:9090

# Grafana dashboards
http://localhost:3000
Default credentials:
- Username: admin
- Password: admin
A configuração do Docker inclui:

Aplicação FastAPI
banco de dados PostgreSQL
Prometheus para coleta de métricas
Grafana para visualização de métricas
Painéis pré-configurados para:
Métricas de desempenho da API
estatísticas de limitação de taxa
Desempenho do banco de dados
Utilização de recursos do sistema
📊 Avaliação do Modelo
O projeto inclui uma estrutura de avaliação robusta para medir e acompanhar o desempenho do modelo ao longo do tempo. O avaliador busca automaticamente os dados de rastreamento do Langfuse, aplica as métricas de avaliação e gera relatórios detalhados.

Executando avaliações
Você pode executar avaliações com diferentes opções usando os comandos Makefile fornecidos:

# Interactive mode with step-by-step prompts
make eval [ENV=development|staging|production]

# Quick mode with default settings (no prompts)
make eval-quick [ENV=development|staging|production]

# Evaluation without report generation
make eval-no-report [ENV=development|staging|production]
Características de avaliação
CLI interativa : Interface amigável com saída colorida e barras de progresso.
Configuração flexível : defina valores padrão ou personalize em tempo de execução.
Relatórios detalhados : Relatórios JSON com métricas abrangentes, incluindo:
Taxa de sucesso geral
Desempenho específico da métrica
Informações sobre duração e horários
Detalhes de sucesso/falha em nível de rastreamento
Personalizando métricas
As métricas de avaliação são definidas em evals/metrics/prompts/arquivos Markdown:

Crie um novo arquivo Markdown (por exemplo, my_metric.md) no diretório de prompts.
Defina os critérios de avaliação e a lógica de pontuação.
O avaliador irá detectar e aplicar automaticamente sua nova métrica.
Relatórios de visualização
Os relatórios são gerados automaticamente no evals/reports/diretório com os registros de data e hora no nome do arquivo:

evals/reports/evaluation_report_YYYYMMDD_HHMMSS.json
Cada relatório inclui:

Estatísticas de alto nível (contagem total de rastros, taxa de sucesso, etc.)
Métricas de desempenho por métrica
Informações detalhadas em nível de rastreamento para depuração
🔧 Configuração
O aplicativo utiliza um sistema de configuração flexível com configurações específicas para cada ambiente:

.env.development- Configurações de desenvolvimento local
.env.staging- Configurações do ambiente de teste
.env.production- Configurações do ambiente de produção
Variáveis ​​de ambiente
As principais variáveis ​​de configuração incluem:

# Application
APP_ENV=development
PROJECT_NAME="FastAPI LangGraph Agent"
DEBUG=true

# Database
POSTGRES_HOST=localhost
POSTGRES_PORT=5432
POSTGRES_DB=mydb
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres

# LLM Configuration
OPENAI_API_KEY=your_openai_api_key
DEFAULT_LLM_MODEL=gpt-4o
DEFAULT_LLM_TEMPERATURE=0.7
MAX_TOKENS=4096

# Long-Term Memory
LONG_TERM_MEMORY_COLLECTION_NAME=agent_memories
LONG_TERM_MEMORY_MODEL=gpt-4o-mini
LONG_TERM_MEMORY_EMBEDDER_MODEL=text-embedding-3-small

# Observability
LANGFUSE_PUBLIC_KEY=your_public_key
LANGFUSE_SECRET_KEY=your_secret_key
LANGFUSE_HOST=https://cloud.langfuse.com

# Security
SECRET_KEY=your_secret_key_here
ACCESS_TOKEN_EXPIRE_MINUTES=30

# Rate Limiting
RATE_LIMIT_ENABLED=true
🧠 Memória de longo prazo
O aplicativo inclui um sofisticado sistema de memória de longo prazo baseado em mem0ai e pgvector:

Características
Armazenamento de memória semântica : Armazena e recupera memórias com base na similaridade semântica.
Memórias específicas do usuário : Cada usuário possui seu próprio espaço de memória isolado.
Gerenciamento automático de memória : as memórias são extraídas, armazenadas e recuperadas automaticamente.
Busca vetorial : Utiliza pgvector para busca eficiente de similaridade.
Modelos Configuráveis : Modelos separados para processamento de memória e incorporações.
Como funciona
Adição de memória : Durante as conversas, informações importantes são extraídas e armazenadas automaticamente.
Recuperação de memória : memórias relevantes são recuperadas com base no contexto da conversa.
Busca na memória : A busca semântica encontra memórias relacionadas em conversas.
Atualizações de memória : As memórias existentes podem ser atualizadas à medida que novas informações se tornam disponíveis.
🤖 Serviço LLM
O serviço LLM oferece interações robustas com modelos de linguagem, prontas para produção, com lógica de repetição automática e suporte a múltiplos modelos.

Características
Suporte a múltiplos modelos : Suporte pré-configurado para GPT-4o, GPT-4o-mini, GPT-5 e variantes do GPT-5.
Tentativas automáticas : Utiliza tenacidade para lógica de repetição com recuo exponencial.
Configuração de raciocínio : os modelos GPT-5 suportam níveis de esforço de raciocínio configuráveis.
Ajustes específicos para cada ambiente : parâmetros diferentes para desenvolvimento e produção.
Mecanismos de contingência : Degradação controlada quando os modelos primários falham.
Modelos suportados
Modelo	Caso de uso	Esforço de raciocínio
gpt-5	Tarefas de raciocínio complexo	Médio
gpt-5-mini	Desempenho equilibrado	Baixo
gpt-5-nano	Respostas rápidas	Mínimo
gpt-4o	cargas de trabalho de produção	N / D
gpt-4o-mini	tarefas com boa relação custo-benefício	N / D
Configuração de repetição
Tentativas automáticas em caso de timeouts da API, limites de taxa e erros temporários.
Número máximo de tentativas : 3
Estratégia de espera : Recuo exponencial (1s, 2s, 4s)
Registro de logs : Todas as tentativas de repetição são registradas com contexto.
📝 Registro Avançado
O aplicativo usa structlog para registro estruturado e contextual com rastreamento automático de solicitações.

Características
Registro estruturado : Todos os registros são estruturados com campos consistentes.
Contexto da solicitação : Vinculação automática de request_id, session_id e user_id.
Formatação específica do ambiente : JSON em produção, console colorido em desenvolvimento.
Rastreamento de desempenho : registro automático da duração e do status das solicitações.
Rastreamento de exceções : rastreamento completo da pilha de chamadas com preservação do contexto.
Middleware de contexto de registro
Cada solicitação recebe automaticamente:

ID de solicitação exclusivo
ID da sessão (se autenticado)
ID do usuário (se autenticado)
Caminho e método da solicitação
Estado e duração da resposta
Padrões de formato de log
Nomes de eventos : minúsculas_com_sublinhados
Sem strings F : passe variáveis ​​como argumentos nomeados para filtragem adequada.
Vinculação de contexto : sempre inclua IDs e contexto relevantes.
Níveis apropriados : depuração, informação, aviso, erro, exceção
⚡ Otimizações de desempenho
Integração uvloop
O aplicativo utiliza uvloop para melhor desempenho assíncrono (habilitado automaticamente via Makefile):

Melhorias de desempenho :

Operações asyncio 2 a 4 vezes mais rápidas
Menor latência para tarefas com uso intensivo de E/S
Melhor gerenciamento do pool de conexões
Uso reduzido da CPU para solicitações simultâneas
Agrupamento de conexões
Banco de dados : Agrupamento de conexões assíncronas com tamanho de pool configurável.
LangGraph Checkpointing : Pool de conexões compartilhadas para persistência de estado
Redis (opcional): Pool de conexões para cache
Estratégia de cache
Somente as respostas bem-sucedidas são armazenadas em cache.
TTL configurável com base na volatilidade dos dados.
Invalidação de cache em atualizações
Suporta cache Redis ou em memória.
🔌 Referência da API
Pontos de extremidade de autenticação
POST /api/v1/auth/register- Registrar um novo usuário
POST /api/v1/auth/login- Autenticar e receber token JWT
POST /api/v1/auth/logout- Sair e invalidar a sessão
Pontos de extremidade de bate-papo
POST /api/v1/chatbot/chat- Enviar mensagem e receber resposta
POST /api/v1/chatbot/chat/stream- Enviar mensagem com resposta em fluxo contínuo
GET /api/v1/chatbot/history- Obter histórico de conversas
DELETE /api/v1/chatbot/history- Limpar histórico de bate-papo
Saúde e monitoramento
GET /health- Verificação de integridade com status do banco de dados
GET /metrics- Ponto de extremidade de métricas do Prometheus
Para obter documentação detalhada da API, visite /docs(Swagger UI) ou /redoc(ReDoc) ao executar o aplicativo.

📚 Estrutura do Projeto
whatsapp-food-order/
├── app/
│   ├── api/
│   │   └── v1/
│   │       ├── auth.py              # Authentication endpoints
│   │       ├── chatbot.py           # Chat endpoints
│   │       └── api.py               # API router aggregation
│   ├── core/
│   │   ├── config.py                # Configuration management
│   │   ├── logging.py               # Logging setup
│   │   ├── metrics.py               # Prometheus metrics
│   │   ├── middleware.py            # Custom middleware
│   │   ├── limiter.py               # Rate limiting
│   │   ├── langgraph/
│   │   │   ├── graph.py             # LangGraph agent
│   │   │   └── tools.py             # Agent tools
│   │   └── prompts/
│   │       ├── __init__.py          # Prompt loader
│   │       └── system.md            # System prompts
│   ├── models/
│   │   ├── user.py                  # User model
│   │   └── session.py               # Session model
│   ├── schemas/
│   │   ├── auth.py                  # Auth schemas
│   │   ├── chat.py                  # Chat schemas
│   │   └── graph.py                 # Graph state schemas
│   ├── services/
│   │   ├── database.py              # Database service
│   │   └── llm.py                   # LLM service with retries
│   ├── utils/
│   │   ├── __init__.py
│   │   └── graph.py                 # Graph utility functions
│   └── main.py                      # Application entry point
├── evals/
│   ├── evaluator.py                 # Evaluation logic
│   ├── main.py                      # Evaluation CLI
│   ├── metrics/
│   │   └── prompts/                 # Evaluation metric definitions
│   └── reports/                     # Generated evaluation reports
├── grafana/                         # Grafana dashboards
├── prometheus/                      # Prometheus configuration
├── scripts/                         # Utility scripts
├── docker-compose.yml               # Docker Compose configuration
├── Dockerfile                       # Application Docker image
├── Makefile                         # Development commands
├── pyproject.toml                   # Python dependencies
├── schema.sql                       # Database schema
├── SECURITY.md                      # Security policy
└── README.md                        # This file
