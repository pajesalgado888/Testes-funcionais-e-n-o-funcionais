Documentação de Software e Plano de Testes – PsiCompany

Este repositório contém a **Documentação Técnica** e o **Plano de Testes** unificados do projeto **PsiCompany**, desenvolvidos como parte da atividade prática da disciplina de Qualidade e Testes de Software (QTS) / Projeto Integrador do curso Técnico em Desenvolvimento de Sistemas.

---

1. Identificação do Projeto
- **Nome do Projeto:** PsiCompany (Registro de informações, vídeo chamada e chat em tempo real)
- **Curso:** Técnico em Desenvolvimento de Sistemas (3º Ano – Integrado ao Ensino Médio)
- **Versão do Plano:** `1.0`
- **Data de Entrega:** 02/09/2026

---

2. Escopo do Teste & Objetivos

### Escopo Incluído:
- **Backend & Comunicação:** Validação de rotas, serviços de sinalização WebRTC e simulação de resposta.
- **Persistência:** Estado local (state management) e integridade dos dados de teste.
- **Lógica de Negócio:** Aplicação de máscaras de entrada (CPF `000.000.000-00` e Telefone `(00) 00000-0000`), validação de e-mail e tratamento de envio.
- **Autenticação / Fluxo:** Cadastro seletivo por perfil (Paciente vs. Psicólogo) e redirecionamentos.
- **Frontend SPA:** Interface responsiva, testes de usabilidade no Dashboard, Chat e Videochamada.

### Objetivos:
1. Verificar a correção das unidades de código (métodos e funções utilitárias).
2. Validar a integração entre as camadas (`Controller` ↔ `Service` ↔ `Repository` / State).
3. Automatizar a execução de testes via **Integração Contínua (CI)** com GitHub Actions.
4. Mapear e documentar vulnerabilidades e pontos críticos da solução.

---

3. Tipos de Teste e Responsabilidades

| Tipo de Teste | Foco Principal | Ferramentas | Responsável |
| :--- | :--- | :--- | :--- |
| **Testes Unitários** | Lógica pura, máscaras, validações e utilitários | Jest / React Testing Library | Toda a equipe |
| **Testes de Integração** | Interação entre camadas e fluxo WebRTC (PeerJS) | Jest / Testing Library | Equipe (membro por fluxo) |
| **Integração Contínua (CI)** | Build automatizado e execução de testes a cada PR/push | GitHub Actions | Equipe (Configuração do repo) |

---

4. Levantamento de Requisitos

### Requisitos Funcionais (RF)
- **RF01:** Seleção de perfil ("Paciente" ou "Psicólogo").
- **RF02:** Fluxo de cadastro direcionado ao perfil escolhido.
- **RF03:** Cadastro com Nome, E-mail, Telefone e CPF.
- **RF04:** Máscara automática no CPF (`000.000.000-00`).
- **RF05:** Máscara automática no Telefone (`(00) 00000-0000`).
- **RF06:** Validação sintática de formato de e-mail.
- **RF07:** Navegação de retorno na tela de cadastro.
- **RF08:** Exibição de preferências personalizadas conforme perfil.
- **RF09:** Seleção múltipla de áreas de interesse.
- **RF10:** Transição automática ao Dashboard pós-preferências.
- **RF11:** Listagem de conexões sugeridas no Dashboard.
- **RF12:** Exibição de Nome, Foto, Especialidade/Tipo e Bio em cada card.
- **RF13:** Exibição de preferências ativas no Dashboard.
- **RF14:** Painel lateral com dados do usuário logado e nota.
- **RF15:** Inicialização de conversa via Chat a partir dos cards.
- **RF16:** Inicialização de Videochamada com conexões sugeridas.
- **RF17:** Exibição do histórico de mensagens no Chat.
- **RF18:** Envio de novas mensagens de texto.
- **RF19:** Impedimento de envio de mensagens em branco.
- **RF20:** Simulação de resposta automática da outra parte.
- **RF21:** Botão de navegação para retornar ao Dashboard.
- **RF22:** Geração de Peer ID exclusivo para chamada P2P.
- **RF23:** Início de videochamada informando o Peer ID do destinatário.
- **RF24:** Solicitador de permissão de acesso à câmera e microfone.
- **RF25:** Modal para aceitar ou recusar chamadas recebidas.
- **RF26:** Renderização de vídeo local e vídeo remoto na chamada.
- **RF27:** Botão para encerramento de chamada a qualquer momento.
- **RF28:** Fechamento e liberação das tracks de mídia ao sair do componente.

### Requisitos Não Funcionais (RNF)
- **RNF01 (Usabilidade):** Interface 100% responsiva (Mobile e Desktop).
- **RNF02 (Usabilidade):** Feedbacks visuais de estado ("Conectando...", "Online").
- **RNF03 (Compatibilidade):** Suporte aos navegadores modernos com WebRTC.
- **RNF04 (Performance):** Importação otimizada via CDN sem processo de build.
- **RNF05 (Design):** Cores tom pastel (verde) e tipografia *Quicksand*.
- **RNF06 (Confiabilidade):** Tratamento de erros de mídia sem travamento.
- **RNF07 (Segurança):** Isolamento de dados sensíveis na camada local.
- **RNF08 (Comunicação):** Arquitetura P2P via WebRTC (PeerJS).
- **RNF09 (Idioma):** Interface em Português (pt-BR).
- **RNF10 (Portabilidade):** Single-Page Application (SPA) em arquivo unificado.

---

5. Análise de Vulnerabilidades e Pontos Críticos

1. **Persistência de Dados Sensíveis no Cliente:** Como os dados (CPF, Telefone, E-mail) são mantidos em estado local, há vulnerabilidade a vazamentos em dispositivos compartilhados. *Ação recomendada:* Criptografia local e migração para backend seguro com autenticação JWT.
2. **Tratamento de Mídia & Permissões:** Recusas de permissão de câmera/microfone pelo usuário podem travar a execução se não forem capturadas por exceções. *Ação recomendada:* Implementação de retries e avisos amigáveis em tela.
3. **Limitações de Rede P2P (WebRTC):** Conexões P2P podem ser bloqueadas em redes corporativas/NAT simétrico. *Ação recomendada:* Integração de servidores STUN/TURN fallback no protocolo de sinalização.

---
*Documentação gerada e padronizada para submissão técnica.*
