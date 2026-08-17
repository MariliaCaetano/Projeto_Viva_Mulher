# Viva Mulher - Sistema Integrado de Saúde Feminina 🌸

Bem-vindo ao repositório do projeto **Viva Mulher**, um protótipo de plataforma digital inovadora desenvolvida para modernizar e unificar o atendimento à saúde feminina no município de Saquarema.

## 🎯 Objetivo do Projeto

O alvo do projeto é demonstrar que a rede Viva Mulher tem potencial para atender a toda a saúde de Saquarema, englobando hospitais, clínicas, postos de saúde da família e demais unidades de atendimento, promovendo:
- **Menos filas**
- **Mais prevenção**
- **Mais cuidado focado na mulher**

## ✨ Principais Funcionalidades

- **Design Premium e Responsivo**: Interface web moderna construída do zero, com uma abordagem imersiva (vídeo em plano de fundo com transição suave em degradê) inspirada em grandes empresas de tecnologia.
- **Página de Clínicas Dedicada**: Catálogo de unidades de atendimento (Hospital Municipal, Clínica da Mulher, Postos ESF) integradas diretamente à API do Google Maps para facilitar a localização das pacientes.
- **Agendamento Inteligente**: Sistema de simulação de login, cadastro e marcação de consultas intuitivo para reduzir gargalos de espera.
- **Dashboard da Paciente**: Um painel exclusivo onde a usuária pode visualizar suas próximas consultas (com alerta de antecedência) e histórico médico.
- **Apresentação Institucional**: Seção sobre a proposta de valor, estatísticas de infraestrutura (leitos, ambulâncias) e membros do projeto.

## 💻 Tecnologias Utilizadas

Este projeto foi construído com foco em fluidez, organização e demonstração das funcionalidades:
- **HTML5 & CSS3 Vanilla**: Código limpo, componentizado em CSS flexbox e grid, sem frameworks pesados, garantindo carregamento instantâneo.
- **JavaScript (ES6)**: Controle de fluxo entre views (Single Page Application - SPA simulado), animações e lógicas de interação de interface.
- **Google Maps Embed API**: Integração com mapas reais para visualização das unidades médicas.

## 🚀 Como Executar

Por ser um projeto web "client-side", a execução é extremamente simples:
1. Faça o clone ou o download deste repositório.
2. Abra a pasta do projeto.
3. Dê um duplo clique no arquivo `index.html` para abri-lo no seu navegador padrão (recomendamos Google Chrome, Edge ou Firefox).
4. Navegue através dos menus "INÍCIO", "AGENDAMENTO", "CLÍNICAS" e "LOGIN/CADASTRO" para experimentar o fluxo do usuário.

## 🌐 Publicação em URL pública

O projeto foi preparado para publicação em plataformas cloud. Como é um site estático, basta conectar o repositório ou enviar a pasta do projeto.

### 🚀 **Opção 1: Vercel (Recomendado)**

1. Acesse [vercel.com](https://vercel.com)
2. Clique em **"New Project"**
3. Conecte seu repositório GitHub
4. Vercel detectará automaticamente a configuração (`vercel.json`)
5. Clique em **"Deploy"**

A URL final ficará no formato: `https://seu-projeto.vercel.app`

**Sem Git:** Use o comando `vercel` via CLI ou faça upload manual na dashboard do Vercel.

### 📦 **Opção 2: Netlify**

1. Acesse o painel do Netlify
2. Clique em **"Add new site"** → **"Import an existing project"**
3. Conecte o repositório do GitHub ou arraste a pasta do projeto
4. Confirme que o diretório de publicação está como `.`
5. Faça o deploy

A URL final ficará no formato: `https://seu-site.netlify.app`

**Configuração em ambos os casos:**
- Diretório de publicação: `.`
- Comando de build: nenhum

Se preferir publicar sem Git, use a opção de upload manual.

## Limitações Conhecidas (Protótipo)

Este projeto é um protótipo acadêmico desenvolvido exclusivamente e para fins de demonstração.

- A aplicação funciona 100% no lado do cliente ('cliente-side').
- Não existe backend, servidor de autenticação ou banco de dados real.
- Algumas informações são armazenadas localmente no navegador apenas para simular o funcionamento do sistema.
- Os mecanismos de login, sessão e controle de acesso não oferecem segurança adequada para uso em produção.
- Não devem ser inseridos dados pessoais, credenciais reais ou informações sensíveis de saúde.
- O projeto não substitui um sistema profissional em conformidade com a LGPD.

---
*Este é um projeto acadêmico/protótipo de apresentação.*
