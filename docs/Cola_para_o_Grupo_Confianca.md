# Cola para o Grupo — como a confiança é calculada

**Fórmula (RN04):** `C = 0,4·F + 0,3·K + 0,2·A + 0,1·Q`
- **F** (fonte): sensor calibrado = 90 · fonte oficial = 95 · relato = reputação do autor (30–80)
- **K** (corroboração): outras fontes independentes → 0 = 0 · 1 = 50 · 2 = 80 · 3 ou mais = 100 (−15 por contestação)
- **A** (atualidade): 100 até 5 min; depois cai ~1,8 ponto por minuto e zera aos 60 min
- **Q** (qualidade): relato = foto +40 · GPS +30 · descrição +30
- **Classes:** Alta ≥ 75 · Média 50–74 · Baixa < 50 · validado por agente = 100

---

## 1) Av. Marechal Tito (E1) = 86

| Fator | Valor | Por quê | × peso | Pontos |
|---|---|---|---|---|
| F | 90 | Fonte principal: pluviômetro PLV-0231, calibrado | × 0,4 | **36** |
| K | 80 | 2 fontes confirmam: sensor de nível CRG-009 + 1 relato | × 0,3 | **24** |
| A | 95 | Idade média de 8 min → 100 − 3 × 1,82 ≈ 95 | × 0,2 | **19** |
| Q | 70 | Sensores ok, mas o relato não tem foto | × 0,1 | **7** |
| | | | **Total** | **86 → Alta** |

**Risco:** S4 (55 mm/h) × E3 (escola a 200 m) = **12 → Crítico**.
**Crítico + Alta = P1:** alerta automático, sem agente, com push + SMS.

## 2) Rua Tietê (E7): de 47 para 62

**Antes (1 relato isolado):**
`0,4×50 + 0,3×0 + 0,2×100 + 0,1×70 = 20 + 0 + 20 + 7 = 47` → **Baixa** (fica só na fila, sem push)

**A Marina relata a ~160 m (menos de 500 m, mesmo tipo) → o relato é agrupado ao evento:**
- **K:** 0 → **50** (agora existe 1 fonte independente) → +15 pontos
- **F:** continua **50** (a fonte principal é o relato original)
- **A:** continua **100** (dado novo)
- **Q:** média entre o relato antigo (70) e o da Marina (foto 40 + GPS 30 = 70) = **70**

**Depois:** `20 + 15 + 20 + 7 = 62` → **Média** (continua na fila, P4)

**Agente valida → C = 100** → Moderado (R = 3 × 2 = 6) + confiança Alta = **P3** → o botão "Emitir alerta" é liberado.

> **Regra de bolso:** uma fonte a mais é o que mais pesa (K vale 30%). Sozinha, ela levou o evento de Baixa para Média (+15). E confiança Baixa **nunca** dispara push automático.
>
> **Se a banca perguntar:** se a Marina tivesse enviado sem foto, o relato dela valeria Q = 30, a média seria 50 e a conta daria 60. Com foto e descrição, Q = 85 e a conta daria 64. O número muda, a lógica é a mesma.
