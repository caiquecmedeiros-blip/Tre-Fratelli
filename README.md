Documentação do Projeto: Tre Fratelli Barbearia

1. Motivação e Relevância

Motivação

O setor de serviços de beleza e cuidados pessoais, especificamente barbearias, tem crescido exponencialmente. No entanto, muitos estabelecimentos ainda dependem de agendamentos manuais (telefone ou WhatsApp), o que gera interrupções no serviço, erros de marcação e limita o horário de atendimento ao horário comercial.

A motivação para este projeto foi criar uma solução digital para a Tre Fratelli Barbearia, eliminando a fricção no processo de agendamento.

Relevância

A solução é relevante pois:

Autonomia: Permite que o cliente agende horários 24/7, sem depender de um atendente.

Organização: Evita conflitos de horários (overbooking) através de validação em tempo real.

Modernização: Eleva a percepção de marca da barbearia, oferecendo uma interface profissional e responsiva.

Eficiência: Libera os profissionais para focarem no corte, reduzindo o tempo gasto ao telefone.

2. Arquitetura da Solução

A aplicação foi desenvolvida seguindo uma arquitetura Serverless (sem servidor próprio) e SPA (Single Page Application).

Comunicação Frontend-Backend

O Frontend comunica-se diretamente com o Backend (Supabase) através de chamadas de API assíncronas via HTTPS. Não há um servidor intermediário (como Node.js ou PHP) gerenciando as rotas; o próprio navegador cliente faz as requisições ao banco de dados.

graph LR
    A[Cliente (Navegador)] -- HTTPS / JS SDK --> B[Supabase (BaaS)]
    B --> C[(Database PostgreSQL)]
    B --> D[Auth Service]
    D -- Token JWT --> A
    C -- JSON Data --> A


Frontend: HTML5, Tailwind CSS e JavaScript (Vanilla).

Backend: Supabase (PostgreSQL + GoTrue para Autenticação).

3. Manual de Uso

Este guia orienta o cliente final sobre como interagir com o sistema.

3.1. Navegação Inicial

Ao acessar o site, o usuário encontra a página inicial com o banner da barbearia e um menu de navegação. É possível visitar as seções "Sobre", "Serviços" e "Localização" livremente.

3.2. Cadastro e Login

Para realizar um agendamento, é obrigatório ter uma conta.

Clique em "Login / Cadastro" no menu.

Se for novo, selecione a opção "Cadastre-se". Preencha e-mail e senha (mínimo 6 caracteres).

Se já tiver conta, insira suas credenciais e clique em "Entrar".

3.3. Realizar Agendamento

Após o login, o usuário é direcionado à tela de agendamento:

Passo 1: Selecione o serviço desejado (ex: Corte, Barba, Combo). O preço é exibido no card.

Passo 2: Escolha a data no calendário. Dias passados, domingos e segundas-feiras (dias de folga) são bloqueados ou avisados.

Passo 3: O sistema carrega os horários disponíveis. Horários já ocupados por outros clientes aparecem cinzas e não clicáveis. Clique num horário disponível (branco).

Confirmação: Um resumo aparecerá. Confirme os dados e clique em "Confirmar Agendamento".

3.4. Visualizar Histórico

Na mesma tela de agendamento, há uma seção lateral chamada "Seus Agendamentos". Ali, o usuário pode consultar todos os horários futuros e passados confirmados em seu nome.

4. Manual Técnico (Para Desenvolvedores)

4.1. Construção da Aplicação

A aplicação foi construída com foco na simplicidade de deployment.

Arquivo Único: Toda a lógica (HTML, CSS via CDN e JS) reside no index.html. Isso elimina a necessidade de bundlers complexos como Webpack para este escopo.

Gestão de Estado: Um objeto global state gerencia o usuário atual, a página ativa e o serviço selecionado.

Design System: Utiliza classes utilitárias do Tailwind CSS para garantir responsividade e consistência visual (Dark Mode).

4.2. Instalação e Execução

Pré-requisitos:

Conta no Supabase.

VS Code com extensão "Live Server".

Passos:

Clone o projeto ou baixe os arquivos (index.html e imagens .webp).

Configure o Banco de Dados:

Crie um projeto no Supabase.

Crie uma tabela agendamentos com as colunas: data (date), horario (text), email (text), servico (text).

Desative o "Confirm Email" nas configurações de Autenticação.

Configure as Chaves:

Abra o index.html.

Localize as constantes SUPABASE_URL e SUPABASE_KEY no início do script.

Insira as credenciais do seu projeto Supabase.

Execute:

Clique com o botão direito no index.html e selecione "Open with Live Server".

4.3. Código Principal e Bibliotecas

@supabase/supabase-js: Biblioteca oficial para interagir com o backend. Métodos principais usados:

.auth.signUp() / .signInWithPassword(): Gestão de sessão.

.from('tabela').select(): Busca dados (horários ocupados).

.from('tabela').insert(): Salva novos agendamentos.

.onAuthStateChange(): "Ouvinte" que detecta login/logout em tempo real.

Tailwind CSS (CDN): Responsável por todo o estilo visual. Configurado via script no head para customizar as cores (gold, darker).

4.4. Fluxo de Dados (Data Flow)

Fluxo de Agendamento:

sequenceDiagram
    participant User as Usuário
    participant UI as Interface (JS)
    participant DB as Supabase (DB)

    User->>UI: Seleciona Data
    UI->>DB: SELECT horario FROM agendamentos WHERE data = X
    DB-->>UI: Retorna (Ocupados)
    UI->>UI: Renderiza grade (Bloqueia 10:00 e 14:00)
    User->>UI: Clica em 15:00
    UI->>User: Pede confirmação
    User->>UI: Confirma
    UI->>DB: INSERT INTO agendamentos (data, 15:00, user_email, servico)
    DB-->>UI: Sucesso (201 OK)
    UI->>User: Mostra "Confirmado" e atualiza lista


5. Resultados e Conclusão

Desafios Enfrentados

O Problema do CORS (Google Sheets): Inicialmente, tentamos usar o Google Sheets como banco de dados. Enfrentamos bloqueios severos de CORS (Cross-Origin Resource Sharing) e redirecionamentos de autenticação devido ao uso de uma conta institucional (Senai).

Persistência de Dados no Frontend: Garantir que a interface limpasse os dados do usuário anterior ao fazer logout foi um desafio de lógica de estado, resolvido com a função resetBookingForm.

Aprendizados

Limitações de Ferramentas: Aprendemos que, embora o Google Sheets seja poderoso, não é um backend adequado para aplicações web públicas com autenticação.

Vantagens do BaaS: A migração para o Supabase demonstrou como um Backend-as-a-Service simplifica drasticamente a autenticação e a manipulação de dados, eliminando a necessidade de gerenciar infraestrutura.

Segurança: A importância de tratar senhas e dados de usuários através de serviços dedicados em vez de planilhas.

Melhorias Futuras

Painel Administrativo: Criar uma área restrita para os barbeiros visualizarem a agenda completa e cancelarem horários.

Integração com Pagamento: Cobrar um sinal ou o valor total via Stripe ou PIX no momento do agendamento.

Notificações: Enviar e-mail ou WhatsApp automático lembrando o cliente do horário (usando Edge Functions do Supabase).
