# TalentHub Executive · Adriana Olivos

Sistema web para gestionar procesos de selección y headhunting. Tiene tableros de procesos y candidatos, expedientes con documentos, finanzas, métricas (Time-to-Hire), usuarios con permisos, un formulario para postulantes y una vista de seguimiento para el cliente.

## Archivos

| Archivo | Para qué sirve |
|---|---|
| `index.html` | El sistema completo. Es lo que se publica en GitHub Pages. |
| `supabase_setup.sql` | Crea la base de datos en Supabase. Se ejecuta **una sola vez**. |
| `README.md` | Esta guía. |

## Paso 0 · Probarlo ya (modo demo)

Haz doble clic en `index.html`. Se abre en **modo demo**: los datos se guardan solo en ese navegador y la barra amarilla te deja probar cada rol (Administradora, Editor, Solo lectura). Sirve para conocer el sistema antes de instalarlo.

## Paso 1 · Crear la base de datos en Supabase (gratis, unos 10 minutos)

1. Entra a <https://supabase.com> y crea una cuenta. Conviene usar el correo de Adriana.
2. Crea un proyecto nuevo con **New project**:
   - Nombre: `talenthub`.
   - Contraseña de la base de datos: guárdala en un lugar seguro.
   - Región: **South America (São Paulo)**, que es la más cercana a Perú.
3. Cuando el proyecto esté listo, entra a **SQL Editor → New query**. Pega **todo** el contenido de `supabase_setup.sql` y presiona **Run**. Debe aparecer "Success".
4. Entra a **Project Settings → API** (o **API Keys**) y copia dos datos:
   - **Project URL**, algo como `https://abcd1234.supabase.co`.
   - La clave **publishable** o **anon public**. **Nunca** uses la clave `service_role` ni la `secret`.
5. Abre `index.html` con un editor de texto (Bloc de notas sirve). Al inicio del código, pega esos dos datos:
   ```js
   const SUPABASE_URL = 'https://abcd1234.supabase.co';
   const SUPABASE_ANON_KEY = 'pega-aquí-la-clave-publishable';
   ```
   Guarda el archivo.

## Paso 2 · Publicarlo en GitHub Pages

1. Crea una cuenta en <https://github.com>.
2. Crea un repositorio con **New repository**:
   - Nombre: `talenthub`.
   - Tipo: **Public**. GitHub Pages es gratis solo con repositorios públicos. Solo se ve el código; los datos quedan protegidos en Supabase.
3. Dentro del repositorio, usa **Add file → Upload files**, sube `index.html` y `README.md`, y presiona **Commit changes**.
4. Entra a **Settings → Pages**:
   - Source: **Deploy from a branch**.
   - Branch: `main`, carpeta `/ (root)`.
   - Presiona **Save**.
5. En 1 o 2 minutos aparecerá la dirección, por ejemplo `https://tu-usuario.github.io/talenthub/`. Esa es la página que Adriana abrirá en su computadora personal y en la del trabajo.

## Paso 3 · Conectar el inicio de sesión con la página

En Supabase, entra a **Authentication → URL Configuration**:

- **Site URL**: pega la dirección de GitHub Pages.
- **Redirect URLs**: agrega esa misma dirección.

Así funcionan los correos de confirmación y de "olvidé mi contraseña".

## Paso 4 · Primer ingreso y usuarios

1. Adriana abre la página, entra a **Crear cuenta** y confirma el correo que le llega.
2. **La primera cuenta registrada queda como Administradora automáticamente.** Por eso Adriana debe registrarse primero.
3. Para dar acceso a su jefe o a una asistente:
   - Envíale el enlace de la página. La persona crea su cuenta y queda **Pendiente**.
   - Adriana entra a **Usuarios & Config.** y le asigna un rol:
     - **Editor**: crea y mueve procesos y candidatos.
     - **Solo lectura**: ve el avance sin modificar nada. Es el rol ideal para el jefe.
   - Finanzas y Usuarios solo los ve la Administradora.
   - Para quitarle el acceso a alguien, cambia su rol a **Pendiente**.

## Uso diario: lo principal

- **Procesos B2B**: arrastra la tarjeta para cambiar de etapa. En *Editar proceso* se activan dos enlaces:
  - **Formulario de postulación**: el candidato llena su ficha y sube su CV, y entra solo a la fase 1.
  - **Vista para el cliente**: muestra el avance y la terna, sin DNI.
- **Candidatos**: arrastra entre fases. Los filtros rápidos muestran a quienes tienen checklist 4/4, CUL conforme, están listos para el informe o están sin movimiento. El botón **Contratar** registra la fecha que alimenta el Time-to-Hire. Puedes importar desde Excel o CSV.
- **Informe psicolaboral**: la calificación (Apto / Apto con observaciones / No apto) y la conclusión se eligen en la ficha. El informe se imprime o se guarda como PDF.
- **Métricas**: incluye el Time-to-Hire (desde la fecha de brief del proceso hasta la contratación), la conversión por fase, las alertas de procesos o candidatos sin movimiento y la actividad del equipo.
- **Usuarios & Config.**: renombra las fases del tablero (por ejemplo, "Fase 1" → "Entrevista por competencias") y define los días que activan las alertas.
- **Respaldo**: una vez por semana, usa **Exportar respaldo (.json)** y guárdalo en Drive o OneDrive.

## Traer los datos del HTML anterior

En la versión anterior, presiona **Exportar Base** para descargar el CSV. Luego, en el sistema nuevo, ve a **Candidatos → Importar Excel / CSV**. Las columnas se reconocen solas y los DNI duplicados se omiten.

## Bueno saber

- **Plan gratuito de Supabase**: 500 MB de datos y 1 GB de archivos, suficiente para miles de candidatos. El proyecto se pausa si pasa 7 días sin uso; se reactiva desde el panel de Supabase.
- **Archivos**: máximo 10 MB cada uno. Se guardan de forma privada y solo los usuarios con acceso pueden abrirlos.
- **Si no llegan los correos de confirmación**: el correo gratuito de Supabase tiene un límite por hora. Puedes desactivar la confirmación en **Authentication → Sign In / Providers → Email → Confirm email**. La aprobación de Adriana sigue protegiendo el acceso.
- **Protección de datos**: el formulario del postulante pide su consentimiento según la Ley N.º 29733.
- **Para actualizar el sistema**: reemplaza `index.html` en GitHub con **Upload files** y vuelve a pegar tus dos datos de Supabase.
