# Plano de Implementacao - Botao de Panico Comunitario (Viva Mulher)

## Contexto
Este documento organiza as tarefas para adicionar ao projeto uma funcionalidade de botao de panico voltada para mulheres em situacao de violencia domestica, com acionamento via WhatsApp e operacao durante acao comunitaria em local fisico.

## Objetivo
Criar um fluxo seguro, rapido e auditavel para pedido de ajuda, com:
- LGPD (base legal, consentimento, retencao e seguranca)
- Cadastro minimo para uso do botao
- Botao dinamico (estado em tempo real)
- Tempo de resposta monitorado (SLA)
- Compartilhamento de localizacao da usuaria
- Fluxo operacional claro para equipe de resposta

## Escopo funcional (MVP)
1. Cadastro da usuaria (dados minimos e consentimentos).
2. Acionamento do botao de panico no app web.
3. Redirecionamento seguro para WhatsApp com mensagem estruturada.
4. Coleta de localizacao (quando permitido pela usuaria).
5. Registro local/servidor do evento de emergencia (id, horario, status).
6. Painel de acompanhamento do chamado (recebido, em atendimento, concluido).
7. Medicao de tempo de resposta da equipe.

## Requisitos de negocio
- O botao deve ficar visivel em area de facil acesso.
- O acionamento deve exigir no maximo 2 toques apos login.
- Em caso de falha no WhatsApp, deve haver plano B (ligacao 190 / contato local).
- O fluxo deve deixar claro que nao substitui emergencia policial.
- O processo deve funcionar em celular com internet instavel (mensagem curta e objetiva).

## Arquitetura sugerida (alto nivel)
- Frontend (site atual):
  - Novo modulo de emergencia em script.js ou arquivo dedicado.
  - Estado do botao (ativo, enviando, confirmado, erro).
- Integracao de comunicacao:
  - Fase 1: link wa.me com texto preformatado.
  - Fase 2: WhatsApp Business API (confirmacao automatica e trilha de status).
- Persistencia:
  - Fase 1: armazenamento local com sincronizacao basica.
  - Fase 2: backend para trilha de auditoria, SLA e relatorios.

## Fluxo de acionamento (WhatsApp)
1. Usuaria toca em "Preciso de ajuda agora".
2. Sistema coleta:
   - nome (ou alias)
   - horario
   - localizacao (se permitido)
   - codigo unico do evento
3. Sistema monta mensagem:
   - "ALERTA VIVA MULHER"
   - identificacao minima
   - link de localizacao
   - nivel de risco (baixo/medio/alto)
4. Sistema abre WhatsApp com mensagem pronta para numero da equipe.
5. Painel interno marca chamado como "disparado" e inicia cronometro de resposta.

## Mensagem padrao (exemplo)
ALERTA VIVA MULHER
ID: EVT-20260813-00123
Nome: [NOME OU ALIAS]
Horario: [DD/MM/AAAA HH:MM]
Risco: [BAIXO|MEDIO|ALTO]
Localizacao: [LINK MAPS OU COORDENADAS]
Observacao: Preciso de apoio imediato.

## LGPD - requisitos obrigatorios
### 1) Base legal e finalidade
- Definir finalidade explicita: protecao da vida e acolhimento em situacao de risco.
- Mapear base legal aplicavel com apoio juridico (ex.: tutela da saude/protecao da vida, consentimento quando cabivel).

### 2) Minimizacao de dados
- Coletar apenas o necessario para atendimento.
- Evitar campos sensiveis nao essenciais no cadastro inicial.

### 3) Consentimento e transparencia
- Exibir termo simples antes do uso do botao.
- Registrar aceite (data/hora/versao do termo).
- Disponibilizar politica de privacidade em linguagem clara.

### 4) Retencao e descarte
- Definir prazo de retencao para logs de emergencia.
- Implementar rotina de anonimizar ou excluir dados apos prazo.

### 5) Seguranca
- Proteger dados em transito (HTTPS) e em repouso (criptografia quando houver backend).
- Restringir acesso aos dados somente para perfis autorizados.
- Manter trilha de auditoria de acessos e alteracoes.

