# 🏥 Doutor Agenda - Sistema de Gestão de Clínicas

<div align="center">
  <h3>Sistema completo para gestão de clínicas médicas com agendamentos, autenticação segura e pagamentos integrados</h3>
  <img src="./public/doctor_agenda.png" alt="Doutor Agenda - Capa do Projeto" width="800"/>
  
  [![Next.js](https://img.shields.io/badge/Next.js-16-black?logo=next.js&logoColor=white)](https://nextjs.org/)
  [![React](https://img.shields.io/badge/React-19-blue?logo=react&logoColor=white)](https://reactjs.org/)
  [![TypeScript](https://img.shields.io/badge/TypeScript-5-blue?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
  [![Drizzle ORM](https://img.shields.io/badge/Drizzle-ORM-green?logo=drizzle&logoColor=white)](https://orm.drizzle.team/)
  [![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-blue?logo=postgresql&logoColor=white)](https://postgresql.org/)
  [![TailwindCSS](https://img.shields.io/badge/Tailwind-CSS-38B2AC?logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
</div>

---

## 📋 Sobre o Projeto

O **Doutor Agenda** é uma aplicação fullstack moderna e robusta para gestão completa de clínicas médicas. Desenvolvido com foco em produtividade, segurança e experiência do usuário, oferece uma solução completa para gerenciamento de consultas, médicos, pacientes e muito mais.

### 🎯 Principais Funcionalidades

- 🔐 **Autenticação Segura** - Login com Google OAuth e email/senha
- 💳 **Sistema de Assinatura** - Integração completa com Stripe
- 👨‍⚕️ **Gestão de Médicos** - Cadastro com horários, especialidades e valores
- 👥 **Gestão de Pacientes** - Controle completo de informações dos pacientes
- 📅 **Agendamento Inteligente** - Sistema avançado de agendamentos com validação de horários
- 📊 **Dashboard Analítico** - Estatísticas, gráficos e relatórios detalhados
- 🏢 **Multi-tenant** - Suporte a múltiplas clínicas
- 📱 **Design Responsivo** - Interface adaptada para todos os dispositivos

---

## 🚀 Tecnologias Utilizadas

### Frontend

| Tecnologia          | Versão   | Descrição                              |
| ------------------- | -------- | -------------------------------------- |
| **Next.js**         | `16.1.6` | Framework React com SSR e App Router   |
| **React**           | `19.0.0` | Biblioteca para interfaces de usuário  |
| **TypeScript**      | `5.x`    | Tipagem estática para JavaScript       |
| **TailwindCSS**     | `4.x`    | Framework CSS utilitário               |
| **Radix UI**        | `1.x`    | Componentes acessíveis e customizáveis |
| **React Hook Form** | `7.66.0` | Gerenciamento de formulários           |
| **Zod**             | `4.1.12` | Validação de esquemas TypeScript       |

### Backend & Banco de Dados

| Tecnologia           | Versão   | Descrição                       |
| -------------------- | -------- | ------------------------------- |
| **PostgreSQL**       | `Latest` | Banco de dados relacional       |
| **Drizzle ORM**      | `0.43.1` | ORM TypeScript-first            |
| **Better Auth**      | `1.2.7`  | Sistema de autenticação moderno |
| **Next Safe Action** | `7.10.8` | Actions seguras no servidor     |

### Integrações & Serviços

| Serviço          | Descrição                                 |
| ---------------- | ----------------------------------------- |
| **Stripe**       | Processamento de pagamentos e assinaturas |
| **Google OAuth** | Autenticação social                       |
| **Vercel**       | Deploy e hosting                          |

### Ferramentas de Desenvolvimento

| Ferramenta      | Descrição                        |
| --------------- | -------------------------------- |
| **ESLint**      | Linting e padronização de código |
| **Prettier**    | Formatação automática            |
| **Drizzle Kit** | Migrations e studio do banco     |

---

## 🏗️ Arquitetura do Projeto

```
src/
├── 📁 actions/           # Server Actions (operações do servidor)
│   ├── add-appointment/
│   ├── create-clinic/
│   ├── create-stripe-checkout/
│   ├── delete-appointment/
│   ├── get-available-times/
│   └── upsert-doctor/
├── 📁 app/              # App Router (páginas e rotas)
│   ├── (protected)/     # Rotas protegidas
│   │   ├── dashboard/   # Dashboard principal
│   │   ├── appointments/# Gestão de agendamentos
│   │   ├── doctors/     # Gestão de médicos
│   │   ├── patients/    # Gestão de pacientes
│   │   └── subscription/# Planos e assinaturas
│   ├── api/            # API Routes
│   │   ├── auth/       # Endpoints de autenticação
│   │   └── stripe/     # Webhooks do Stripe
│   └── authentication/ # Páginas de login/registro
├── 📁 components/       # Componentes reutilizáveis
│   └── ui/             # Componentes da UI
├── 📁 db/              # Configuração do banco
│   ├── schema.ts       # Schema do Drizzle
│   └── index.ts        # Conexão com banco
├── 📁 lib/             # Utilitários e configurações
│   ├── auth.ts         # Configuração Better Auth
│   ├── auth-client.ts  # Cliente de autenticação
│   └── utils.ts        # Funções utilitárias
└── 📁 hooks/           # React Hooks customizados
```

---

## 🗄️ Schema do Banco de Dados

### Principais Tabelas

#### 👤 **Users** (Usuários)

```sql
- id (PK)
- name, email, image
- stripeCustomerId, stripeSubscriptionId
- plan (essential | null)
- emailVerified
```

#### 🏥 **Clinics** (Clínicas)

```sql
- id (PK)
- name
- createdAt, updatedAt
```

#### 👨‍⚕️ **Doctors** (Médicos)

```sql
- id (PK)
- clinicId (FK)
- name, avatarImageUrl
- specialty
- availableFromWeekDay, availableToWeekDay
- availableFromTime, availableToTime
- appointmentPriceInCents
```

#### 👥 **Patients** (Pacientes)

```sql
- id (PK)
- clinicId (FK)
- name, email, phoneNumber
- sex (enum: male/female)
```

#### 📅 **Appointments** (Agendamentos)

```sql
- id (PK)
- date
- appointmentPriceInCents
- clinicId, patientId, doctorId (FKs)
```

---

## ⚙️ Configuração e Instalação

### Pré-requisitos

- Node.js 18+
- PostgreSQL
- Conta Stripe
- Projeto Google OAuth
- Git

### 1. Clone o repositório

```bash
git clone https://github.com/seu-usuario/doutor-agenda.git
cd doutor-agenda
```

### 2. Instale as dependências

```bash
npm install
```

### 3. Configure as variáveis de ambiente

Crie um arquivo `.env.local` na raiz do projeto:

```env
# ===== DATABASE =====
DATABASE_URL="postgresql://usuario:senha@localhost:5432/doutor_agenda"

# ===== AUTHENTICATION =====
BETTER_AUTH_SECRET="seu-secret-muito-seguro-aqui"

# ===== GOOGLE OAUTH =====
GOOGLE_CLIENT_ID="seu-google-client-id"
GOOGLE_CLIENT_SECRET="seu-google-client-secret"

# ===== STRIPE =====
STRIPE_SECRET_KEY="sk_test_..."
STRIPE_WEBHOOK_SECRET="whsec_..."
STRIPE_ESSENTIAL_PLAN_PRICE_ID="price_..."

# ===== NEXT.JS =====
NEXT_PUBLIC_APP_URL="http://localhost:3000"
```

### 4. Configure o banco de dados

```bash
# Aplicar schema ao banco
npx drizzle-kit push

# (Opcional) Visualizar banco no Drizzle Studio
npx drizzle-kit studio
```

### 5. Configure o Stripe (Desenvolvimento)

```bash
# Instalar Stripe CLI (se necessário)
# Escutar webhooks localmente
stripe listen --forward-to localhost:3000/api/stripe/webhook
```

### 6. Execute o projeto

```bash
npm run dev
```

Acesse `http://localhost:3000` 🎉

---

## 💳 Configuração do Stripe

### Cartão de Teste

Para testar pagamentos, use os seguintes dados:

```
💳 Número: 4242 4242 4242 4242
👤 Nome: Qualquer nome
📅 Data: Qualquer data no futuro
🔐 CVC: Qualquer código (ex: 123)
```

### Configuração de Produtos

1. Acesse o [Dashboard do Stripe](https://dashboard.stripe.com/)
2. Crie um produto "Plano Essential"
3. Configure preço recorrente mensal
4. Copie o `price_id` para `STRIPE_ESSENTIAL_PLAN_PRICE_ID`

---

## 🔐 Autenticação - Better Auth

O sistema utiliza **Better Auth** para autenticação moderna e segura:

### Funcionalidades Implementadas

- ✅ **Login com Google OAuth**
- ✅ **Login com Email/Senha**
- ✅ **Registro de usuários**
- ✅ **Sessões seguras**
- ✅ **Verificação de email**
- ✅ **Proteção de rotas**
- ✅ **Custom session com dados da clínica**

### Configuração Google OAuth

1. Acesse [Google Cloud Console](https://console.cloud.google.com/)
2. Crie um projeto ou selecione existente
3. Ative a API Google+
4. Configure OAuth 2.0:
   - **URIs de redirecionamento**: `http://localhost:3000/api/auth/callback/google`
   - **Origem autorizada**: `http://localhost:3000`

---

## 📊 Dashboard e Funcionalidades

### Dashboard Principal

- 📈 **Gráficos de agendamentos** por período
- 🏆 **Top médicos** por número de consultas
- 🩺 **Especialidades mais procuradas**
- 📅 **Agendamentos por status**
- 💰 **Estatísticas financeiras**

### Gestão de Médicos

- ➕ Cadastro completo com avatar
- ⏰ Configuração de horários disponíveis
- 💰 Definição de valores por consulta
- 🩺 Especialidades médicas
- 📊 Estatísticas individuais

### Gestão de Pacientes

- 📝 Cadastro com dados pessoais
- 📞 Informações de contato
- 👫 Dados demográficos
- 📋 Histórico de consultas

### Sistema de Agendamentos

- 📅 Interface de calendário intuitiva
- ⏰ Validação automática de horários
- 🚫 Prevenção de conflitos
- 📧 Notificações automáticas
- 💰 Cálculo automático de valores

---

## 🔒 Segurança

### Implementações de Segurança

- 🔐 **Autenticação JWT** com Better Auth
- 🛡️ **Proteção CSRF** automática
- 🚫 **Rate limiting** em APIs sensíveis
- 📝 **Validação rigorosa** com Zod
- 🔒 **Headers de segurança** configurados
- 🎯 **Autorização granular** por clínica

### Proteção de Dados

- 🗄️ **Conexões seguras** com banco
- 🔑 **Variáveis de ambiente** protegidas
- 🧹 **Sanitização** de inputs

---

## 🎨 UI/UX

### Design System

- 🎨 **Design consistente** com Radix UI
- ♿ **Acessibilidade** (WCAG 2.1)
- ⚡ **Animações fluidas** com Tailwind

### Componentes Principais

- 📊 **DataTable** com filtering/sorting
- 📅 **Calendar** para agendamentos
- 🎛️ **Forms** com validação em tempo real
- 📄 **Modals** e **Dialogs** acessíveis
- 🔔 **Toast notifications** com Sonner

---

## 📈 Performance

### Otimizações Implementadas

- ⚡ **App Router** do Next.js 16
- 🎯 **Server Components** por padrão
- 📦 **Bundle splitting** automático
- 🗂️ **Lazy loading** de componentes
- 🏃‍♂️ **Streaming** de dados
- 💾 **Caching** inteligente

---

## 🚀 Deploy

### Deploy na Vercel (Recomendado)

1. Acesse https://vercel.com
2. Conecte sua conta do GitHub
3. Importe o repositório do projeto
4. Configure as variáveis de ambiente
5. Clique em **Deploy**

### Variáveis de Produção

Certifique-se de configurar todas as variáveis de ambiente na Vercel:

- `DATABASE_URL` (use um banco PostgreSQL em produção)
- `BETTER_AUTH_SECRET`
- `GOOGLE_CLIENT_ID` e `GOOGLE_CLIENT_SECRET`
- `STRIPE_SECRET_KEY` e `STRIPE_WEBHOOK_SECRET`
- `NEXT_PUBLIC_APP_URL`

---

## 📝 Scripts Disponíveis

```bash
# Desenvolvimento
npm run dev              # Inicia servidor de desenvolvimento

# Produção
npm run build           # Build para produção
npm start              # Inicia servidor de produção

# Qualidade de código
npm run lint           # Executa ESLint
npx eslint --fix src   # Corrige imports automaticamente

# Banco de dados
npx drizzle-kit push   # Aplica schema ao banco
npx drizzle-kit studio # Abre Drizzle Studio

# Stripe (Desenvolvimento)
stripe listen --forward-to localhost:3000/api/stripe/webhook
```

---

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

---

## 👨‍💻 Autor

**Lucas Sarasa**

- 🌐 GitHub: [@lucasarasa](https://github.com/lucasarasa)
- 💼 LinkedIn: [Lucas Sarasa](https://www.linkedin.com/in/lucassarasa/)
- ✉️ Email: lucasmsarasa@gmail.com

---

<div align="center">
  <p>Desenvolvido com ❤️ por Lucas Sarasa</p>
  
  ⭐ Deixe uma estrela se este projeto te ajudou!
</div>
