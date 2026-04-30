# 🏺 TUS RECUERDOS — PROMPT MAESTRO NEXT.JS v2.0

## 🤖 ROL

Actúa como un **Arquitecto de Software Senior especializado en Next.js fullstack**.  
Tu misión es construir el sistema **"Tus Recuerdos"** paso a paso, en este orden estricto:
```
1. CARPETAS → 2. ARCHIVOS VACÍOS → 3. CÓDIGO REAL
```

> ⚠️ Nunca escribas código antes de haber creado la carpeta y el archivo.  
> ⚠️ Todos los comandos PowerShell usan `;` como separador. Nunca uses `&&`.

---

## 🎯 QUÉ HACE EL SISTEMA

| Módulo | Qué hace |
|--------|----------|
| Landing pública | Página principal con info del negocio + seguimiento de orden |
| Auth | Login, registro, roles (admin / cliente) con NextAuth |
| Dashboard Admin | Gestión completa: clientes, órdenes, fotos, bitácora |
| Dashboard Cliente | Ver mis órdenes, estados, galería de fotos |
| Órdenes | Crear, cambiar estado, historial completo |
| Bitácora | Registro automático de cada cambio de estado |
| Fotos | Subir fotos clasificadas (antes / proceso / después) |
| WhatsApp | Notificación simulada al cliente al cambiar estado |

---

## ⚙️ STACK TECNOLÓGICO

| Capa | Tecnología |
|------|------------|
| Framework | Next.js 14 App Router + TypeScript strict |
| Estilos | Tailwind CSS v3 |
| Base de datos | MySQL 8 con Prisma ORM |
| Autenticación | NextAuth.js v5 (credentials provider) |
| Contraseñas | bcryptjs |
| Formularios | React Hook Form + Zod |
| HTTP cliente | fetch nativo (Server Actions) |
| Upload fotos | Next.js API Route + fs (local storage) |
| WhatsApp | Simulación por console.log (preparado para Twilio) |

> Sin backend separado. Todo en Next.js con Server Actions y API Routes.

---

## 🗂️ ESTRUCTURA DE CARPETAS

### PASO 1 — Ejecuta estos comandos PowerShell exactamente en este orden:
```powershell
# 1. Crear proyecto Next.js
npx create-next-app@latest tus-recuerdos --typescript --tailwind --eslint --app --src-dir --import-alias "@/*" ;
cd tus-recuerdos ;

# 2. Instalar dependencias
npm install prisma @prisma/client ;
npm install next-auth@beta ;
npm install bcryptjs ;
npm install @types/bcryptjs --save-dev ;
npm install react-hook-form zod @hookform/resolvers ;
npm install lucide-react ;
npm install clsx tailwind-merge ;

# 3. Inicializar Prisma
npx prisma init --datasource-provider mysql ;

# 4. Carpetas del sistema
mkdir src\app\(public) ;
mkdir src\app\(public)\seguimiento ;
mkdir src\app\(auth) ;
mkdir src\app\(auth)\login ;
mkdir src\app\(auth)\registro ;
mkdir src\app\(admin) ;
mkdir src\app\(admin)\dashboard ;
mkdir src\app\(admin)\clientes ;
mkdir src\app\(admin)\clientes\[id] ;
mkdir src\app\(admin)\ordenes ;
mkdir src\app\(admin)\ordenes\nueva ;
mkdir src\app\(admin)\ordenes\[id] ;
mkdir src\app\(admin)\ordenes\[id]\fotos ;
mkdir src\app\(cliente) ;
mkdir src\app\(cliente)\mis-ordenes ;
mkdir src\app\(cliente)\mis-ordenes\[id] ;
mkdir src\app\api\auth\[...nextauth] ;
mkdir src\app\api\ordenes ;
mkdir src\app\api\ordenes\[id] ;
mkdir src\app\api\ordenes\[id]\estado ;
mkdir src\app\api\ordenes\[id]\fotos ;
mkdir src\app\api\clientes ;
mkdir src\app\api\clientes\[id] ;
mkdir src\app\api\upload ;
mkdir src\components\ui ;
mkdir src\components\layout ;
mkdir src\components\ordenes ;
mkdir src\components\dashboard ;
mkdir src\components\forms ;
mkdir src\lib ;
mkdir src\types ;
mkdir src\actions ;
mkdir src\hooks ;
mkdir public\fotos ;
```

---

