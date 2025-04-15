## Prompt 1
**Fecha:** 11-06-2024
**Modelo:** Claude 3.7 Sonnet

**Usuario:**
Eres un ingeniero de bases de datos, experto en postgresql y en el orm prisma.
A continuación te presento el modelo de base de datos actual @schema.prisma y una propuesta de ampliación @propuesta.md .
Analiza ambos ficheros para crear un nuevo modelo de base de datos, que esté lo más normalizado posible y que sea lo más óptimo posible.
La nueva versión del modelo debe escribirse sobre el fichero @schema.prisma 
Sugiere la creación de índices para obtener el mejor rendimiento.
Genera un fichero .sql con el código SQL resultado.
Indícame los pasos a seguir para levantar la base de datos utilizando Prisma.
Antes de hacer nada, hazme todas las preguntas que necesites para llevar a cabo la tarea.
Guarda este prompt siguiendo las instrucciones definidas en @prompts-intrucciones.md 

**Asistente:**
Necesito hacerte algunas preguntas antes de proceder con el diseño de la base de datos:

1. ¿Es necesario mantener compatibilidad con el esquema actual? Es decir, ¿los datos existentes deben migrarse al nuevo esquema?
2. ¿Existen preferencias específicas para la nomenclatura de las tablas? Veo que en el esquema actual se usan nombres en singular (Candidate, Education) mientras que en la propuesta están en mayúsculas.
3. ¿Hay alguna restricción o consideración especial sobre las relaciones entre las entidades que no esté clara en el diagrama?
4. ¿Tienes alguna preferencia específica para los tipos de índices a implementar?
5. ¿Deseas mantener la estructura actual de los modelos existentes o puedo modificarlos si encuentro oportunidades de mejora?

Mientras tanto, guardaré este prompt según las instrucciones. 

## Prompt 2
**Fecha:** 11-06-2024
**Modelo:** Claude 3.7 Sonnet

**Usuario:**
Te respondo a las preguntas:

1.- Si
2.- Utiliza el mismo formato que tiene el esquema actual
3.- No
4.- No. Crea todos los necesarios para la mayor optimización posible
5.- Propón las mejoras que consideres necesarias.

Guarda este prompt siguiendo las instrucciones definidas en @prompts-intrucciones.md 

**Asistente:**
He actualizado el esquema de la base de datos integrando los modelos propuestos en el diagrama ER. A continuación, detallo los cambios realizados y los pasos a seguir para implementarlos.

### Cambios principales:

1. He mantenido compatibilidad con los modelos existentes (Candidate, Education, WorkExperience, Resume).
2. He agregado todos los nuevos modelos: Company, Employee, InterviewFlow, InterviewType, InterviewStep, Position, Application e Interview.
3. He establecido todas las relaciones necesarias entre las entidades.
4. He agregado índices para optimizar las consultas más comunes:
   - Índices en campos de búsqueda frecuente (email, nombre, etc.)
   - Índices en claves foráneas para acelerar los joins
   - Índices compuestos para búsquedas con múltiples criterios (fechas, nombres)
   - Índices para campos utilizados frecuentemente en filtros (status, isVisible)

### Pasos para levantar la base de datos con Prisma:

1. **Configurar el archivo .env**: Asegúrate de que la variable `DATABASE_URL` esté configurada correctamente con la URL de tu base de datos PostgreSQL.

2. **Crear la primera migración**:
   ```bash
   npx prisma migrate dev --name initial
   ```

3. **Aplicar la migración a la base de datos**:
   ```bash
   npx prisma migrate deploy
   ```

4. **Generar el cliente de Prisma**:
   ```bash
   npx prisma generate
   ```

5. **Verificar la estructura de la base de datos**:
   ```bash
   npx prisma studio
   ```

Si necesitas realizar cambios adicionales al esquema, puedes repetir los pasos 2-4 para crear nuevas migraciones.

El archivo migration.sql contiene todo el código SQL necesario para crear las tablas, índices y relaciones en la base de datos PostgreSQL, asegurando un rendimiento óptimo para las consultas más comunes en este tipo de sistema. 