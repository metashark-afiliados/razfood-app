<div align="center">
  <img src="https://raw.githubusercontent.com/metashark-afiliados/razfood-app/main/public/images/logo.png" alt="razfood Logo" width="120" />
  <h1>razfood OS</h1>
  <p><strong>El Sistema Operativo de Inteligencia para Restaurantes Modernos</strong></p>
  <p>
    <a href="https://github.com/metashark-afiliados/razfood-app/blob/main/LICENSE"><img src="https://img.shields.io/github/license/metashark-afiliados/razfood-app?style=for-the-badge&color=FF4F00" alt="Licencia"></a>
    <a href="https://vercel.com/metashark-tech/razfood-app"><img src="https://img.shields.io/github/deployments/metashark-afiliados/razfood-app/production?label=Vercel&logo=vercel&style=for-the-badge&color=F5F5F5" alt="Deploy en Vercel"></a>
    <a href="#"><img src="https://img.shields.io/badge/TypeScript-100%25-3178C6?style=for-the-badge&logo=typescript" alt="TypeScript"></a>
    <a href="#"><img src="https://img.shields.io/badge/Prisma-ORM-2D3748?style=for-the-badge&logo=prisma" alt="Prisma ORM"></a>
  </p>
</div>

---

**razfood-app** es una plataforma SaaS (Software as a Service) multi-tenant de nivel de producción, diseñada para ser el sistema operativo central de la industria gastronómica. Nuestra misión es inyectar **eficiencia radical**, **inteligencia de negocio accionable** y **control absoluto** en cada punto de la cadena de valor de un restaurante, desde la gestión de catálogos hasta las operaciones en tiempo real.

[**Ver Demo en Vivo**](https://razfood-app.vercel.app/)

## ✨ Características Principales

- **🏢 Gestión Multi-Tenant:** Arquitectura `workspace-centric` que permite a los operadores gestionar múltiples sucursales o marcas desde un único dashboard.
- **📚 Catálogo Digital Inteligente:** Creación y gestión de menús (`sites`) y productos con una UI optimista y fluida.
- **⚡ Dashboard de Operaciones en Tiempo Real:** Un tablero Kanban que se actualiza instantáneamente con nuevos pedidos a través de Supabase Realtime y WebSockets.
- **🔒 Seguridad por Diseño:** Aislamiento de datos garantizado a nivel de base de datos mediante Row Level Security (RLS) de PostgreSQL.
- **🌐 API Soberana (GraphQL First):** Una única API de GraphQL como fuente de verdad (SSoT) para toda la lógica de negocio, preparada para alimentar múltiples clientes (web, iOS, Android).
- **🛠️ Infraestructura de Datos de Élite:** Acceso a datos 100% tipo-seguro y optimizado gracias a **Prisma ORM**.

## 🛠️ Stack Tecnológico Canónico

| Capa               | Tecnología Principal                                          |
| ------------------ | ------------------------------------------------------------- |
| **Framework**      | Next.js 14 (App Router)                                       |
| **Lenguaje**       | TypeScript                                                    |
| **Base de Datos**  | Supabase (PostgreSQL, Auth, Realtime)                         |
| **Capa de Datos**  | **Prisma ORM** (Cliente Tipo-Seguro y Gestión de Migraciones) |
| **API**            | GraphQL (Apollo Server)                                       |
| **UI**             | Tailwind CSS + shadcn/ui                                      |
| **Estado Cliente** | Zustand                                                       |
| **i18n**           | next-intl                                                     |
| **Despliegue**     | Vercel                                                        |

## 🏗️ Arquitectura de Élite

El ecosistema `razfood` se rige por una filosofía de **Atomicidad Radical** y **"API como SSoT"**. Cada pieza es un aparato soberano, y la API de GraphQL es el núcleo del sistema.

```mermaid
graph TD
    subgraph "Clientes Soberanos"
        A[razfood OS (Dashboard Web)]
        B[razfood Go (App Cliente)]
        C[raztruck (App Repartidor)]
    end

    subgraph "Núcleo del Sistema Operativo"
        API[🚀 API de GraphQL Soberana]
        AUTH[🔐 Supabase Auth (JWT)]
        PRISMA[🛡️ Prisma Client]
        DB[📦 Supabase DB (Postgres + RLS)]
        RT[⚡️ Supabase Realtime]
    end

    A -- "Queries/Mutations" --> API
    B -- "Queries/Mutations" --> API
    C -- "Queries/Mutations" --> API

    API -- "Lógica de Resolvers" --> PRISMA
    PRISMA -- "Consultas Optimizadas" --> DB

    A -- "Suscripciones" --> RT
    B -- "Suscripciones" --> RT
    C -- "Suscripciones" --> RT

    DB -- "Triggers de DB" --> RT
🚀 Puesta en Marcha Local
Para levantar un entorno de desarrollo local, siga estos pasos:
Clonar el Repositorio:
code
Bash
git clone https://github.com/metashark-afiliados/razfood-app.git
cd razfood-app
Instalar Dependencias:
code
Bash
pnpm install
Configurar Supabase Local:
Asegúrese de tener la Supabase CLI instalada.
Inicie los servicios de Supabase:
code
Bash
supabase start
La terminal le proporcionará las credenciales. Preste atención a DB password, API URL y anon key.
Configurar Variables de Entorno:
Cree un archivo .env en la raíz del proyecto copiando el contenido de .env.local.example.
Rellene las variables con las credenciales del paso anterior:
code
Env
# Credenciales de Supabase (del comando 'supabase start')
NEXT_PUBLIC_SUPABASE_URL=http://127.0.0.1:54321
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...

# Cadenas de Conexión de Prisma
DIRECT_URL="postgresql://postgres:SU_DB_PASSWORD_AQUI@127.0.0.1:54322/postgres"
DATABASE_URL="postgresql://postgres:SU_DB_PASSWORD_AQUI@127.0.0.1:54322/postgres"
Aplicar Migraciones de Base de Datos:
Este comando aplicará todos los archivos .sql a su base de datos local.
code
Bash
pnpm prisma:migrate
Iniciar el Servidor de Desarrollo:
code
Bash
pnpm dev
La aplicación estará disponible en http://localhost:3000.

📜 Scripts Principales
Script	Descripción
pnpm dev	Inicia el servidor de desarrollo.
pnpm build	Compila la aplicación para producción.
pnpm type:check	Ejecuta el compilador de TypeScript para verificar tipos.
pnpm prisma:pull	Introspecta la DB y actualiza schema.prisma.
pnpm prisma:gen	Genera el cliente de Prisma tipado.
pnpm prisma:migrate	Aplica las migraciones pendientes.
pnpm prisma:studio	Abre la UI de Prisma Studio para visualizar los datos.
🗺️ Roadmap de Desarrollo

Fase 0: Cimentación y Arquitectura (DB Schema, Auth, i18n, Logging)
Fase 1: Migración de Infraestructura a Prisma
Fase 2: Completar el CRUD del Catálogo (UI Optimista, Acciones de Servidor)
Fase 3: El Flujo de Pedido del Cliente (Vista Pública, Carrito, Checkout)
Fase 4: El Dashboard de Operaciones en Tiempo Real
Fase 5: Implementación Completa de la API de GraphQL
Fase 6: Desarrollo de Aplicaciones Nativas (razfood Go, raztruck)

🤝 Contribuciones
Las contribuciones que se adhieren al Protocolo de Excelencia son bienvenidas. Por favor, abra un issue para discutir cambios significativos antes de crear un Pull Request.
📄 Licencia
Este proyecto está bajo la Licencia MIT. Ver el archivo LICENSE para más detalles.
```