### PASO 2 — Crear archivos vacíos en orden
```powershell
# Prisma
New-Item prisma\schema.prisma -Force ;

# Variables de entorno
New-Item .env -Force ;
New-Item .env.example -Force ;

# Tipos globales
New-Item src\types\index.ts -Force ;

# Lib utilitarios
New-Item src\lib\prisma.ts -Force ;
New-Item src\lib\auth.ts -Force ;
New-Item src\lib\utils.ts -Force ;
New-Item src\lib\whatsapp.ts -Force ;
New-Item src\lib\validations.ts -Force ;

# Server Actions
New-Item src\actions\auth.actions.ts -Force ;
New-Item src\actions\orden.actions.ts -Force ;
New-Item src\actions\cliente.actions.ts -Force ;
New-Item src\actions\foto.actions.ts -Force ;

# Hooks
New-Item src\hooks\useOrden.ts -Force ;

# Componentes UI base
New-Item src\components\ui\button.tsx -Force ;
New-Item src\components\ui\input.tsx -Force ;
New-Item src\components\ui\card.tsx -Force ;
New-Item src\components\ui\badge.tsx -Force ;
New-Item src\components\ui\modal.tsx -Force ;
New-Item src\components\ui\table.tsx -Force ;
New-Item src\components\ui\alert.tsx -Force ;

# Componentes layout
New-Item src\components\layout\Sidebar.tsx -Force ;
New-Item src\components\layout\Navbar.tsx -Force ;
New-Item src\components\layout\Footer.tsx -Force ;
New-Item src\components\layout\AdminLayout.tsx -Force ;
New-Item src\components\layout\ClienteLayout.tsx -Force ;

# Componentes de órdenes
New-Item src\components\ordenes\EstadoBadge.tsx -Force ;
New-Item src\components\ordenes\OrdenTimeline.tsx -Force ;
New-Item src\components\ordenes\FotoGaleria.tsx -Force ;
New-Item src\components\ordenes\CambiarEstadoForm.tsx -Force ;

# Componentes dashboard
New-Item src\components\dashboard\MetricCard.tsx -Force ;
New-Item src\components\dashboard\OrdenesRecientes.tsx -Force ;

# Componentes formularios
New-Item src\components\forms\NuevaOrdenForm.tsx -Force ;
New-Item src\components\forms\LoginForm.tsx -Force ;
New-Item src\components\forms\RegistroForm.tsx -Force ;
New-Item src\components\forms\SubirFotoForm.tsx -Force ;

# Páginas públicas
New-Item src\app\(public)\page.tsx -Force ;
New-Item src\app\(public)\layout.tsx -Force ;
New-Item src\app\(public)\seguimiento\page.tsx -Force ;

# Páginas auth
New-Item src\app\(auth)\layout.tsx -Force ;
New-Item src\app\(auth)\login\page.tsx -Force ;
New-Item src\app\(auth)\registro\page.tsx -Force ;

# Páginas admin
New-Item src\app\(admin)\layout.tsx -Force ;
New-Item src\app\(admin)\dashboard\page.tsx -Force ;
New-Item src\app\(admin)\clientes\page.tsx -Force ;
New-Item "src\app\(admin)\clientes\[id]\page.tsx" -Force ;
New-Item src\app\(admin)\ordenes\page.tsx -Force ;
New-Item src\app\(admin)\ordenes\nueva\page.tsx -Force ;
New-Item "src\app\(admin)\ordenes\[id]\page.tsx" -Force ;
New-Item "src\app\(admin)\ordenes\[id]\fotos\page.tsx" -Force ;

# Páginas cliente
New-Item src\app\(cliente)\layout.tsx -Force ;
New-Item src\app\(cliente)\mis-ordenes\page.tsx -Force ;
New-Item "src\app\(cliente)\mis-ordenes\[id]\page.tsx" -Force ;

# API Routes
New-Item src\app\api\auth\[...nextauth]\route.ts -Force ;
New-Item src\app\api\ordenes\route.ts -Force ;
New-Item "src\app\api\ordenes\[id]\route.ts" -Force ;
New-Item "src\app\api\ordenes\[id]\estado\route.ts" -Force ;
New-Item "src\app\api\ordenes\[id]\fotos\route.ts" -Force ;
New-Item src\app\api\clientes\route.ts -Force ;
New-Item "src\app\api\clientes\[id]\route.ts" -Force ;
New-Item src\app\api\upload\route.ts -Force ;

# Root layout y global css
New-Item src\app\layout.tsx -Force ;
New-Item src\app\globals.css -Force ;

# Middleware de protección de rutas
New-Item src\middleware.ts -Force ;
```

---

## 🗄️ BASE DE DATOS

### PASO 3 — Código de `prisma/schema.prisma`
```prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "mysql"
  url      = env("DATABASE_URL")
}

enum Rol {
  admin
  cliente
}

enum EstadoOrden {
  ingresado
  en_diagnostico
  presupuesto_enviado
  en_reparacion
  en_pintura
  en_horneado
  listo_para_retiro
  entregado
}

enum TipoFoto {
  antes
  proceso
  despues
}

model User {
  id                Int       @id @default(autoincrement())
  nombre_completo   String    @db.VarChar(100)
  email             String?   @unique @db.VarChar(100)
  telefono_whatsapp String    @db.VarChar(20)
  password          String    @db.VarChar(255)
  rol               Rol       @default(cliente)
  direccion_entrega String?   @db.Text
  activo            Boolean   @default(true)
  createdAt         DateTime  @default(now())

  ordenes           Orden[]
  bitacoras         BitacoraOrden[]

  @@index([telefono_whatsapp])
  @@index([rol])
  @@map("users")
}

model Orden {
  id                    Int          @id @default(autoincrement())
  cliente_id            Int
  descripcion_pieza     String       @db.VarChar(150)
  tipo_trabajo          String?      @db.Text
  estado                EstadoOrden  @default(ingresado)
  fecha_promesa_entrega DateTime?
  fecha_entrega_real    DateTime?
  notas_admin           String?      @db.Text
  createdAt             DateTime     @default(now())
  updatedAt             DateTime     @updatedAt

  cliente               User         @relation(fields: [cliente_id], references: [id], onDelete: Cascade)
  bitacoras             BitacoraOrden[]
  fotos                 FotoOrden[]

  @@index([estado])
  @@index([cliente_id])
  @@map("ordenes")
}

model BitacoraOrden {
  id                       Int      @id @default(autoincrement())
  orden_id                 Int
  usuario_id               Int
  estado_anterior          String?  @db.VarChar(50)
  estado_nuevo             String   @db.VarChar(50)
  mensaje_whatsapp_enviado String?  @db.Text
  createdAt                DateTime @default(now())

  orden                    Orden    @relation(fields: [orden_id], references: [id], onDelete: Cascade)
  usuario                  User     @relation(fields: [usuario_id], references: [id], onDelete: Cascade)

  @@map("bitacora_ordenes")
}

model FotoOrden {
  id          Int      @id @default(autoincrement())
  orden_id    Int
  url_foto    String   @db.VarChar(255)
  tipo_foto   TipoFoto @default(antes)
  descripcion String?  @db.VarChar(100)
  createdAt   DateTime @default(now())

  orden       Orden    @relation(fields: [orden_id], references: [id], onDelete: Cascade)

  @@index([orden_id])
  @@map("fotos_ordenes")
}
```

---

## 🌍 VARIABLES DE ENTORNO

