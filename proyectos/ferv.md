---
nombre: Ferv
tipo: portafolio
estado: activo
repo: https://github.com/Jacogz/Ferv
ciclo: 2
inicio: 2026-11-30
appetite: 6 semanas (30/11/2026 → 10/01/2027) × 10 h = ~60 h
---

# Ferv

## Por qué existe
Ferv es un recomendador de terceros espacios en Medellín: un chat tipo "amigo callejero" y un grafo personal de lugares. Es el producto en el que quiero seguir trabajando a largo plazo (meta: funcionando antes de julio de 2027). Este ciclo es la primera apuesta de varias: poner la app actual en manos de usuarios reales.
Lo que quiero aprender: llevar un producto a usuarios reales sobre AWS, con la infraestructura en Terraform y CI/CD.
Para un empleador: IA + infraestructura de punta a punta, con infraestructura como código, despliegue continuo, costos controlados y usuarios reales.

## Entregables
En portafolio, esta tabla es la fuente.

| # | Entregable | Fecha | Descripción | Estado | Enlace |
|---|---|---|---|---|---|
| 1 | Infraestructura y CI/CD | 2026-12-13 | La app actual corre en AWS, con la infraestructura en Terraform y el despliegue automático desde `main` | pendiente | |
| 2 | Piloto abierto | 2026-12-27 | Consentimiento (Ley 1581), auditoría de datos de Google, descripciones e imágenes en los lugares, y sugerencias por texto o audio | pendiente | |
| 3 | 25 usuarios + demo grabado | 2027-01-10 | 25 usuarios externos usan la app; video de 2 min de un usuario que usa el recomendador y el grafo, añade una descripción y una imagen a un lugar y envía una sugerencia | pendiente | |

Estados: pendiente · en curso · entregado · recortado

## Definición de terminado
Cada criterio debe poder verificarse con un comando, un test o una captura.

**Infraestructura (→ 13/12)**
- [ ] Toda la infraestructura de AWS (cómputo, PostgreSQL con pgvector, almacenamiento de imágenes y audios, red y permisos) está declarada en Terraform dentro del repo, con el estado remoto en S3. Verificación: después de un `terraform apply`, `terraform plan` no muestra cambios.
- [ ] Cada PR a `main` corre `pytest` y `terraform plan` en GitHub Actions, y cada merge a `main` despliega solo en AWS. Actions se autentica por OIDC, sin access keys guardadas. Verificación: enlace a un run en verde y al deploy que disparó.
- [ ] Cada PR que toca Terraform lo escribí yo en modo *Solo primero* y tiene una revisión agéntica registrada en el PR. Verificación: la lista de PRs.
- [ ] Hay una alarma de AWS Budgets, declarada en Terraform, con un tope de US$10 al mes y aviso al 80 %. Verificación: la alarma aparece en la consola.
- [ ] El costo real de AWS se mantiene en US$10 al mes o menos durante el ciclo. Verificación: Cost Explorer al 10/01.

**Piloto (→ 27/12)**
- [ ] `docs/auditoria-datos.md` lista cada campo que se guarda de un lugar, con su fuente y su licencia. Ningún nombre, dirección ni reseña de Google Places se guarda más allá de lo que permiten sus términos. Verificación: el documento y una consulta a la BD.
- [ ] El registro pide autorización explícita para tratar datos personales (Ley 1581) y enlaza una política de tratamiento publicada. El usuario puede borrar su cuenta y sus datos, incluidos sus archivos en S3. Verificación: captura del registro y un test del borrado.
- [ ] Un usuario puede añadir una descripción y una imagen a un lugar, y las dos se ven en la ficha del lugar después de un redeploy. Verificación: test, más una captura antes y después del redeploy.
- [ ] Un usuario puede enviar una sugerencia en texto o en audio desde la app. Queda guardada con su usuario y su fecha, y se puede consultar en el admin. Verificación: un test por cada tipo.

