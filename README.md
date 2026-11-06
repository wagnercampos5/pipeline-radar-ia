# 🛰️ Radar de Inteligência de Mercado & Tecnologia

Pipeline automatizado de curadoria e inteligência competitiva com n8n self-hosted via Docker, integração com API REST pública e inteligência artificial via Google Gemini.

---

## 📌 Visão Geral da Solução
O sistema executa rotinas agendadas para coletar notícias e debates de tecnologia da API pública do Hacker News. Em seguida, os dados são filtrados por relevância via JavaScript, analisados semanticamente pelo modelo Gemini em português do Brasil e compilados em um relatório executivo em Markdown persistido localmente.

---

## 🛠️ Tecnologias Utilizadas
- **n8n Community (v2.x):** Orquestração e automação de fluxos de trabalho.
- **Docker & Docker Compose:** Containerização, isolamento de ambiente e persistência de volumes.
- **Google Gemini API:** Análise crítica de mercado, tradução, extração de impacto e classificação de tendências.
- **JavaScript (Node.js):** Filtragem, ordenação por pontuação e agregação de payloads JSON.
- **Hacker News Algolia API:** Fonte de dados públicos da indústria de tecnologia.

---

## ⚙️ Arquitetura do Pipeline
1. **Schedule Trigger:** Gatilho temporal configurado para execução automática periódica.
2. **HTTP Request:** Chamada GET aos endpoints do Hacker News para busca de tópicos de IA.
3. **Code (Filtro JS):** Sanitização dos itens, ordenação por engajamento e seleção dos top 5 artigos.
4. **Google Gemini (Message a Model):** Geração de resumos executivos, riscos, oportunidades e tendências em pt-BR.
5. **Code (Compilador JS):** Agregação de todas as análises individuais em um único documento Markdown.
6. **Convert to File:** Conversão do texto estruturado em payload binário (`.md`).
7. **Read/Write Files from Disk:** Gravação persistente do relatório na pasta mapeada do host (`meus_arquivos`).

---

## 🚀 Como Executar o Projeto Localmente

### 1. Pré-requisitos
- Docker e Docker Compose instalados e em execução.
- Chave de API ativa do Google AI Studio.

### 2. Inicialização do Ambiente
Suba o container do n8n com o comando:
docker compose up -d

### 3. Acesso e Importação
- Acesse a interface web em `http://localhost:5678`.
- Configure sua credencial da Google Gemini API no n8n.
- Importe o fluxo exportado (`pipeline-radar-ia.json`) e ative o workflow.
- O relatório compilado será gerado automaticamente no caminho local `./meus_arquivos/briefing_ia.md`.