### PASO 4 — Código de `.env` y `.env.example`
```env
# Base de datos MySQL
DATABASE_URL="mysql://root:password@localhost:3306/tus_recuerdos"

# NextAuth
NEXTAUTH_SECRET="cambia_esto_por_64_caracteres_aleatorios_seguros"
NEXTAUTH_URL="http://localhost:3000"

# WhatsApp (simulado por defecto)
WHATSAPP_ENABLED=false
TWILIO_SID=
TWILIO_TOKEN=
TWILIO_FROM=whatsapp:+14155238886

# App
NEXT_PUBLIC_APP_NAME="Tus Recuerdos"
NEXT_PUBLIC_APP_URL="http://localhost:3000"
```

---

## 📦 LIBRERÍAS UTILITARIAS

### PASO 5 — Código de los archivos en `src/lib/`

#### `src/lib/prisma.ts`
```typescript
// Singleton de Prisma para evitar múltiples conexiones en desarrollo
import { PrismaClient } from '@prisma/client'

const globalForPrisma = globalThis as unknown as { prisma: PrismaClient }

export const prisma =
  globalForPrisma.prisma ?? new PrismaClient({ log: ['query'] })

if (process.env.NODE_ENV !== 'production') globalForPrisma.prisma = prisma
```

#### `src/lib/utils.ts`
```typescript
// Utilidades globales del proyecto
import { clsx, type ClassValue } from 'clsx'
import { twMerge } from 'tailwind-merge'

// Combinar clases Tailwind sin conflictos
export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs))
}

// Etiquetas legibles para cada estado de orden
export const ESTADO_LABELS: Record<string, string> = {
  ingresado:            'Ingresado',
  en_diagnostico:       'En diagnóstico',
  presupuesto_enviado:  'Presupuesto enviado',
  en_reparacion:        'En reparación',
  en_pintura:           'En pintura',
  en_horneado:          'En horneado',
  listo_para_retiro:    'Listo para retiro',
  entregado:            'Entregado',
}

// Colores Tailwind por estado para badges
export const ESTADO_COLORS: Record<string, string> = {
  ingresado:            'bg-gray-100 text-gray-700',
  en_diagnostico:       'bg-yellow-100 text-yellow-800',
  presupuesto_enviado:  'bg-blue-100 text-blue-800',
  en_reparacion:        'bg-orange-100 text-orange-800',
  en_pintura:           'bg-purple-100 text-purple-800',
  en_horneado:          'bg-red-100 text-red-800',
  listo_para_retiro:    'bg-green-100 text-green-800',
  entregado:            'bg-teal-100 text-teal-800',
}

// Formatear fechas en español
export function formatFecha(fecha: Date | string): string {
  return new Date(fecha).toLocaleDateString('es-CO', {
    day: '2-digit', month: 'long', year: 'numeric'
  })
}
```

#### `src/lib/whatsapp.ts`
```typescript
// Servicio de WhatsApp — simulado por consola, preparado para Twilio
const MENSAJES: Record<string, string> = {
  en_diagnostico:      '🔍 Tu pieza #{id} está siendo diagnosticada.',
  presupuesto_enviado: '💰 Hemos enviado el presupuesto para tu pieza #{id}.',
  en_reparacion:       '🛠️ ¡Tu pieza #{id} está en proceso de reparación!',
  en_pintura:          '🎨 Tu pieza #{id} está en la etapa de pintura.',
  en_horneado:         '🔥 Tu pieza #{id} está siendo horneada.',
  listo_para_retiro:   '✅ ¡Tu pieza #{id} está lista para retirar!',
  entregado:           '🎉 Gracias por confiar en Tus Recuerdos. Tu pieza #{id} fue entregada.',
}

export async function enviarNotificacion(
  telefono: string,
  estado: string,
  ordenId: number
): Promise<string> {
  const mensaje = (MENSAJES[estado] ?? 'Estado actualizado.')
    .replace('#{id}', String(ordenId))

  if (process.env.WHATSAPP_ENABLED !== 'true') {
    // Modo simulación: solo imprime en consola del servidor
    console.log(`[WhatsApp SIMULADO] → ${telefono}: ${mensaje}`)
    return mensaje
  }

  // TODO: activar cuando se tengan credenciales Twilio
  // const client = twilio(process.env.TWILIO_SID, process.env.TWILIO_TOKEN)
  // await client.messages.create({ from: process.env.TWILIO_FROM, to: `whatsapp:${telefono}`, body: mensaje })

  return mensaje
}
```

#### `src/lib/validations.ts`
```typescript
// Esquemas Zod para validar formularios
import { z } from 'zod'

export const loginSchema = z.object({
  email:    z.string().email('Email inválido'),
  password: z.string().min(6, 'Mínimo 6 caracteres'),
})

export const registroSchema = z.object({
  nombre_completo:   z.string().min(3, 'Nombre muy corto'),
  email:             z.string().email('Email inválido'),
  telefono_whatsapp: z.string().min(10, 'Teléfono inválido'),
  password:          z.string().min(6, 'Mínimo 6 caracteres'),
})

export const nuevaOrdenSchema = z.object({
  cliente_id:            z.number({ required_error: 'Selecciona un cliente' }),
  descripcion_pieza:     z.string().min(5, 'Describe la pieza').max(150),
  tipo_trabajo:          z.string().optional(),
  fecha_promesa_entrega: z.string().optional(),
  notas_admin:           z.string().optional(),
})

export const cambiarEstadoSchema = z.object({
  estado:      z.string().min(1, 'Selecciona un estado'),
  notas_admin: z.string().optional(),
})

export type LoginInput    = z.infer<typeof loginSchema>
export type RegistroInput = z.infer<typeof registroSchema>
export type NuevaOrdenInput    = z.infer<typeof nuevaOrdenSchema>
export type CambiarEstadoInput = z.infer<typeof cambiarEstadoSchema>
```

---

## 🔐 AUTENTICACIÓN