### 6) Direitos da titular
- Criar canal para solicitacao de acesso/correcao/exclusao, quando aplicavel.
- Documentar processo interno de resposta a solicitacoes LGPD.

## Cadastro - campos minimos recomendados
- Nome social ou alias
- Telefone principal
- Contato de confianca (opcional)
- Bairro/regiao (opcional)
- Aceite dos termos LGPD
- Preferencia de contato em emergencia (WhatsApp/ligacao)

## Botao dinamico - estados e comportamento
Estados:
- Pronto para acionar
- Confirmando envio
- Acionado com sucesso
- Falha no envio

Comportamentos:
- Mudanca visual forte de estado (cor/texto/icone).
- Evitar toque acidental com confirmacao rapida (ex.: segurar por 2 segundos).
- Feedback imediato com vibracao (se suportado) e mensagem na tela.
- Exibir alternativa em caso de erro (repetir envio, ligar para numero local, 190).

## Tempo de resposta (SLA)
Metricas minimas:
- T1: tempo de disparo ate leitura da equipe
- T2: tempo de disparo ate primeiro contato com usuaria
- T3: tempo de disparo ate encerramento

Metas iniciais sugeridas para piloto:
- T1 <= 2 minutos
- T2 <= 5 minutos
- T3 <= 30 minutos (casos de baixo risco)

Painel:
- Lista de chamados abertos por prioridade.
- Cronometro por chamado.
- Alertas visuais para SLA estourando.

## Compartilhamento de localizacao
- Solicitar permissao de geolocalizacao de forma clara.
- Se permitido, anexar coordenadas e link de mapa na mensagem WhatsApp.
- Se negado, oferecer preenchimento rapido manual de referencia de local.
- Reforcar no texto que localizacao aumenta a chance de resposta rapida.

## Backlog de implementacao (tarefas)

### Fase 1 - Planejamento e governanca (Pessoa 1)
- [ ] Definir responsavel juridico/LGPD do projeto.
- [ ] Validar numero oficial de atendimento no WhatsApp.
- [ ] Definir protocolo de triagem (baixo, medio, alto risco).
- [ ] Definir equipe de plantao na acao comunitaria.
- [ ] Escrever termo de uso e politica de privacidade.

### Fase 2 - UX/UI e frontend (Pessoa 2)
- [ ] Criar componente visual do botao de panico na area da paciente.
- [ ] Implementar estados dinamicos do botao.
- [ ] Criar modal de confirmacao de acionamento (toque protegido).
- [ ] Criar tela de cadastro simplificado com aceite LGPD.
- [ ] Criar mensagens de erro e fallback (190, telefone local, posto presencial).

### Fase 3 - Integracao WhatsApp (Pessoa 3)
- [ ] Implementar geracao de mensagem padrao com id de evento.
- [ ] Implementar redirecionamento para wa.me com texto codificado.
- [ ] Registrar status inicial do chamado (disparado).
- [ ] Testar abertura no Android, iOS e WhatsApp Web.
- [ ] Criar procedimento para quando WhatsApp nao estiver instalado.

### Fase 4 - Localizacao (Pessoa 4)
- [ ] Integrar geolocalizacao via navegador.
- [ ] Tratar cenarios de permissao negada/timeout.
- [ ] Incluir localizacao no texto do alerta.
- [ ] Exibir confirmacao para usuaria antes de enviar.

### Fase 5 - Monitoramento e SLA (Pessoa 5)
- [ ] Criar estrutura de log de eventos (id, horario, status, tempos).
- [ ] Implementar calculo de T1, T2, T3.
- [ ] Criar dashboard simples de chamados e tempos.
- [ ] Gerar relatorio diario do piloto comunitario.

### Fase 6 - Seguranca e LGPD tecnica (Pessoa 6)
- [ ] Revisar dados salvos em localStorage e remover dados sensiveis.
- [ ] Implementar expiracao de sessao e logout seguro.
- [ ] Restringir acesso a painel de atendimento por perfil.
- [ ] Preparar politica de retencao e descarte de dados.
- [ ] Registrar versao de termo aceita por cada usuaria.

