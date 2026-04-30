# TODO.md - Progreso del proyecto "Tus Recuerdos"

Estado: 🚀 En progreso

## Plan Aprobado - Pasos Pendientes (Marca con ✅ al completar)

### Fase 1: Setup Inicial (Paso 1 de instrucciones.md)
- ✅ Ejecutar comandos PowerShell Paso 1: npx create-next-app tus-recuerdos + deps + prisma init + mkdirs
- ✅ Verificar estructura de carpetas creada

### Fase 2: Archivos Vacíos (Paso 2)
- [ ] Ejecutar comandos PowerShell Paso 2: New-Item para todos los archivos listados
- [ ] Verificar todos los archivos vacíos creados

### Fase 3: Configuración Base
- [ ] prisma/schema.prisma (schema completo)
- [ ] .env y .env.example
- [ ] prisma/seed.ts (seed admin)

### Fase 4: Librerías (src/lib/)
- [ ] src/lib/prisma.ts
- [ ] src/lib/utils.ts
- [ ] src/lib/whatsapp.ts
- [ ] src/lib/validations.ts
- [ ] src/lib/auth.ts
- [ ] src/middleware.ts
- [ ] tailwind.config.ts

### Fase 5: Server Actions (src/actions/)
- [ ] Todas las actions (.ts)

### Fase 6: Componentes UI
- [ ] src/components/ui/ (button, input, etc.)
- [ ] src/components/layout/
- [ ] src/components/ordenes/
- [ ] src/components/dashboard/
- [ ] src/components/forms/

### Fase 7: Páginas y Layouts
- [ ] src/app/(public)/ pages
- [ ] src/app/(auth)/ pages
- [ ] src/app/(admin)/ pages/layouts
- [ ] src/app/(cliente)/ pages/layouts
- [ ] src/app/layout.tsx, globals.css

### Fase 8: API Routes
- [ ] src/app/api/ todas las routes (.ts)

### Fase 9: Finalización
- [ ] npx prisma generate
- [ ] npx prisma db push
- [ ] npx prisma db seed
- [ ] npm run dev - Verificar funciona
- [ ] Login admin: admin@tusrecuerdos.co / admin123
- [ ] Test crear orden, cambiar estado, upload foto

## Notas
- Directories: cd tus-recuerdos required for some cmds.
- MySQL required for DB (localhost:3306/tus_recuerdos).
- WhatsApp simulated in console.

Última actualización: Fase 1 completada (parcial mkdirs fallaron por paréntesis, recreados manual).


### Fase 2: Archivos Vacíos (Paso 2)
- [ ] Ejecutar comandos PowerShell Paso 2: New-Item para todos los archivos listados
- [ ] Verificar todos los archivos vacíos creados

### Fase 3: Configuración Base
- [ ] prisma/schema.prisma (schema completo)
- [ ] .env y .env.example
- [ ] prisma/seed.ts (seed admin)

### Fase 4: Librerías (src/lib/)
- [ ] src/lib/prisma.ts
- [ ] src/lib/utils.ts
- [ ] src/lib/whatsapp.ts
- [ ] src/lib/validations.ts
- [ ] src/lib/auth.ts
- [ ] src/middleware.ts
- [ ] tailwind.config.ts

### Fase 5: Server Actions (src/actions/)
- [ ] Todas las actions (.ts)

### Fase 6: Componentes UI
- [ ] src/components/ui/ (button, input, etc.)
- [ ] src/components/layout/
- [ ] src/components/ordenes/
- [ ] src/components/dashboard/
- [ ] src/components/forms/

### Fase 7: Páginas y Layouts
- [ ] src/app/(public)/ pages
- [ ] src/app/(auth)/ pages
- [ ] src/app/(admin)/ pages/layouts
- [ ] src/app/(cliente)/ pages/layouts
- [ ] src/app/layout.tsx, globals.css

### Fase 8: API Routes
- [ ] src/app/api/ todas las routes (.ts)

### Fase 9: Finalización
- [ ] npx prisma generate
- [ ] npx prisma db push
- [ ] npx prisma db seed
- [ ] npm run dev - Verificar funciona
- [ ] Login admin: admin@tusrecuerdos.co / admin123
- [ ] Test crear orden, cambiar estado, upload foto

## Notas
- Directories: cd tus-recuerdos required for some cmds.
- MySQL required for DB (localhost:3306/tus_recuerdos).
- WhatsApp simulated in console.

Última actualización: Inicio del proyecto