### PASO 6 — Código de `src/lib/auth.ts`
```typescript
// Configuración de NextAuth con Credentials Provider
import NextAuth from 'next-auth'
import CredentialsProvider from 'next-auth/providers/credentials'
import { prisma } from '@/lib/prisma'
import bcrypt from 'bcryptjs'

export const { handlers, signIn, signOut, auth } = NextAuth({
  providers: [
    CredentialsProvider({
      name: 'credentials',
      credentials: {
        email:    { label: 'Email',      type: 'email' },
        password: { label: 'Contraseña', type: 'password' },
      },
      async authorize(credentials) {
        if (!credentials?.email || !credentials?.password) return null

        // Buscar usuario activo en la base de datos
        const user = await prisma.user.findUnique({
          where: { email: credentials.email as string }
        })

        if (!user || !user.activo) return null

        // Verificar contraseña con bcrypt
        const ok = await bcrypt.compare(credentials.password as string, user.password)
        if (!ok) return null

        return {
          id:      String(user.id),
          name:    user.nombre_completo,
          email:   user.email ?? '',
          rol:     user.rol,
          telefono: user.telefono_whatsapp,
        }
      }
    })
  ],
  callbacks: {
    // Agregar rol y id al token JWT
    async jwt({ token, user }) {
      if (user) {
        token.rol      = (user as any).rol
        token.id       = (user as any).id
        token.telefono = (user as any).telefono
      }
      return token
    },
    // Exponer rol y id en la sesión del cliente
    async session({ session, token }) {
      if (token) {
        session.user.rol      = token.rol as string
        session.user.id       = token.id as string
        session.user.telefono = token.telefono as string
      }
      return session
    },
  },
  pages: {
    signIn: '/login',
    error:  '/login',
  },
  session: { strategy: 'jwt' },
})
```

### PASO 7 — Código de `src/middleware.ts`
```typescript
// Protección de rutas según rol
import { auth } from '@/lib/auth'
import { NextResponse } from 'next/server'

export default auth((req) => {
  const { nextUrl, auth: session } = req
  const isLoggedIn = !!session?.user

  const isAdminRoute  = nextUrl.pathname.startsWith('/(admin)') ||
                        nextUrl.pathname.startsWith('/dashboard') ||
                        nextUrl.pathname.startsWith('/clientes') ||
                        nextUrl.pathname.startsWith('/ordenes')
  const isClienteRoute = nextUrl.pathname.startsWith('/mis-ordenes')
  const isAuthRoute    = nextUrl.pathname.startsWith('/login') ||
                         nextUrl.pathname.startsWith('/registro')

  // Redirigir si no está autenticado
  if ((isAdminRoute || isClienteRoute) && !isLoggedIn) {
    return NextResponse.redirect(new URL('/login', nextUrl))
  }

  // Redirigir si es cliente intentando acceder a rutas de admin
  if (isAdminRoute && session?.user?.rol !== 'admin') {
    return NextResponse.redirect(new URL('/mis-ordenes', nextUrl))
  }

  // Redirigir si ya está logueado e intenta ir al login
  if (isAuthRoute && isLoggedIn) {
    const destino = session?.user?.rol === 'admin' ? '/dashboard' : '/mis-ordenes'
    return NextResponse.redirect(new URL(destino, nextUrl))
  }

  return NextResponse.next()
})

export const config = {
  matcher: ['/((?!api|_next/static|_next/image|favicon.ico|fotos).*)'],
}
```

---

## 🔄 SERVER ACTIONS

### PASO 8 — Código de cada action:

#### `src/actions/auth.actions.ts`
```typescript
'use server'
// Acción: registrar nuevo cliente
import { prisma } from '@/lib/prisma'
import bcrypt from 'bcryptjs'
import { registroSchema, type RegistroInput } from '@/lib/validations'

export async function registrarCliente(data: RegistroInput) {
  // Validar datos con Zod
  const parsed = registroSchema.safeParse(data)
  if (!parsed.success) return { error: parsed.error.errors[0].message }

  // Verificar que el email no exista
  const existe = await prisma.user.findUnique({ where: { email: data.email } })
  if (existe) return { error: 'Este email ya está registrado' }

  // Hashear contraseña y crear usuario
  const hash = await bcrypt.hash(data.password, 12)
  await prisma.user.create({
    data: {
      nombre_completo:   data.nombre_completo,
      email:             data.email,
      telefono_whatsapp: data.telefono_whatsapp,
      password:          hash,
      rol:               'cliente',
    }
  })

  return { success: true }
}
```

#### `src/actions/orden.actions.ts`
```typescript
'use server'
// Acciones para gestión de órdenes
import { prisma } from '@/lib/prisma'
import { auth } from '@/lib/auth'
import { enviarNotificacion } from '@/lib/whatsapp'
import { revalidatePath } from 'next/cache'
import type { NuevaOrdenInput, CambiarEstadoInput } from '@/lib/validations'

// Crear nueva orden (solo admin)
export async function crearOrden(data: NuevaOrdenInput) {
  const session = await auth()
  if (session?.user?.rol !== 'admin') return { error: 'Sin permisos' }

  const orden = await prisma.orden.create({
    data: {
      cliente_id:            data.cliente_id,
      descripcion_pieza:     data.descripcion_pieza,
      tipo_trabajo:          data.tipo_trabajo,
      fecha_promesa_entrega: data.fecha_promesa_entrega
        ? new Date(data.fecha_promesa_entrega) : null,
      notas_admin: data.notas_admin,
    }
  })

  revalidatePath('/ordenes')
  return { success: true, ordenId: orden.id }
}

// Cambiar estado de una orden — dispara bitácora + WhatsApp
export async function cambiarEstado(ordenId: number, data: CambiarEstadoInput) {
  const session = await auth()
  if (session?.user?.rol !== 'admin') return { error: 'Sin permisos' }

  // Obtener orden actual con datos del cliente
  const orden = await prisma.orden.findUnique({
    where: { id: ordenId },
    include: { cliente: true }
  })
  if (!orden) return { error: 'Orden no encontrada' }

  const estadoAnterior = orden.estado

  // Actualizar estado
  await prisma.orden.update({
    where: { id: ordenId },
    data: {
      estado: data.estado as any,
      notas_admin: data.notas_admin,
      fecha_entrega_real: data.estado === 'entregado' ? new Date() : undefined,
    }
  })

  // Enviar notificación WhatsApp
  const mensaje = await enviarNotificacion(
    orden.cliente.telefono_whatsapp,
    data.estado,
    ordenId
  )

  // Registrar en bitácora automáticamente
  await prisma.bitacoraOrden.create({
    data: {
      orden_id:                ordenId,
      usuario_id:              Number(session.user.id),
      estado_anterior:         estadoAnterior,
      estado_nuevo:            data.estado,
      mensaje_whatsapp_enviado: mensaje,
    }
  })

  revalidatePath(`/ordenes/${ordenId}`)
  return { success: true }
}

// Obtener todas las órdenes (admin) o solo las propias (cliente)
export async function getOrdenes() {
  const session = await auth()
  if (!session?.user) return []

  if (session.user.rol === 'admin') {
    return prisma.orden.findMany({
      include: { cliente: { select: { nombre_completo: true, telefono_whatsapp: true } } },
      orderBy: { createdAt: 'desc' }
    })
  }

  return prisma.orden.findMany({
    where: { cliente_id: Number(session.user.id) },
    orderBy: { createdAt: 'desc' }
  })
}

// Obtener detalle de una orden con bitácora y fotos
export async function getOrdenDetalle(ordenId: number) {
  return prisma.orden.findUnique({
    where: { id: ordenId },
    include: {
      cliente:  { select: { nombre_completo: true, email: true, telefono_whatsapp: true } },
      fotos:    { orderBy: { createdAt: 'asc' } },
      bitacoras: {
        include: { usuario: { select: { nombre_completo: true } } },
        orderBy: { createdAt: 'desc' }
      }
    }
  })
}
```

