# Plano de Acao - Viva Mulher

## Contexto
O projeto e um prototipo academico com publicacao atual na GitHub Pages. O objetivo deste documento e transformar os problemas encontrados em um plano prático de correcao, priorizando o que reduz mais risco e melhora mais a entrega.

## Objetivo
Organizar os problemas encontrados no projeto e definir como corrigi-los de forma pratica para um time distribuido.

## 7 etapas de correcao

### 1. Bloquear acesso aos dashboards
Problema: qualquer pessoa consegue abrir os dashboards pela URL, sem validacao de sessao.

Solucao:
- Criar validacao obrigatoria no carregamento de cada dashboard.
- Redirecionar para a pagina inicial quando nao houver sessao valida.
- Impedir acesso direto aos paineis sem autorizacao.

Resultado esperado:
- Ninguem entra no painel apenas digitando a URL.

Arquivos envolvidos:
- Projeto_Viva_Mulher/script.js
- Projeto_Viva_Mulher/dashboard-paciente/dashboard.html
- Projeto_Viva_Mulher/dashboard-medico/dashboard-medico.html
- Projeto_Viva_Mulher/dashboard-recepcao/dashboard-recepcao.html

### 2. Remover credenciais do localStorage
Problema: o cadastro e o login gravam senha, email, tipo e registro no navegador.

Solucao:
- Parar de armazenar senha em localStorage.
- Guardar apenas o minimo necessario para demonstracao local, se isso ainda for preciso.
- Planejar autenticacao real com backend quando o escopo permitir.

Resultado esperado:
- O navegador nao guarda credenciais sensiveis em texto puro.

Arquivos envolvidos:
- Projeto_Viva_Mulher/script.js
- Projeto_Viva_Mulher/dashboard-paciente/configuracoes.html

### 3. Fechar o auto-cadastro de medico
Problema: o fluxo publico permite escolher perfil de medico ou recepcao.

Solucao:
- Limitar o cadastro publico apenas ao perfil de paciente.
- Criar fluxo administrativo separado para perfis internos.
- Se a opcao continuar no mock, deixar claro que nao vale para uso real.

Resultado esperado:
- Usuario comum nao consegue se cadastrar como medico ou recepcao.

Arquivos envolvidos:
- Projeto_Viva_Mulher/index.html
- Projeto_Viva_Mulher/script.js

### 4. Sanear o agendamento contra XSS
Problema: os dados do formulario entram em innerHTML ao criar a linha da tabela.

Solucao:
- Trocar innerHTML por createElement e textContent.
- Validar e sanitizar campos antes de inserir no DOM.
- Nao concatenar entrada do usuario em HTML.

Resultado esperado:
- O formulario nao pode injetar HTML executavel na pagina.

Arquivos envolvidos:
- Projeto_Viva_Mulher/script.js
- Projeto_Viva_Mulher/dashboard-paciente/agendamentos.html

### 5. Corrigir logout e sessao
Problema: sair da conta nao limpa o estado salvo.

Solucao:
- Criar rotina de logout que remova os dados de sessao.
- Limpar usuario ativo e qualquer chave temporaria.
- Revalidar a sessao ao entrar em cada dashboard.

Resultado esperado:
- O usuario realmente sai da conta e nao fica autenticado no navegador.

Arquivos envolvidos:
- Projeto_Viva_Mulher/script.js
- Projetos de dashboard em geral

### 6. Atualizar README e validar a publicacao web
Problema: o README promete ofuscacao e um nivel de seguranca que o codigo nao entrega; alem disso, a publicacao atual da GitHub Pages precisa ser validada ou corrigida.

Solucao:
- Atualizar a documentacao para refletir o que o projeto realmente faz.
- Remover promessa de ofuscacao se ela nao existir.
- Validar a URL atual da GitHub Pages e corrigir caminhos relativos, se necessario.
- Registrar no README a URL final e o modo correto de acesso.

Resultado esperado:
- A documentacao bate com o codigo e a versao publicada abre corretamente na web.

Arquivos envolvidos:
- Projeto_Viva_Mulher/README.md
- Projeto_Viva_Mulher/manifest.json
- Projeto_Viva_Mulher/index.html

### 7. Revisar service worker e CDNs externas
Problema: o service worker usa cache-first simples e o app depende de CDNs externas sem integridade verificada.

Solucao:
- Ajustar a estrategia de cache para evitar conteudo antigo.
- Limpar cache antigo quando houver atualizacao.
- Revisar dependencias externas e, se possivel, fixar versoes ou hospedar localmente os recursos criticos.

Resultado esperado:
- O site nao fica preso em cache velho e tem menos dependencia externa fragil.

Arquivos envolvidos:
- Projeto_Viva_Mulher/sw.js
- Projeto_Viva_Mulher/index.html
- Projeto_Viva_Mulher/dashboard-paciente/dashboard.html
- Projeto_Viva_Mulher/dashboard-medico/dashboard-medico.html
- Projeto_Viva_Mulher/dashboard-recepcao/dashboard-recepcao.html

## Ordem sugerida de execucao

1. Bloquear acesso aos dashboards.
2. Remover credenciais do localStorage.
3. Fechar o auto-cadastro de medico.
4. Sanear o agendamento contra XSS.
5. Corrigir logout e limpeza de sessao.
6. Atualizar README e validar a publicacao web.
7. Revisar service worker e CDNs externas.

## Divisao sugerida para 7 desenvolvedores

- Dev 1: guarda de sessao e bloqueio de dashboards.
- Dev 2: limpeza do localStorage e fluxo de login/cadastro.
- Dev 3: restricao de cadastro publico para paciente.
- Dev 4: correcoes do agendamento e prevencao de XSS.
- Dev 5: logout, limpeza de sessao e redirecionamentos.
- Dev 6: README, documentacao, deploy e URL publica.
- Dev 7: service worker, caches e dependencias externas.

## Critérios de aceite

- Nao e possivel abrir dashboard sem sessao valida.
- Senhas nao ficam persistidas no navegador.
- Usuario comum nao consegue se cadastrar como medico ou recepcao.
- O agendamento nao injeta HTML vindo do usuario.
- O logout limpa o estado local.
- O README descreve o projeto sem exagerar seguranca ou maturidade.
- O site publicado abre em uma URL funcional e testada.
- O app nao fica preso em cache antigo apos atualizacao.

## Observacao final
Este projeto continua sendo um prototipo academico. O foco aqui e reduzir risco, alinhar a documentacao com o codigo e deixar o fluxo mais seguro para demonstracao.