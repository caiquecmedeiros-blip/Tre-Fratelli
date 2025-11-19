Tre Fratelli Barbearia - Website & Sistema de Agendamento

Um sistema completo de agendamento online e apresentação para barbearias modernas, com autenticação segura e gestão de horários em tempo real.

📋 Visão Geral

Este projeto é uma solução "Single Page Application" (SPA) desenvolvida para modernizar a experiência de agendamento da Tre Fratelli Barbearia. Ele elimina a necessidade de contacto telefónico, permitindo que os clientes escolham serviços, verifiquem disponibilidade e confirmem horários de forma autónoma e intuitiva.

Funcionalidades Principais

Autenticação Segura: Sistema de Login e Cadastro de utilizadores via Supabase.

Agendamento Inteligente:

Seleção visual de serviços com preços.

Calendário dinâmico que bloqueia dias fechados (Dom/Seg).

Grelha de horários em tempo real (evita conflitos de agenda).

Gestão de Sessão: O utilizador permanece logado mesmo após recarregar a página.

Histórico Pessoal: Área exclusiva onde o cliente vê os seus agendamentos confirmados.

Design Premium: Interface "Dark Mode" com detalhes em dourado, totalmente responsiva (Mobile-First).

🚀 Tecnologias Utilizadas (Stack)

O projeto foi construído com foco em simplicidade, desempenho e facilidade de manutenção (Serverless).

Tecnologia

Função

HTML5

Estrutura semântica e acessível.

Tailwind CSS

Estilização moderna, responsiva e utilitária (via CDN).

JavaScript (ES6+)

Lógica de frontend, roteamento (SPA) e integração com API.

Supabase

Backend-as-a-Service (BaaS) completo: Banco de Dados (PostgreSQL) e Autenticação.

📂 Estrutura do Projeto

A arquitetura é minimalista, concentrando a lógica num único ficheiro para facilitar o deploy e a edição.

/
├── index.html          # O coração do projeto (Frontend + Lógica JS)
├── barbearia.webp      # Imagens otimizadas para web
├── corte.webp
├── ...
└── README.md           # Documentação


⚙️ Configuração e Instalação

Para rodar este projeto localmente ou fazer um fork, siga os passos abaixo.

Pré-requisitos

Uma conta gratuita no Supabase.

Um editor de código (recomendado: VS Code com a extensão "Live Server").

1. Configurar o Supabase

Crie um novo projeto no Supabase.

Vá ao Table Editor e crie uma tabela chamada agendamentos.

Desative o RLS (Row Level Security) para este teste inicial.

Adicione as colunas: data (date), horario (text), email (text), servico (text).

Vá a Authentication > Providers > Email e desative a opção "Confirm Email".

2. Configurar o Código

Clone este repositório:

git clone [https://github.com/caiquecmedeiros-blip/Tre-Fratelli](https://github.com/caiquecmedeiros-blip/Tre-Fratelli)


Abra o ficheiro index.html.

Procure pelas variáveis de configuração no início do script:

const SUPABASE_URL = 'SUA_URL_DO_SUPABASE_AQUI';
const SUPABASE_KEY = 'SUA_CHAVE_ANON_AQUI';


Substitua pelos valores encontrados em Project Settings > API no seu painel do Supabase.

3. Executar

Abra o ficheiro index.html com o Live Server ou abra-o diretamente no navegador (embora o Live Server seja recomendado para evitar problemas de cache).

🎨 Galeria e Design

O design foi pensado para transmitir a elegância de uma barbearia clássica com a conveniência digital.

Paleta de Cores: Preto Profundo (#050505), Cinza Carvão (#1a1a1a) e Dourado (#D4AF37).

Tipografia: Teko para títulos impactantes e Inter para legibilidade.

🛠️ Histórico de Desenvolvimento

Este projeto evoluiu de uma tentativa inicial com Google Sheets para uma arquitetura robusta com Supabase.

V1 (Google Sheets): Enfrentou problemas complexos de CORS e redirecionamentos de autenticação.

V2 (Supabase): Migração completa para um backend real. Resolveu problemas de segurança, permitiu autenticação persistente e eliminou erros de conexão, oferecendo uma experiência muito mais rápida ao utilizador final.

📄 Licença

Este projeto é de uso livre para fins educacionais e de portefólio.

Desenvolvido com dedicação.