---

## 🎨 COMPONENTES

### PASO 9 — Componentes UI base

#### `src/components/ordenes/EstadoBadge.tsx`
```tsx
// Badge visual para mostrar el estado de una orden
import { cn, ESTADO_LABELS, ESTADO_COLORS } from '@/lib/utils'

interface Props {
  estado: string
  className?: string
}

export function EstadoBadge({ estado, className }: Props) {
  return (
    <span className={cn(
      'inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium',
      ESTADO_COLORS[estado] ?? 'bg-gray-100 text-gray-700',
      className
    )}>
      {ESTADO_LABELS[estado] ?? estado}
    </span>
  )
}
```

#### `src/components/ordenes/OrdenTimeline.tsx`
```tsx
// Timeline vertical del historial de cambios de estado
import { formatFecha, ESTADO_LABELS } from '@/lib/utils'
import type { BitacoraOrden, User } from '@prisma/client'

type BitacoraConUsuario = BitacoraOrden & { usuario: Pick<User, 'nombre_completo'> }

interface Props {
  bitacoras: BitacoraConUsuario[]
}

export function OrdenTimeline({ bitacoras }: Props) {
  return (
    <div className="relative pl-6 border-l-2 border-terracota/30 space-y-6">
      {bitacoras.map((entry) => (
        <div key={entry.id} className="relative">
          {/* Punto en la línea */}
          <span className="absolute -left-[1.35rem] top-1 w-3 h-3 rounded-full bg-terracota" />
          <p className="text-sm font-medium text-stone-800">
            {ESTADO_LABELS[entry.estado_nuevo] ?? entry.estado_nuevo}
          </p>
          <p className="text-xs text-stone-500">
            {formatFecha(entry.createdAt)} · {entry.usuario.nombre_completo}
          </p>
          {entry.estado_anterior && (
            <p className="text-xs text-stone-400 mt-0.5">
              Antes: {ESTADO_LABELS[entry.estado_anterior] ?? entry.estado_anterior}
            </p>
          )}
        </div>
      ))}
    </div>
  )
}
```

#### `src/components/dashboard/MetricCard.tsx`
```tsx
// Card de métrica para el dashboard admin
interface Props {
  titulo: string
  valor:  number | string
  icono:  React.ReactNode
  color?: string
}

export function MetricCard({ titulo, valor, icono, color = 'bg-terracota/10' }: Props) {
  return (
    <div className="bg-white rounded-xl border border-beige-dark p-5 flex items-center gap-4 shadow-sm">
      <div className={`p-3 rounded-lg ${color}`}>
        {icono}
      </div>
      <div>
        <p className="text-sm text-stone-500">{titulo}</p>
        <p className="text-2xl font-semibold text-stone-800">{valor}</p>
      </div>
    </div>
  )
}
```

#### `src/components/layout/Sidebar.tsx`
```tsx
// Sidebar de navegación para admin y cliente
'use client'
import Link from 'next/link'
import { usePathname } from 'next/navigation'
import { signOut } from 'next-auth/react'
import { cn } from '@/lib/utils'

interface NavItem {
  href:  string
  label: string
  icon:  React.ReactNode
}

interface Props {
  rol:   'admin' | 'cliente'
  items: NavItem[]
}

export function Sidebar({ rol, items }: Props) {
  const pathname = usePathname()

  return (
    <aside className="w-64 min-h-screen bg-white border-r border-stone-100 flex flex-col">
      {/* Logo */}
      <div className="p-6 border-b border-stone-100">
        <h1 className="font-display text-xl text-terracota font-semibold">Tus Recuerdos</h1>
        <p className="text-xs text-stone-400 mt-0.5">
          {rol === 'admin' ? 'Panel Administrador' : 'Mi Portal'}
        </p>
      </div>

      {/* Navegación */}
      <nav className="flex-1 p-4 space-y-1">
        {items.map((item) => (
          <Link
            key={item.href}
            href={item.href}
            className={cn(
              'flex items-center gap-3 px-3 py-2.5 rounded-lg text-sm transition-colors',
              pathname === item.href
                ? 'bg-terracota text-white font-medium'
                : 'text-stone-600 hover:bg-stone-50'
            )}
          >
            {item.icon}
            {item.label}
          </Link>
        ))}
      </nav>

      {/* Cerrar sesión */}
      <div className="p-4 border-t border-stone-100">
        <button
          onClick={() => signOut({ callbackUrl: '/login' })}
          className="w-full text-left px-3 py-2 text-sm text-stone-500 hover:text-red-600 rounded-lg hover:bg-red-50 transition-colors"
        >
          Cerrar sesión
        </button>
      </div>
    </aside>
  )
}
```

