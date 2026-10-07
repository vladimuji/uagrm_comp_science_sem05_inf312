# Implementación del diseño físico en SQL Server

El diseño físico lleva a SQL Server la estructura definida para el sistema de gestión de fletes y mudanzas **Los Camioncitos**. En esta etapa se especifican las tablas, los tipos de datos, las claves y las relaciones que permiten almacenar la información y mantener su integridad.

La implementación se encuentra en el script [`logistics_mssql.sql`](../assets/db/logistics_mssql.sql).

## Creación de la base de datos y las tablas

El script crea la base de datos `logistics` y, a continuación, la selecciona con `USE` para ejecutar en ella las instrucciones de definición del esquema. Las instrucciones `GO` separan lotes para que SQL Server procese en el orden requerido la creación y configuración de los objetos.

El modelo organiza la información en tablas relacionadas por claves primarias y foráneas:

- **Usuarios y perfiles:** `users` guarda los datos generales; `customer`, `staff`, `driver` y `car_owner` representan los distintos perfiles asociados al usuario. Los identificadores de perfil también son claves foráneas a `users`.
- **Vehículos:** `car` registra placa, marca, modelo, color y capacidad, y se relaciona con conductores y propietarios.
- **Servicios y pagos:** `cargo_service` registra los detalles del flete, sus ubicaciones, fecha, precio, estado, cliente y conductor. `service_status` mantiene el catálogo de estados. `payment_receipt` almacena los comprobantes y se relaciona con `payment_method`, `cargo_service` y `customer`.
- **Datos de contacto:** `users_mobiles` y `users_addresses` permiten asociar varios teléfonos y domicilios a un usuario. Cada tabla emplea una clave primaria compuesta por el usuario y el dato correspondiente.
- **Información geográfica y rutas:** `nodes` contiene ciudades, departamento, coordenadas y un indicador de disponibilidad. `edges` representa rutas entre ciudades con distancia, costos, duración, estado de la vía y datos de rutas de Google en formato JSON.
- **Auditoría:** `audit_log` define una estructura para registrar operaciones y cambios. Su creación está protegida con `IF OBJECT_ID`, de modo que no se intenta crear nuevamente si ya existe.

Se emplean tipos propios de SQL Server de acuerdo con los datos, como `INT`, `VARCHAR`, `FLOAT`, `BIT`, `DATETIME`, `TIME`, `NVARCHAR(MAX)` y `DATETIME2`. Las claves primarias identifican los registros; las restricciones `UNIQUE` evitan duplicar ciertos valores, como el correo o el CI; y las claves foráneas expresan las dependencias entre entidades. También se especifican acciones `CASCADE` y `NO ACTION` para definir cómo se comportan las relaciones ante actualizaciones o eliminaciones.

## Inserción de datos

Después de crear las tablas, el script carga datos geográficos de referencia:

- Inserta **120 ciudades o localidades** en `nodes`, incluyendo su nombre, departamento, latitud, longitud y si están listadas como disponibles.
- Inserta rutas en `edges` con origen y destino, kilómetros, costos estimados, duración y la respuesta de rutas de Google serializada como JSON. La clave primaria compuesta por `origin_node` y `destination_node` identifica cada recorrido dirigido.

Los comentarios del script indican que los registros geográficos fueron generados a partir de `nodes.json` y `edges.json` (con rutas consolidadas desde `edges_merged.json`). Para las inserciones de rutas se usa `SET NOCOUNT ON` y cada registro se ejecuta en un lote separado mediante `GO`.

Esta carga inicial prepara catálogos geográficos para consultas y operaciones posteriores. En este archivo, las inserciones de datos se concentran en `nodes` y `edges`; aunque también se crean las tablas de usuarios, perfiles, vehículos, servicios y pagos, el script no incluye datos de ejemplo para esas tablas.

## Ejecución

Se puede ejecutar el archivo completo desde SQL Server Management Studio o una herramienta compatible con scripts de SQL Server, usando una cuenta con permisos para crear bases de datos y tablas. Una vez finalizada la ejecución, la base `logistics` contiene el esquema físico y los datos geográficos incluidos en el script.