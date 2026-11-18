# 🛡️ Alerta Vivo — Urban Risk Intelligence Platform

> **Global Solution 2026.2 · Engenharia de Software · Contexto CitizenTech · FIAP**
> Protótipo funcional de uma plataforma que monitora riscos urbanos cotidianos (alagamentos, ilhas de calor e interrupções de serviços essenciais), **mostrando a origem e o nível de confiança de cada dado**.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-CDN-06B6D4?logo=tailwindcss&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-Vanilla-F7DF1E?logo=javascript&logoColor=black)
![Lucide](https://img.shields.io/badge/Icons-Lucide-F56565)
![Status](https://img.shields.io/badge/status-protótipo-blue)

🔗 **Demo online:** https://lucasc-c.github.io/Alerta_Vivo_GS2026/
🎬 **Vídeo de demonstração (até 3 min):** `<link do YouTube não listado>`
📄 **Documentação (requisitos, UML e arquitetura):** [`docs/Urban_Risk_Intelligence_Platform_Documentacao.md`](docs/Urban_Risk_Intelligence_Platform_Documentacao.md)

---

## 👥 Integrantes

| Nome completo | RM |
|---|---|
| Lucas do Carmo Cima | RM564964 |
| Arthur Ederson de Oliveira Silva | RM557079 |

---

## 📌 Sobre o projeto

Informação sobre riscos urbanos existe, mas está **fragmentada** entre sensores, bases públicas e grupos de mensagens, e chega **tarde** ou **sem credibilidade**. O Alerta Vivo:

1. **Recebe** dados de **sensores IoT**, **bases públicas oficiais** e **registros da comunidade**;
2. **Valida e classifica** cada evento pelo **nível de risco** (R = Severidade × Exposição) e pelo **nível de confiança** (C = 0,4F + 0,3K + 0,2A + 0,1Q);
3. **Prioriza** os alertas de P1 a P5 por uma matriz risco × confiança;
4. **Notifica** só quem está na área afetada, sempre exibindo **de onde veio a informação e quanto confiar nela**;
5. Trata dados pessoais conforme a **LGPD** (minimização, pseudonimização, consentimento granular e direitos do titular).

> ⚠️ Este repositório contém o **protótipo de front-end** (SPA em um único arquivo). Os dados são **simulados (mock)** em memória, mas seguem fielmente as regras de negócio RN01–RN09 da documentação. Não há backend nem coleta real de dados.

---

## 🖥️ Telas implementadas (10)

| ID | Tela | Requisitos atendidos |
|---|---|---|
| **T01** | Boas-vindas, login e consentimento LGPD (cidadão, visitante e agente com MFA) | RF14 · RNF07 · RNF09 |
| **T02** | Painel de acompanhamento: mapa interativo, filtros, zoom e bottom sheet | RF01 · RF02 · RF05 · RF06 · RF07 |
| **T03** | Lista de alertas ordenada por prioridade P1→P5, com filtros | RF05 · RF06 · RF08 |
| **T04** | Detalhe do alerta: linha do tempo, recomendações, corroborar/contestar | RF06 · RF08 · RF15 |
| **T05** | ★ **Origem e nível de confiança do dado**: gauge, decomposição F/K/A/Q, fontes e matriz de prioridade | RF06 · RNF05 · RNF07 |
| **T06** | Central de notificações: lida/não lida, abas e agrupamento anti-spam | RF09 · RF10 · RF16 |
| **T07** | Registro comunitário de ocorrência em 3 passos (≤ 3 toques) | RF03 · RNF05 · RNF09 |
| **T08** | Confirmação e acompanhamento do relato (stepper = Diagrama de Estados) | RF03 · RF16 |
| **T09** | Console da Defesa Civil / Operador: fila de validação, eventos ativos, interrupções, indicadores e auditoria | RF04 · RF11 · RF12 · RF17 · RNF08 |
| **T10** | Perfil, áreas monitoradas, preferências e painel de privacidade LGPD | RF13 · RF14 · RNF09 |

---

## ✨ Destaques funcionais

- **Regras de negócio executáveis:** risco, confiança e prioridade são **calculados em tempo real** pelas funções `calc()`, `kOf()` e `cOf()` e pela constante `MATRIX` (RN01–RN07).
- **Correlação de relatos (RF04):** um relato do mesmo tipo a até **500 m** de um evento ativo é **agrupado** a ele, e a confiança é recalculada (ex.: 47 → 62).
- **Validação humana:** ao validar no console, a confiança vai para **100** (selo *Validado pela Defesa Civil*), a prioridade é recalculada e o morador recebe um push.
- **Ciclo de vida completo:** `Reportado → Em validação → Confirmado → Alerta emitido → Em monitoramento → Encerrado / Descartado`, refletido na T04 (linha do tempo), na T08 (stepper) e no console.
- **Prazos de validação (RN07/RN09):** contagem regressiva na fila; quando o prazo estoura, o item aparece como **"Escalado"**.
- **Anti-spam (RN08):** atualizações do mesmo evento são agrupadas em uma notificação.
- **RBAC:** o perfil *Operadora* (Juliana) só acessa Interrupções e Indicadores.
- **Auditoria imutável (RNF08):** toda ação gera um registro encadeado por hash.
- **LGPD na prática:** consentimentos granulares, ID pseudônimo, fotos desfocadas, exportação real dos dados em JSON, correção e exclusão de conta.
- **Acessibilidade:** risco sempre com **cor + forma + texto** (círculo, triângulo, losango, octógono), `aria-label` nos controles, foco visível e suporte a `prefers-reduced-motion`.

---

## 🚀 Como executar

### Opção 1: abrir direto no navegador (mais simples)
1. Baixe ou clone o repositório:
   ```bash
   git clone https://github.com/LucasC-C/Alerta_Vivo_GS2026.git
   cd Alerta_Vivo_GS2026
   ```
2. Dê **duplo clique em `index.html`** ou arraste o arquivo para o Chrome, Edge, Firefox ou Safari.

> É preciso estar conectado à internet: Tailwind CSS, Lucide Icons e a fonte Inter são carregados por CDN.

### Opção 2: servidor local (recomendado para gravar o vídeo)
```bash
# Python 3
python -m http.server 8080

# ou Node.js
npx serve .
```
Depois, acesse **http://localhost:8080**.

### Requisitos
- Navegador moderno (Chrome 110+, Edge 110+, Firefox 115+, Safari 16+)
- Conexão com a internet (para as CDNs)
- **Nenhuma** instalação, build ou dependência local

---

## 🌐 Deploy

### GitHub Pages
1. Faça push do `index.html` para a branch `main` (na raiz do repositório).
2. No GitHub: **Settings → Pages → Build and deployment**.
3. Em *Source*, escolha **Deploy from a branch**, selecione **`main`** e a pasta **`/ (root)`**, e clique em **Save**.
4. Em 1 a 2 minutos o site fica disponível em https://lucasc-c.github.io/Alerta_Vivo_GS2026/.

### Vercel
```bash
npm i -g vercel
vercel --prod
```
(ou importe o repositório em [vercel.com/new](https://vercel.com/new); não é preciso configurar build).

### Netlify
Arraste a pasta do projeto em [app.netlify.com/drop](https://app.netlify.com/drop).

> ✅ Antes de entregar, teste o link em uma **janela anônima**, como pede o enunciado.

---

## 🎬 Roteiro de demonstração (fluxo principal)

| # | Tela | Ação |
|---|---|---|
| 1 | **T01** | Mostrar os consentimentos LGPD e clicar em **Continuar como cidadão** |
| 2 | **T02** | Mapa ao vivo; após ~3 s chega um **push** de alagamento Crítico |
| 3 | **T06 / T04** | Abrir a notificação e ver o detalhe do alerta |
| 4 | **T05** | Tocar no **Selo de Confiança** e mostrar a nota **86/100** decomposta em F, K, A e Q |
| 5 | **T04** | "Também estou vendo" recalcula a confiança (86 → 92) |
| 6 | **T07** | Relatar alagamento: tipo → local → **Enviar agora** (3 toques) |
| 7 | **T08** | O relato se junta ao evento da Rua Tietê; status "Em validação" |
| 8 | **T09** | Console: **Validar → Emitir alerta**; depois, em *Eventos ativos*, **Encerrar** |
| 9 | **T06 / T08** | O morador recebe "Seu relato foi confirmado" e o stepper avança |

### Controles do Modo Demonstração
| Controle | Função |
|---|---|
| Botões **T01…T10** (barra superior) | Pulam direto para qualquer tela |
| Teclas **1–9** e **0** | Atalhos para T01–T10 |
| Tecla **D** | Oculta/mostra a barra (para gravar a tela limpa) |
| **Push de teste** | Dispara uma notificação no celular simulado |
| **Relato de outro morador** | Coloca um novo item na fila de validação do console |
| **Resetar** | Restaura todos os dados iniciais |

---

## 🧮 Regras de negócio implementadas

| Regra | Implementação |
|---|---|
| **RN01** Severidade (S 1–5) | Faixas por tipo; `sevClientes()` para interrupções; intensidade do relato → S2/S3/S4 |
| **RN02** Exposição (E 1–3) | Por bairro (`BAIRROS`), considerando equipamentos sensíveis |
| **RN03** Risco | `R = S × E` → Baixo (1–3), Moderado (4–6), Alto (7–10), Crítico (11–15) |
| **RN04** Confiança | `C = 0,4F + 0,3K + 0,2A + 0,1Q`; K: 0/1/2/≥3 fontes = 0/50/80/100, fonte oficial = 100, −15 por contestação; validado = 100 |
| **RN05** Reputação | +5 se confirmado, −10 se descartado (limites 30–80); não é exibida publicamente |
| **RN06** Validação mínima | Bloqueia relato duplicado do mesmo usuário em < 10 min |
| **RN07** Matriz de prioridade | `MATRIX[risco][confiança]` → P1…P5; confiança Baixa nunca gera push |
| **RN08** Anti-spam | Agrupamento de atualizações do mesmo evento; P1 ignora o horário de silêncio |
| **RN09** Escalonamento e encerramento | Prazo estourado → "Escalado"; encerramento com motivo obrigatório |

---

## 🗂️ Estrutura

```text
.
├── index.html                                   # SPA completa: HTML + Tailwind (CDN) + JavaScript Vanilla
├── README.md
└── docs/
    ├── Urban_Risk_Intelligence_Platform_Documentacao.md   # requisitos, UML, arquitetura, telas, roteiro
    ├── Cola_para_o_Grupo_Confianca.md                     # contas de confiança explicadas
    ├── Diagrama_Sequencia_Alerta.png
    ├── Diagrama_Estados_Evento.png
    └── Arquitetura_Camadas.png
```

Organização interna do `index.html`:

```text
<script>
├── Relógio simulado (cenário às 18:14)
├── Catálogos (RISK, TIPOS, PRIO, BAIRROS)
├── Regras de negócio (calc, kOf, cOf, MATRIX, sevClientes, qRelato)
├── Dados mockados (seed: eventos E1–E10, notificações, personas)
├── Componentes (riskBadge, seal, prioChip, mapBase, marker…)
├── Views T01–T10
├── render() / go() — roteamento SPA
└── A — ações (validar, emitir, encerrar, relatar, LGPD…)
```

---

## 🧑‍🤝‍🧑 Personas

| Persona | Perfil | Onde aparece |
|---|---|---|
| **Marina Souza** | Moradora do Jardim Pantanal, enfermeira | App do cidadão (T01–T08, T10) |
| **Sgt. Ricardo Almeida** | Coordenador regional da Defesa Civil | Console: fila, eventos ativos, auditoria |
| **Juliana Torres** | Analista de operações de uma distribuidora de energia | Console: interrupções e indicadores |

---

## ⚠️ Limitações do protótipo

- Dados simulados em memória: ao recarregar a página, tudo volta ao estado inicial.
- O mapa é uma ilustração em SVG da Zona Leste de São Paulo, sem georreferenciamento real.
- Login, SMS, MFA e push são simulados.
- A arquitetura de produção (API Gateway, Kafka, PostGIS, módulo LGPD) está descrita na documentação técnica do projeto.

---

## 📄 Licença

Projeto acadêmico desenvolvido para a Global Solution 2026.2 da FIAP. Uso educacional.