---

## 📄 PÁGINAS

### PASO 10 — Código completo de cada página:

#### `src/app/(public)/page.tsx` — Landing pública
```tsx
// Página principal pública — presenta el negocio
import Link from 'next/link'

export default function LandingPage() {
  return (
    <main className="min-h-screen bg-[#FAFAF8] font-body">
      {/* Hero */}
      <section className="bg-[#F5ECD7] py-24 px-6 text-center">
        <h1 className="font-display text-5xl text-[#A0522D] mb-4">Tus Recuerdos</h1>
        <p className="text-stone-600 text-lg max-w-xl mx-auto mb-8">
          Restauramos piezas de cerámica y objetos con valor sentimental.
          Cada pieza tiene una historia — nosotros la continuamos.
        </p>
        <div className="flex gap-4 justify-center flex-wrap">
          <Link href="/seguimiento"
            className="bg-[#C1694F] text-white px-6 py-3 rounded-lg hover:bg-[#A0522D] transition-colors font-medium">
            Rastrear mi orden
          </Link>
          <Link href="/login"
            className="border border-[#C1694F] text-[#C1694F] px-6 py-3 rounded-lg hover:bg-[#C1694F] hover:text-white transition-colors font-medium">
            Ingresar al portal
          </Link>
        </div>
      </section>

      {/* Servicios */}
      <section className="py-16 px-6 max-w-5xl mx-auto">
        <h2 className="font-display text-3xl text-stone-800 text-center mb-12">Nuestros Servicios</h2>
        <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
          {[
            { titulo: 'Restauración',  desc: 'Reparamos grietas, fracturas y piezas faltantes con técnica artesanal.' },
            { titulo: 'Pintura',       desc: 'Recuperamos colores y acabados originales con pigmentos de alta calidad.' },
            { titulo: 'Horneado',      desc: 'Sellamos las reparaciones con hornos especializados para durabilidad.' },
          ].map((s) => (
            <div key={s.titulo} className="bg-white border border-stone-100 rounded-xl p-6 shadow-sm">
              <h3 className="font-display text-xl text-[#C1694F] mb-2">{s.titulo}</h3>
              <p className="text-stone-500 text-sm leading-relaxed">{s.desc}</p>
            </div>
          ))}
        </div>
      </section>

      {/* Footer */}
      <footer className="bg-stone-800 text-stone-400 text-center py-8 text-sm">
        © {new Date().getFullYear()} Tus Recuerdos — Pereira, Colombia
      </footer>
    </main>
  )
}
```

#### `src/app/(auth)/login/page.tsx`
```tsx
// Página de login con formulario React Hook Form + Zod
'use client'
import { useForm } from 'react-hook-form'
import { zodResolver } from '@hookform/resolvers/zod'
import { signIn } from 'next-auth/react'
import { useRouter } from 'next/navigation'
import { useState } from 'react'
import { loginSchema, type LoginInput } from '@/lib/validations'
import Link from 'next/link'

export default function LoginPage() {
  const router  = useRouter()
  const [error, setError] = useState('')
  const { register, handleSubmit, formState: { errors, isSubmitting } } = useForm<LoginInput>({
    resolver: zodResolver(loginSchema)
  })

  async function onSubmit(data: LoginInput) {
    setError('')
    const res = await signIn('credentials', { ...data, redirect: false })
    if (res?.error) { setError('Credenciales incorrectas'); return }
    // Redirigir según rol (NextAuth callback lo maneja)
    router.refresh()
    router.push('/dashboard')
  }

  return (
    <div className="min-h-screen bg-[#F5ECD7] flex items-center justify-center p-4">
      <div className="bg-white rounded-2xl shadow-sm border border-stone-100 p-8 w-full max-w-sm">
        <h1 className="font-display text-3xl text-[#A0522D] text-center mb-2">Tus Recuerdos</h1>
        <p className="text-stone-500 text-sm text-center mb-8">Ingresa a tu cuenta</p>

        {error && (
          <div className="bg-red-50 border border-red-200 text-red-700 text-sm px-4 py-3 rounded-lg mb-4">
            {error}
          </div>
        )}

        <form onSubmit={handleSubmit(onSubmit)} className="space-y-4">
          <div>
            <label className="block text-sm font-medium text-stone-700 mb-1">Email</label>
            <input {...register('email')} type="email" placeholder="tu@email.com"
              className="w-full border border-stone-200 rounded-lg px-3 py-2.5 text-sm focus:outline-none focus:ring-2 focus:ring-[#C1694F]/40" />
            {errors.email && <p className="text-red-500 text-xs mt-1">{errors.email.message}</p>}
          </div>
          <div>
            <label className="block text-sm font-medium text-stone-700 mb-1">Contraseña</label>
            <input {...register('password')} type="password" placeholder="••••••"
              className="w-full border border-stone-200 rounded-lg px-3 py-2.5 text-sm focus:outline-none focus:ring-2 focus:ring-[#C1694F]/40" />
            {errors.password && <p className="text-red-500 text-xs mt-1">{errors.password.message}</p>}
          </div>
          <button type="submit" disabled={isSubmitting}
            className="w-full bg-[#C1694F] text-white py-2.5 rounded-lg font-medium hover:bg-[#A0522D] transition-colors disabled:opacity-60">
            {isSubmitting ? 'Ingresando...' : 'Ingresar'}
          </button>
        </form>

        <p className="text-center text-sm text-stone-500 mt-6">
          ¿No tienes cuenta?{' '}
          <Link href="/registro" className="text-[#C1694F] font-medium hover:underline">Regístrate</Link>
        </p>
      </div>
    </div>
  )
}
```

