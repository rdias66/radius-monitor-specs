# Especificação Técnica
## Monitoramento Radius

**Versão:** 0.1  
**Data:** 21/10/2025

---

## 1. VISÃO GERAL

Sistema de monitoramento integrado à plataforma SGP para detectção de  anomalias de conectividade em tempo real com notificações automaticas via canal do [Telegram ↗](https://web.telegram.org/) 

---

## 2. IMPLANTAÇÃO

### 2.1 Integração SGP

**Autenticação via API:**
- **Documentação e guia do próprio SGP:** https://bookstack.sgp.net.br/books/api/page/autenticacoes-via-api#bkmrk-02-%7C-token-e-app
- **Tópico:**  Token e App
- **Requisitos:** Token de integração SGP válido e credencial(Nome) da Aplicação autorizada

---

## 3. ESPECIFICAÇÕES TÉCNICAS

### 3.1 Tipos de Notificação e precisão de detecção

**1. Alerta de Alto Volume de Desconexões**
- Disparado quando desconexões excedem limite configurado, indica aumento anormal na taxa de desconexões
- Precisão de entrega de notificação de 1 a 20 segundos
![Notificação de alto volume](https://github.com/rdias66/radius-monitor-template/blob/main/specs/assets/high_volume.png?raw=true)


**2. Queda Regional Detectada**
- Notificação crítica de perda simultânea de conectividade em região específica
- Prioridade alta, requer ação imediata
- Precisão de entrega de notificação de 1 a 130 segundos
![Notificação de queda regional](https://github.com/rdias66/radius-monitor-template/blob/main/specs/assets/outage_detection.png?raw=true)


**3. Queda Regional Resolvida**
- Confirmação de restauração da conectividade
- Permite fechamento do incidente
- Precisão de entrega de notificação de 1 a 130 segundos
![Notificação de resolução queda regional](https://github.com/rdias66/radius-monitor-template/blob/main/specs/assets/outage_resolution.png?raw=true)


### 3.2 Parâmetros Configuráveis

| Parâmetro | Descrição | Padrão |
|-----------|-----------|--------|
| `limite_minimo_alto_volume` | Mínimo de desconexões para alerta de alto volume | 35 |
| `limite_minimo_queda_regional` | Mínimo de desconexões para queda regional | 10 |
| `porcentagem_minima_resolucao` | Percentual mínimo para considerar uma queda resolvida | 60% |

---

## 4. CALIBRAÇÃO

Os valores ideais dos parâmetros serão ajustados através de testes progressivos:

1. Implementação de valores iniciais
2. Monitoramento de falsos positivos/negativos
3. Refinamento iterativo dos limiares

O agrupamento de conexões é feito através do cadastro do cliente:

1. Inicialmente agrupados via campo "Bairro" 
2. Triagem feita a partir da analise de latitude e longitude

> É essencial que os dados de localizações dos clientes e contratos estejam cadastrados no SGP

---

## 6. REQUISITOS

- **Token e App:** Cadastrados no SGP, exemplo: radius-monitor e 09068f87-b159-474d-bfca-14d396d98d58
- **URL SGP:** URL padrão do SGP do provedor, exemplo: https://franetpg.sgp.tsmx.com.br

---

## 7. PRÓXIMOS PASSOS

1. Integração com API SGP
2. Implementação do monitoramento
3. Fase de testes e calibração
4. Implantação em produção

---

**Versão** | **Data** | **Descrição**
0.1 | 21/10/2025 | Protótipo para testes