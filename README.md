# Sophia_Cursos

Sistema completo de gerenciamento de cursos com autenticação robusta, construído com Next.js 15, NextAuth v5, e Sequelize. Oferece autenticação por credenciais e OAuth (Google/GitHub) com suporte a diferentes roles de usuário.

**Projeto Acadêmico** - Turma DSI10  
Curso de Análise e Desenvolvimento de Sistemas  
Instrutora: Luana

**🔗 Deploy:** [https://sophia-cursos-louis0113s-projects.vercel.app/](https://sophia-cursos-louis0113s-projects.vercel.app/)

> ⚠️ **Nota sobre o deploy:** A autenticação não está funcionando na versão implantada devido a configurações de ambiente e banco de dados. Para testar o sistema completo, execute localmente seguindo as instruções de instalação.

> ⚠️ **Nota sobre o projeto:** Este projeto está incompleto. Foi desenvolvido com dedicação e representa meu melhor esforço dentro do prazo e recursos disponíveis. Algumas funcionalidades planejadas ainda estão em desenvolvimento.

## 🚀 Tecnologias

- **Next.js 15** - Framework React com App Router
- **NextAuth v5** - Autenticação completa
- **TypeScript** - Tipagem estática
- **Sequelize** - ORM para MySQL
- **MySQL** - Banco de dados
- **Tailwind CSS** - Estilização
- **Radix UI** - Componentes acessíveis
- **React Hook Form** - Gerenciamento de formulários
- **Zod** - Validação de schemas
- **bcryptjs** - Hash de senhas

## 📋 Funcionalidades

### Autenticação

- ✅ Login com credenciais (email/senha)
- ✅ Login social (Google e GitHub)
- ✅ Registro de novos usuários
- ✅ Seleção de role (Aluno/Instrutor)
- ✅ Proteção de rotas
- ✅ Sessões JWT

### Sistema de Roles

- **Aluno** - Acesso a cursos e conteúdos
- **Instrutor** - Criação e gerenciamento de cursos
- **Admin** - Acesso completo ao sistema

### Estrutura de Dados

- **Cursos** - Gerenciamento de cursos
- **Módulos** - Organização de conteúdo
- **Vídeos** - Upload e armazenamento
- **Arquivos** - Material complementar
- **Testes** - Avaliações com questões e alternativas
- **Comentários** - Interação entre usuários

## 🛠️ Instalação

### Pré-requisitos

- Node.js 18+
- MySQL 8+
- npm ou yarn

### Passos

1. **Clone o repositório**

```bash
git clone https://github.com/seu-usuario/SOphia_Cursos.git
cd SOphia_Cursos
```

2. **Instale as dependências**

```bash
npm install
```

3. **Configure as variáveis de ambiente**

Crie um arquivo `.env.local` na raiz do projeto:

```env
# Database
DATABASE_USER=seu_usuario
DATABASE_PASS=sua_senha
DATABASE_NAME=sophia_cursos
NODE_ENV=development

# NextAuth
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=sua_chave_secreta_aqui

# OAuth Google
AUTH_GOOGLE_ID=seu_google_client_id
AUTH_GOOGLE_SECRET=seu_google_client_secret

# OAuth GitHub
AUTH_GITHUB_ID=seu_github_client_id
AUTH_GITHUB_SECRET=seu_github_client_secret
```

4. **Configure o banco de dados**

Crie o banco de dados MySQL:

```sql
CREATE DATABASE sophia_cursos;
```

5. **Execute as migrations**

```bash
npx sequelize-cli db:migrate
```

6. **Inicie o servidor de desenvolvimento**

```bash
npm run dev
```

Acesse [http://localhost:3000](http://localhost:3000)

## 📁 Estrutura do Projeto

```
src/
├── app/
│   ├── (auth)/              # Rotas de autenticação
│   │   ├── login/
│   │   ├── register/
│   │   ├── role/
│   │   └── error/
│   ├── api/
│   │   ├── auth/            # Endpoints NextAuth
│   │   └── user-info/       # Informações do usuário
│   └── lib/
│       ├── actions/         # Server actions
│       └── data/            # Queries do banco
├── components/
│   ├── auth/                # Componentes de autenticação
│   └── ui/                  # Componentes reutilizáveis
├── models/                  # Modelos Sequelize
├── migrations/              # Migrations do banco
├── schemas/                 # Schemas Zod
├── types/                   # Definições TypeScript
└── styles/                  # Estilos globais
```

## 🔐 Configuração OAuth

### Google OAuth

1. Acesse o [Google Cloud Console](https://console.cloud.google.com/)
2. Crie um novo projeto
3. Ative a API Google+
4. Configure a tela de consentimento OAuth
5. Crie credenciais OAuth 2.0
6. Adicione as URLs de redirecionamento:
   - `http://localhost:3000/api/auth/callback/google`

### GitHub OAuth

1. Acesse [GitHub Developer Settings](https://github.com/settings/developers)
2. Crie um novo OAuth App
3. Configure as URLs:
   - Homepage URL: `http://localhost:3000`
   - Authorization callback URL: `http://localhost:3000/api/auth/callback/github`

## 🗃️ Schema do Banco de Dados

### Users

- id (UUID)
- name
- email (único)
- password (hash)
- role (aluno, instrutor, admin)
- emailVerified
- image

### Courses

- id
- name
- desc
- modules (JSON)

### Modules

- id
- name
- desc
- archives (JSON)
- videos (JSON)

### Videos

- id
- name
- desc
- video (BLOB)

### Archives

- id
- name
- desc
- archive (BLOB)

### Tests

- id
- name
- desc
- questions (JSON)
- alternatives (JSON)

### Comments

- id
- name
- message

## 🚦 Rotas

### Públicas

- `/` - Landing page

### Autenticação

- `/login` - Página de login
- `/register` - Página de registro
- `/role` - Seleção de role
- `/error` - Página de erro

### Protegidas

- `/api/user-info` - Informações do usuário logado

## 🔒 Middleware de Proteção

O sistema utiliza middleware para proteger rotas baseado em:

- Status de autenticação
- Role do usuário
- Verificação de email

## 🎨 Componentes UI

O projeto utiliza uma biblioteca customizada de componentes baseada em Radix UI:

- Button
- Card
- Input
- Select
- Field (formulários)
- Label
- Separator

## 📝 Validação de Formulários

Todos os formulários são validados usando Zod schemas:

- **LoginSchema** - Validação de login
- **RegisterSchema** - Validação de registro
- **SelectRole** - Validação de seleção de role

## 🤝 Contribuindo

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

## 📄 Licença

Este projeto está sob a licença MIT.

## 👥 Autor

**Luiz Henrique Ramos de Souza**  
Turma DSI10 - Análise e Desenvolvimento de Sistemas  
Instrutora: Luana

---

**Agradecimentos:** Agradeço à professora Luana pela orientação e aos colegas da turma DSI10 pelo apoio durante o desenvolvimento deste projeto.

Projeto desenvolvido como parte do curso de Análise e Desenvolvimento de Sistemas, representando o aprendizado e dedicação ao longo do semestre.

## 🐛 Status do Projeto

### ✅ Funcionalidades Implementadas

- Sistema completo de autenticação (credenciais e OAuth)
- Gerenciamento de usuários e roles
- Estrutura do banco de dados
- Interface de login e registro
- Proteção de rotas
- Componentes UI reutilizáveis

### 🚧 Funcionalidades Incompletas

- Sistema completo de gerenciamento de cursos
- Upload e reprodução de vídeos
- Sistema de testes/avaliações
- Dashboard do instrutor
- Área do aluno com progresso de cursos

> **Nota do desenvolvedor:** Este projeto representa meu melhor esforço e dedicação ao aprendizado das tecnologias envolvidas. Embora incompleto, demonstra a implementação sólida de autenticação moderna, arquitetura de banco de dados e boas práticas de desenvolvimento web.

## 📞 Suporte

Para suporte ou dúvidas sobre o projeto SOphia_Cursos, entre em contato através do GitHub ou abra uma issue no repositório.

Teste2