### Fase 7 - Operacao em campo (acao comunitaria) (Pessoa 7)
- [ ] Treinar equipe para protocolo de atendimento.
- [ ] Definir script de resposta inicial no WhatsApp.
- [ ] Definir ponto focal presencial no evento.
- [ ] Simular 5 cenarios reais antes de abrir ao publico.
- [ ] Criar plano de contingencia (queda de internet/energia).

## Divisao direta por 7 pessoas
1. Pessoa 1: Planejamento, governanca e alinhamento juridico/LGPD.
2. Pessoa 2: Experiencia da usuaria e implementacao visual do botao.
3. Pessoa 3: Fluxo de acionamento e integracao com WhatsApp.
4. Pessoa 4: Captura, tratamento e envio da localizacao.
5. Pessoa 5: Logs, indicadores e monitoramento de tempo de resposta (SLA).
6. Pessoa 6: Seguranca da aplicacao e conformidade tecnica LGPD.
7. Pessoa 7: Operacao presencial, treinamento e contingencia do evento.

## Cenarios de teste obrigatorios
- [ ] Acionamento com internet boa.
- [ ] Acionamento com internet lenta.
- [ ] Usuaria sem permissao de localizacao.
- [ ] WhatsApp indisponivel no aparelho.
- [ ] Acionamento acidental e cancelamento rapido.
- [ ] Chamados simultaneos (stress test basico).

## Criterios de aceite
- Botao aciona WhatsApp com mensagem completa em ate 3 segundos.
- Localizacao aparece no alerta quando permissao e concedida.
- Sistema registra id do evento e horario de disparo.
- Equipe consegue acompanhar status e tempo de resposta.
- Termo LGPD e exibido e aceite fica registrado.
- Fluxo de fallback funciona quando WhatsApp falha.

## Ideias extras para adicionar ao projeto
1. Palavra-codigo discreta: mensagem aparentemente neutra que sinaliza risco.
2. Botao camuflado: atalho discreto dentro de outra tela para reduzir exposicao.
3. Contato de confianca automatico: opcao de notificar pessoa indicada pela usuaria.
4. Check-in de seguranca: app pergunta periodicamente se esta tudo bem.
5. Mapa de pontos de apoio: delegacia da mulher, CRAS, UBS, abrigo e defensoria proximos.
6. Modo offline de emergencia: salvar evento e disparar assim que voltar internet.
7. Escalonamento automatico: sem resposta em X minutos, notificar segundo canal.
8. Relatorio anonimizado de impacto: total de acionamentos, tempo medio, taxa de resposta.
9. Biblioteca de orientacoes rapidas: direitos, como preservar provas, para onde ir.
10. Integracao com audio curto: gravar mensagem de voz opcional para contexto rapido.

## Riscos e mitigacoes
- Risco: uso indevido do botao.
  Mitigacao: trilha de auditoria, validacao de sessao, educacao de uso.
- Risco: falsa sensacao de seguranca.
  Mitigacao: aviso explicito de que nao substitui emergencia policial.
- Risco: vazamento de dados sensiveis.
  Mitigacao: minimizacao de dados, controle de acesso, retencao curta.
- Risco: indisponibilidade de internet no local.
  Mitigacao: plano de contingencia com atendimento presencial e telefone.

## Cronograma sugerido (piloto de 4 semanas)
- Semana 1: requisitos, LGPD, UX e protocolo operacional.
- Semana 2: implementacao frontend + WhatsApp + localizacao.
- Semana 3: painel SLA, logs e testes de campo.
- Semana 4: simulacoes, ajustes finais e treinamento da equipe.

## Donos por frente (sugestao)
- Produto/UX: definir fluxo, linguagem e usabilidade.
- Engenharia frontend: botao, estados, cadastro, geolocalizacao.
- Integracao/Backend: logs, status, SLA e auditoria.
- Operacao social: protocolo de acolhimento e resposta.
- Juridico/LGPD: termos, base legal, governanca e retencao.

## Observacao final
Este modulo deve ser implementado com foco em seguranca real da usuaria, simplicidade de uso e responsabilidade juridica. A tecnologia ajuda, mas o resultado depende do protocolo humano de resposta, treinamento e monitoramento continuo.