#### `src/app/(admin)/dashboard/page.tsx`
```tsx
// Dashboard admin con métricas y tabla de últimas órdenes
import { prisma } from '@/lib/prisma'
import { EstadoBadge } from '@/components/ordenes/EstadoBadge'
import { MetricCard } from '@/components/dashboard/MetricCard'
import { formatFecha } from '@/lib/utils'
import Link from 'next/link'

export default async function DashboardPage() {
  // Consultas en paralelo para mejor rendimiento
  const [totalOrdenes, listasRetiro, totalClientes, ultimas] = await Promise.all([
    prisma.orden.count({ where: { NOT: { estado: 'entregado' } } }),
    prisma.orden.count({ where: { estado: 'listo_para_retiro' } }),
    prisma.user.count({ where: { rol: 'cliente', activo: true } }),
    prisma.orden.findMany({
      take: 10,
      orderBy: { createdAt: 'desc' },
      include: { cliente: { select: { nombre_completo: true } } }
    })
  ])

  return (
    <div className="space-y-8">
      <h1 className="font-display text-2xl text-stone-800">Dashboard</h1>

      {/* Métricas */}
      <div className="grid grid-cols-1 sm:grid-cols-3 gap-4">
        <MetricCard titulo="Órdenes activas"    valor={totalOrdenes}  icono={<span>📋</span>} />
        <MetricCard titulo="Listas para retiro" valor={listasRetiro}   icono={<span>✅</span>} color="bg-green-100" />
        <MetricCard titulo="Clientes"           valor={totalClientes} icono={<span>👥</span>} color="bg-blue-50" />
      </div>

      {/* Tabla de últimas órdenes */}
      <div className="bg-white rounded-xl border border-stone-100 overflow-hidden">
        <div className="px-6 py-4 border-b border-stone-100 flex justify-between items-center">
          <h2 className="font-medium text-stone-800">Últimas órdenes</h2>
          <Link href="/ordenes" className="text-sm text-[#C1694F] hover:underline">Ver todas</Link>
        </div>
        <table className="w-full text-sm">
          <thead className="bg-stone-50 text-stone-500 text-xs uppercase">
            <tr>
              {['#', 'Cliente', 'Pieza', 'Estado', 'Fecha', ''].map((h) => (
                <th key={h} className="px-6 py-3 text-left font-medium">{h}</th>
              ))}
            </tr>
          </thead>
          <tbody className="divide-y divide-stone-50">
            {ultimas.map((o) => (
              <tr key={o.id} className="hover:bg-stone-50/50 transition-colors">
                <td className="px-6 py-4 text-stone-400">#{o.id}</td>
                <td className="px-6 py-4 font-medium text-stone-800">{o.cliente.nombre_completo}</td>
                <td className="px-6 py-4 text-stone-600 max-w-[180px] truncate">{o.descripcion_pieza}</td>
                <td className="px-6 py-4"><EstadoBadge estado={o.estado} /></td>
                <td className="px-6 py-4 text-stone-400">{formatFecha(o.createdAt)}</td>
                <td className="px-6 py-4">
                  <Link href={`/ordenes/${o.id}`} className="text-[#C1694F] hover:underline text-xs">Ver</Link>
                </td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    </div>
  )
}
```

#### `src/app/(admin)/layout.tsx`
```tsx
// Layout del panel admin con sidebar
import { auth } from '@/lib/auth'
import { redirect } from 'next/navigation'
import { Sidebar } from '@/components/layout/Sidebar'
import { LayoutDashboard, Users, ClipboardList } from 'lucide-react'

const NAV_ADMIN = [
  { href: '/dashboard', label: 'Dashboard',  icon: <LayoutDashboard size={16} /> },
  { href: '/clientes',  label: 'Clientes',   icon: <Users size={16} /> },
  { href: '/ordenes',   label: 'Órdenes',    icon: <ClipboardList size={16} /> },
]

export default async function AdminLayout({ children }: { children: React.ReactNode }) {
  const session = await auth()
  if (!session || session.user?.rol !== 'admin') redirect('/login')

  return (
    <div className="flex min-h-screen bg-[#FAFAF8] font-body">
      <Sidebar rol="admin" items={NAV_ADMIN} />
      <main className="flex-1 p-8">{children}</main>
    </div>
  )
}
```

#### `src/app/(cliente)/layout.tsx`
```tsx
// Layout del portal del cliente
import { auth } from '@/lib/auth'
import { redirect } from 'next/navigation'
import { Sidebar } from '@/components/layout/Sidebar'
import { ClipboardList } from 'lucide-react'

const NAV_CLIENTE = [
  { href: '/mis-ordenes', label: 'Mis Órdenes', icon: <ClipboardList size={16} /> },
]

export default async function ClienteLayout({ children }: { children: React.ReactNode }) {
  const session = await auth()
  if (!session) redirect('/login')

  return (
    <div className="flex min-h-screen bg-[#FAFAF8] font-body">
      <Sidebar rol="cliente" items={NAV_CLIENTE} />
      <main className="flex-1 p-8">{children}</main>
    </div>
  )
}
```