**Usuarios y cierre (→ 10/01)**
- [ ] Al menos 25 usuarios externos crearon una cuenta y pidieron al menos una recomendación. Verificación: consulta a la BD.
- [ ] El video de 2 minutos está enlazado en el README.
- [ ] El acuerdo de propiedad con Salomé y Juan José queda escrito, y el repo tiene un `LICENSE`. Verificación: el archivo, más una nota en el README.

## Fuera de alcance
- La API nueva con fronteras de fuentes de lugares y de LLM (control#8). Pasa al ciclo 3.
- La app móvil. El CI/CD la prepara, pero no se escribe código móvil en este ciclo.
- Más de un entorno: no hay staging, solo producción. Tampoco Kubernetes, multi-región, alta disponibilidad ni balanceador de carga.
- Migrar el catálogo completo a Foursquare OS Places u Overture. En este ciclo solo entra la auditoría, más lo mínimo para cumplir los términos de Google.
- Medir la retención semanal de una red atómica y el experimento de disposición a pagar (ver el estudio). Los 25 usuarios dan señales, pero no son esa medición.
- Funciones sociales, importar desde TikTok o Instagram, y monetización.

## Riesgos y huecos conocidos
- **US$10 al mes es muy poco para AWS.** Un balanceador de carga solo ya cuesta más que eso, y una RDS fuera de la capa gratuita se acerca al tope. Con ese tope, lo realista es una sola instancia pequeña (EC2 o Lightsail) con Postgres en la misma máquina, sin NAT gateway, más S3. Si el ADR de cómputo no cabe en US$10, se sube el tope o se cambia la arquitectura antes del primer `apply`, no después. El tope cubre solo AWS; Gemini se paga aparte.
- **10 h por semana es una apuesta nueva.** Venías de semanas con 1 día de actividad. Si el 13/12 la app no corre en AWS con un `terraform apply`, se recorta en este orden: primero el audio, después el `terraform plan` en CI.
- **Reclutar 25 usuarios no está planeado.** Falta saber quiénes son, por qué canal llegan y desde cuándo se empieza a invitar. Las fiestas de diciembre y enero caen justo en esa ventana. Si el 27/12 no hay al menos 10 invitaciones aceptadas, el criterio baja a lo que se haya logrado y se anota como hallazgo.
- **Usuarios reales = obligaciones reales.** La auditoría de Google y el consentimiento de la Ley 1581 son requisitos para abrir el piloto, no extras. El audio es un dato personal más sensible que el texto.
- **Las imágenes y los audios van a S3**, no al disco del servidor. Requieren su propio consentimiento y una política de acceso privada.
- **Gemini anuncia que duplica su precio el 1/01/2027** (dato de fuente única, sin verificar). Cae dentro del ciclo y afecta el costo por usuario del piloto.

## Decisiones
- Estudio de mercado (20/11/2026, local por decisión propia): `~/Documents/projects/ferv/Estudio de mercado de Ferv.md`. Resumen en control#9.
- Despliegue en AWS con infraestructura gestionada en Terraform, en lugar de Render (26/11/2026).
- La fase de la API nueva se recortó de este ciclo; el ciclo 2 es solo el piloto (26/11/2026).
- Modo por componente (control#8): Terraform va en *Solo primero* (yo escribo, el agente revisa), porque es donde más quiero aprender este ciclo. Despliegue, consentimiento y funciones del piloto van en *Delegar* o *Pareja* según la tarea.
- [Pendiente] ADR: servicio de cómputo y base de datos en AWS dentro de US$10 al mes. Se decide en la primera semana, con el costo mensual estimado.
- [Pendiente] ADR: almacenamiento de imágenes y audios en S3 (acceso, retención y borrado).

## Cierre
Se llena al archivar o entregar, mientras el contexto está fresco.
- **Estado real:**
- **Mi rol:**
- **Cómo correrlo:**
- **Qué aprendí / qué haría distinto:**
- **¿Candidato a demo?** IA+infra: sí/no · Derecho a publicar: sí/no · Demo en un ciclo: sí/no
- **Pitch (si los tres son sí):**
