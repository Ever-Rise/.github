<div align="center">

<!-- HERO BADGE -->
<img src="https://img.shields.io/badge/EVERRISE-Medical%20Solutions-93E9BE?style=for-the-badge&labelColor=185FA5&color=93E9BE" alt="EVERRISE Medical Solutions" />

<br/><br/>

# EVERRISE — Medical Solutions

### Guincho Hospitalar Autônomo com IA Embarcada

**Projeto Demoday · Instituto PROA 2026 · Suzano, SP**

<br/>

[![Status](https://img.shields.io/badge/Status-Em%20Desenvolvimento-93E9BE?style=flat-square&labelColor=2C2C2A)](https://github.com/everrise-medical)
[![Prazo](https://img.shields.io/badge/Demoday-30%20Jun%202026-185FA5?style=flat-square&labelColor=2C2C2A)](https://github.com/everrise-medical)
[![Equipe](https://img.shields.io/badge/Equipe-8%20Membros-DBDBDB?style=flat-square&labelColor=2C2C2A&color=DBDBDB)](https://github.com/orgs/everrise-medical/people)
[![Licença](https://img.shields.io/badge/Licença-Privado-2C2C2A?style=flat-square&labelColor=2C2C2A)](https://github.com/everrise-medical)

<br/>

---

</div>

## 🏥 Sobre o Projeto

O **EVERRISE** é um sistema de transferência hospitalar autônomo com Inteligência Artificial embarcada, desenvolvido como projeto de conclusão do programa **Demoday do Instituto PROA 2026**.

O produto combina um guincho hospitalar adaptado com uma plataforma web de controle remoto, três módulos de IA em tempo real e hardware embarcado (Raspberry Pi + ESP32), com foco em segurança do paciente, acessibilidade e uso em ambientes clínicos e domiciliares.

> **"Tecnologia que devolve movimento, autonomia e dignidade."**

---

## 🎯 O Problema

Famílias e profissionais de saúde que cuidam de pacientes com mobilidade reduzida enfrentam diariamente:

- Risco de queda e lesão durante transferências manuais
- Ausência de equipamentos acessíveis para uso domiciliar
- Falta de monitoramento inteligente durante o transporte do paciente

---

## ✅ Nossa Solução — MVP

| Funcionalidade | Descrição |
|---|---|
| 🦾 **Movimento bilateral** | Elevação e suporte dos braços do paciente com controle preciso |
| 🌐 **Controle via Web** | Plataforma web responsiva com controle remoto em tempo real |
| 🤖 **IA de Segurança** | Monitoramento de carga (FSR 402) e detecção de obstáculos (YOLOv5n) offline |
| 💬 **Chatbot Inteligente** | Suporte ao usuário com base de conhecimento do produto via Gemini Flash |
| 🔒 **Failsafe de Hardware** | Botão físico de emergência + trava mecânica + limites de peso automáticos |
| 📡 **Telemetria em tempo real** | Dashboard com bateria, conectividade, alertas e estado do guincho |

---

## 🏗️ Arquitetura do Sistema

```
┌─────────────────────────────────────────────────────────────┐
│                     CAMADA DE APRESENTAÇÃO                  │
│              React + Vite · Tailwind CSS · Vercel           │
└──────────────────────────┬──────────────────────────────────┘
                           │ HTTPS / WebSocket
┌──────────────────────────▼──────────────────────────────────┐
│                      CAMADA DE BACKEND                      │
│           Spring Boot · Java 21 · Railway (free tier)       │
│                  MySQL + Redis (Railway)                     │
└──────────────────────────┬──────────────────────────────────┘
                           │ MQTT (HiveMQ Cloud)
┌──────────────────────────▼──────────────────────────────────┐
│                    CAMADA EMBARCADA                         │
│        Raspberry Pi 4 (4GB) · UART · ESP32                  │
│   ┌─────────────────┐     ┌──────────────────────────────┐  │
│   │   IA Embarcada  │     │       Controle de Hardware   │  │
│   │ TFLite + YOLOv5 │     │  BTS7960 · PID · FSR 402     │  │
│   │   OpenCV (local)│     │  DC Motors · LED · Botões    │  │
│   └─────────────────┘     └──────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

> ⚠️ **Princípio de segurança crítico:** Os módulos de IA de segurança (monitoramento de carga e detecção de obstáculos) rodam **100% offline no Raspberry Pi**, sem dependência de nuvem — garantindo operação mesmo sem internet.

---

## 🤖 Módulos de Inteligência Artificial

### 1. Monitoramento Preditivo de Carga
- **Hardware:** Sensor FSR 402
- **Onde roda:** Raspberry Pi (TFLite — offline)
- **Função:** Detecta padrões anômalos de pressão e interrompe o movimento automaticamente
- **Latência máxima:** 500ms

### 2. Detecção de Obstáculos (Visão Computacional)
- **Hardware:** Câmera USB (640×480 mín.)
- **Modelo:** YOLOv5n (INT8 quantizado) + OpenCV
- **Onde roda:** Raspberry Pi (offline)
- **Função:** Identifica obstáculos em tempo real e para o guincho antes da colisão
- **Latência máxima:** 300ms

### 3. Chatbot Inteligente de Suporte
- **API:** Gemini Flash (Google AI)
- **Onde roda:** Backend (nuvem — requer internet)
- **Função:** Responde dúvidas sobre uso, segurança e funcionalidades do produto
- **Idioma principal:** Português brasileiro (pt-BR)

---

## 🗂️ Estrutura de Repositórios

```
everrise-medical/
├── 📦 everrise-web          → Frontend React + Vite (Vercel)
├── ⚙️  everrise-api          → Backend Spring Boot · Java 21 (Railway)
├── 🤖 everrise-embedded     → Firmware ESP32 (C++) + Scripts Raspberry Pi (Python)
├── 🧠 everrise-ai           → Modelos TFLite, scripts de treino e inferência
├── 📐 everrise-hardware      → Esquemas elétricos, modelagem 3D (Tinkercad/PETG)
└── 📚 everrise-docs         → Documentação geral, requisitos, arquitetura
```

---

## 🛠️ Stack Tecnológica

### Frontend
![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB)
![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/Tailwind-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)
![Three.js](https://img.shields.io/badge/Three.js-000000?style=flat-square&logo=three.js&logoColor=white)

### Backend
![Java](https://img.shields.io/badge/Java%2021-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)

### IoT & Embarcado
![Raspberry Pi](https://img.shields.io/badge/Raspberry%20Pi-A22846?style=flat-square&logo=raspberrypi&logoColor=white)
![ESP32](https://img.shields.io/badge/ESP32-E7352C?style=flat-square&logo=espressif&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=flat-square&logo=c%2B%2B&logoColor=white)

### IA & ML
![TensorFlow Lite](https://img.shields.io/badge/TFLite-FF6F00?style=flat-square&logo=tensorflow&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=flat-square&logo=opencv&logoColor=white)
![Google Gemini](https://img.shields.io/badge/Gemini%20Flash-4285F4?style=flat-square&logo=google&logoColor=white)

### Infraestrutura
![Vercel](https://img.shields.io/badge/Vercel-000000?style=flat-square&logo=vercel&logoColor=white)
![Railway](https://img.shields.io/badge/Railway-0B0D0E?style=flat-square&logo=railway&logoColor=white)
![HiveMQ](https://img.shields.io/badge/HiveMQ%20Cloud-MQTT-185FA5?style=flat-square&labelColor=2C2C2A)

---

## 👥 A Equipe

| Membro | Papel | Área Principal |
|---|---|---|
| **Anderson** | Product Owner · Tech Lead · Arquiteto | Full Stack · Gestão de Produto |
| **João Pedro** | Scrum Master · Full Stack | Liderança Técnica · Integração HW/SW |
| **Rafa** | Idealizadora · Validação Clínica | Requisitos de Segurança · Prototipagem |
| **Nalbert** | UI/UX Designer · Frontend | Figma · React · Identidade Visual |
| **Kaue** | Dev · Maker · Financeiro | Audiovisual · Prototipagem de Telas |
| **Duda** | Maker · Marketing | Protótipo Físico · Comunicação Visual |
| **Letícia** | Dev · Maker | Frontend · Protótipo Físico |
| **João Victor** | Dev · Maker | Documentação · Montagem Física |

---

## 🗓️ Roadmap de Sprints

```
Sprint 1  ████████████████████░░░░  Concluída
          Identidade visual · Arquitetura · Requisitos · Pitch inicial

Sprint 2  ░░░░░░░░░░░░░░░░░░░░░░░░  Em andamento
          Hardware MVP · Backend base · Frontend core · IA módulo 1

Sprint 3  ░░░░░░░░░░░░░░░░░░░░░░░░  Planejada
          Integração completa · IA módulos 2 e 3 · Testes de campo

Sprint 4  ░░░░░░░░░░░░░░░░░░░░░░░░  Planejada
          Polimento · Pitch final · Ensaios · Demoday 30/06/2026
```

---

## 🎨 Identidade Visual

| Papel | Nome | Hex |
|---|---|---|
| **Primária** — highlights, botões, logo | Aquamarine | `#93E9BE` |
| **Secundária** — headers, nav, links | Baltic Blue | `#185FA5` |
| **Escura** — texto, fundos escuros | Graphite | `#2C2C2A` |
| **Fundo claro** — background principal | Beige | `#F5F5DC` |
| **Neutro** — cards, divisórias | Alabaster Grey | `#DBDBDB` |
| ⚠️ **Emergência APENAS** | Princeton Orange | `#FF8200` |

> **Atenção:** O laranja Princeton (`#FF8200`) é reservado **exclusivamente** para elementos de emergência (ex: botão de parada de emergência). Nunca deve ser usado de forma decorativa.

**Tipografia:** `Raleway` (display, headings, nav, botões) · `Lato` (corpo do texto)

---

## 🔗 Links Úteis

| Recurso | Link |
|---|---|
| 🌐 Plataforma Web (Staging) | Em breve |
| 📋 Backlog (Trello) | Acesso interno |
| 🎨 Design System (Figma) | Acesso interno |
| 📄 Levantamento de Requisitos | [`/everrise-docs`](https://github.com/everrise-medical/everrise-docs) |
| 🗺️ Jornada do Usuário | [Excalidraw](https://excalidraw.com/#json=m3EjX1yNs4geNIzEfz3t3,2Cq7pk_bED2k69f9w3lBPg) |

---

## 📋 Como Contribuir (Interno)

1. Verifique o card no Trello antes de iniciar qualquer tarefa
2. Crie uma branch com o padrão: `feature/nome-da-tarefa` ou `fix/descricao`
3. Abra um Pull Request para `develop` — nunca direto para `main`
4. Todo PR precisa de revisão de Anderson ou João Pedro antes do merge
5. Descreva claramente o que foi feito e como testar

---

## ⚠️ Regras de Segurança do Projeto

- **Nenhuma chave de API** deve ser commitada — use variáveis de ambiente (`.env`)
- **IA de segurança offline**: os módulos de carga e obstáculos jamais devem ser refatorados para rodar em nuvem
- **Emergência sempre tem prioridade**: qualquer sinal de `EMERGENCIA` no firmware interrompe todo o movimento imediatamente, sem exceção

---

<div align="center">

<br/>

**EVERRISE — Medical Solutions**
Projeto Demoday · Instituto PROA 2026 · Suzano, SP

*Desenvolvido com dedicação por uma equipe de 8 estudantes que acreditam que tecnologia pode transformar vidas.*

<br/>

![Demoday PROA 2026](https://img.shields.io/badge/Demoday%20PROA-2026-93E9BE?style=for-the-badge&labelColor=185FA5)

</div>