#### `src/app/(admin)/ordenes/[id]/page.tsx`
```tsx
// Detalle de orden: info + timeline + galería + cambio de estado
import { getOrdenDetalle } from '@/actions/orden.actions'
import { notFound } from 'next/navigation'
import { EstadoBadge } from '@/components/ordenes/EstadoBadge'
import { OrdenTimeline } from '@/components/ordenes/OrdenTimeline'
import { CambiarEstadoForm } from '@/components/ordenes/CambiarEstadoForm'
import { formatFecha } from '@/lib/utils'

export default async function OrdenDetallePage({ params }: { params: { id: string } }) {
  const orden = await getOrdenDetalle(Number(params.id))
  if (!orden) notFound()

  // Agrupar fotos por tipo
  const fotosPorTipo = {
    antes:   orden.fotos.filter(f => f.tipo_foto === 'antes'),
    proceso: orden.fotos.filter(f => f.tipo_foto === 'proceso'),
    despues: orden.fotos.filter(f => f.tipo_foto === 'despues'),
  }

  return (
    <div className="space-y-8 max-w-4xl">
      {/* Encabezado */}
      <div className="flex items-start justify-between">
        <div>
          <h1 className="font-display text-2xl text-stone-800">Orden #{orden.id}</h1>
          <p className="text-stone-500 text-sm mt-1">{orden.descripcion_pieza}</p>
        </div>
        <EstadoBadge estado={orden.estado} />
      </div>

      <div className="grid grid-cols-1 lg:grid-cols-3 gap-8">
        {/* Info + acciones */}
        <div className="lg:col-span-2 space-y-6">
          {/* Datos de la orden */}
          <div className="bg-white rounded-xl border border-stone-100 p-6">
            <h2 className="font-medium text-stone-800 mb-4">Información</h2>
            <dl className="space-y-2 text-sm">
              <div className="flex justify-between">
                <dt className="text-stone-500">Cliente</dt>
                <dd className="font-medium">{orden.cliente.nombre_completo}</dd>
              </div>
              <div className="flex justify-between">
                <dt className="text-stone-500">Teléfono</dt>
                <dd>{orden.cliente.telefono_whatsapp}</dd>
              </div>
              <div className="flex justify-between">
                <dt className="text-stone-500">Ingreso</dt>
                <dd>{formatFecha(orden.createdAt)}</dd>
              </div>
              {orden.fecha_promesa_entrega && (
                <div className="flex justify-between">
                  <dt className="text-stone-500">Fecha promesa</dt>
                  <dd>{formatFecha(orden.fecha_promesa_entrega)}</dd>
                </div>
              )}
            </dl>
          </div>

          {/* Formulario cambio de estado */}
          <CambiarEstadoForm ordenId={orden.id} estadoActual={orden.estado} />

          {/* Galería de fotos */}
          {Object.entries(fotosPorTipo).map(([tipo, fotos]) => fotos.length > 0 && (
            <div key={tipo} className="bg-white rounded-xl border border-stone-100 p-6">
              <h2 className="font-medium text-stone-800 mb-4 capitalize">Fotos — {tipo}</h2>
              <div className="grid grid-cols-3 gap-3">
                {fotos.map(f => (
                  <img key={f.id} src={`/fotos/${f.url_foto}`} alt={f.descripcion ?? tipo}
                    className="rounded-lg object-cover aspect-square w-full border border-stone-100" />
                ))}
              </div>
            </div>
          ))}
        </div>

        {/* Timeline */}
        <div className="bg-white rounded-xl border border-stone-100 p-6 h-fit">
          <h2 className="font-medium text-stone-800 mb-6">Historial</h2>
          <OrdenTimeline bitacoras={orden.bitacoras} />
        </div>
      </div>
    </div>
  )
}
```

---

## 🎨 TAILWIND CONFIG

### PASO 11 — `tailwind.config.ts`
```typescript
import type { Config } from 'tailwindcss'

const config: Config = {
  content: ['./src/**/*.{ts,tsx}'],
  theme: {
    extend: {
      colors: {
        terracota: {
          DEFAULT: '#C1694F',
          dark:    '#A0522D',
          light:   '#F5ECD7',
        },
        beige: {
          DEFAULT: '#F5ECD7',
          dark:    '#E8D5B7',
        }
      },
      fontFamily: {
        display: ['"Playfair Display"', 'serif'],
        body:    ['"DM Sans"', 'sans-serif'],
      }
    }
  },
  plugins: [],
}

export default config
```

---

## 🚀 COMANDOS FINALES
```powershell
# Generar cliente de Prisma
npx prisma generate ;

# Crear base de datos y tablas
npx prisma db push ;

# Seed: crear usuario admin de prueba
npx prisma db seed ;

# Servidor de desarrollo
npm run dev ;
```

### Seed de admin (`prisma/seed.ts`):
```typescript
import { PrismaClient } from '@prisma/client'
import bcrypt from 'bcryptjs'

const prisma = new PrismaClient()

async function main() {
  const hash = await bcrypt.hash('admin123', 12)
  await prisma.user.upsert({
    where: { email: 'admin@tusrecuerdos.co' },
    update: {},
    create: {
      nombre_completo:   'Administrador',
      email:             'admin@tusrecuerdos.co',
      telefono_whatsapp: '3001234567',
      password:          hash,
      rol:               'admin',
    }
  })
  console.log('✅ Admin creado: admin@tusrecuerdos.co / admin123')
}

main().catch(console.error).finally(() => prisma.$disconnect())
```

---

## 📋 ENTREGA ESPERADA — EN ESTE ORDEN EXACTO
```
1.  ✅ Comandos PowerShell — crear carpetas
2.  ✅ Comandos PowerShell — crear archivos vacíos
3.  ✅ prisma/schema.prisma completo
4.  ✅ .env y .env.example
5.  ✅ src/lib/prisma.ts
6.  ✅ src/lib/utils.ts
7.  ✅ src/lib/whatsapp.ts
8.  ✅ src/lib/validations.ts
9.  ✅ src/lib/auth.ts
10. ✅ src/middleware.ts
11. ✅ src/actions/auth.actions.ts
12. ✅ src/actions/orden.actions.ts
13. ✅ src/actions/cliente.actions.ts
14. ✅ src/actions/foto.actions.ts
15. ✅ Todos los componentes UI
16. ✅ Sidebar con navegación por rol
17. ✅ Landing pública (/)
18. ✅ Login (/login) y Registro (/registro)
19. ✅ Dashboard admin con métricas
20. ✅ Páginas de clientes, órdenes y detalle
21. ✅ Dashboard cliente — mis órdenes
22. ✅ tailwind.config.ts con paleta terracota
23. ✅ prisma/seed.ts con admin de prueba
24. ✅ API Routes para upload de fotos
```

> ⚠️ **Regla absoluta**: Sin `TODO`, sin `// completar aquí`, sin pseudocódigo.  
> Todo el código debe estar **100% implementado**, comentado en español,  
> y listo para ejecutar con `npm run dev`.