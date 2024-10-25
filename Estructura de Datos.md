<!-- docker run -d --name neo1 -p 7474:7474 -p 7687:7687 --env=NEO4J_AUTH=none neo4j -->

# Estructura de Datos
Gestión Empresarial. 
La empresa "TechSoft" desea gestionar sus empleados, proyectos y sucursales a nivel nacional. 
Se requiere un sistema para administrar las diferentes áreas de trabajo y operaciones de la empresa.

Sucursales:
    - Cada sucursal tiene una clave, nombre, dirección, ciudad y capacidad (número máximo de empleados que puede albergar).
    - Cada sucursal tiene empleados exclusivos; es decir, un empleado solo puede trabajar en una sucursal a la vez.

Sucursal: - (Nodo)
    - Clave - (Atributo)
    - Nombre - (Atributo)
    - Dirección - (Atributo)
    - Ciudad - (Atributo)
    - Capacidad (Numero maximo de empleados que puede albergar) - (Atributo)
        - Empleados exclusivos (Cada empleado solo puede trabajar en una sucursal) - (condición - Ej: Empleado Juan Perez con clave 'ABC123' no puede trabajar en dos sucursales distintas)

Empleados: 
    - Cada empleado tiene un ID único, nombre, CURP, teléfono, número de cuenta bancaria (donde se deposita el sueldo) y fecha de contratación.
    - Hay tres tipos de empleados en cada sucursal:
    - Gerentes: responsables de supervisar la operación. Se requiere saber el área que gestionan.
    - Desarrolladores: Se requiere su especialización (back-end, front-end, full-stack), su lenguaje principal y el número de proyectos activos.
    - Soporte técnico: Se requiere el tipo de soporte que brindan (infraestructura, software, hardware) y su número de contacto interno.

Empleado: (Nodo)
    - CURP - (Atributo)
    - Nombre - (Atributo)
    - Telefono - (Atributo)
    - Número de cuenta bancaria - (Atributo)
    - Fecha de contratación - (Atributo)
        - 3 tipos de empleados - (Atributo)
            - Gerentes: Area que gestiona - (Relación con proyecto)
            - Desarrolladores: Especialización (back-end, front-end, full-stack) - (Atributo)
                - lenguaje - (Atributo) 
                - proyectos activos - (Relación con proyectos)
            - Soporte Técnico: Tipo de soporte (infraestructura, software, hardware) - (Atributo)
            - número de contacto interno - (Atributo)

Proyectos:
    - Los proyectos tienen un código, nombre, descripción, fecha de inicio, fecha de finalización y un presupuesto 
      asignado.
    - Cada proyecto es gestionado por un gerente y puede tener varios desarrolladores trabajando en él.
    - Un proyecto es  desarrollado en una sucursal específica, pero puede involucrar a empleados de otras sucursales.

Proyectos: - (Nodo)
    - Código - (Atributo)
    - Nombre - (Atributo)
    - Descripción - (Atributo)
    - Fecha de Inicio - (Atributo)
    - Fecha de Finalización - (Atributo)
    - Presupuesto - (Atributo)
        - Cada proyecto es gestionado por un gerente y puede tener varios desarrolladores. - (Relación con empleados)
        - Cada proyecto es de una sucursal especifica, pero puede tener empleados de otras sucursales. - (Relación con sucursal)

Clientes:
    - Cada proyecto está asociado a un cliente, y se requiere su nombre, empresa, teléfono de contacto y correo 
      electrónico.
    - Un cliente puede contratar múltiples proyectos en diferentes sucursales.

Clientes: - (Nodo)
    - Nombre - (Atributo)
    - Empresa - (Atributo)
    - Telefono de contacto - (Atributo)
    - Correo electrónico - (Atributo)
        - Proyecto asociado a cliente - (Relación con cliente)
        - Un cliente puede tener varios proyectos en diferentes sucursales - (Relación con cliente, mismo que la pasada, pero solo implica que un cliente puede tener mas de un proyecto)

Reuniones y visitas:
    - Las sucursales tienen reuniones con clientes. Se debe registrar el cliente, la fecha, la hora y los asistentes 
      de la reunión (empleados de la empresa).
    - Se realizan visitas a las sucursales por parte de los clientes, registrando la fecha, hora, cliente, y motivo 
      de la visita.

Reuniones: (Reunion hecha con los clientes) - (Nodo)
    - Cliente - (Relación)
    - Fecha - (Atributo)
    - Hora - (Atributo)
    - Asistentes de la reunion (empleados) - (Varias relaciones)

Visitas: (Visitas a las sucursales de los clientes) - (Relación)
    - Fecha - (Atributo)
    - Hora - (Atributo)
    - Cliente - (Relación con nodo Cliente)
    - Motivo de visita - (Atributo)
    


Consultas (Querys):
Q00. Script del escenario de datos.
Q01. Obtener la lista de sucursales que tienen más de 5 empleados.
Q02. Encontrar los gerentes que gestionan más de 3 proyectos simultáneamente.
Q03. Obtener la lista de desarrolladores con especialización en back-end que están trabajando en más de 2 proyectos.
Q04. Obtener la lista de proyectos que tienen un presupuesto mayor a $1,000,000.
Q05. Listar los empleados de soporte técnico de todas las sucursales
Q06. Encontrar los proyectos que corresponden a un cliente en específico.
Q07. Obtener la lista de sucursales que han recibido visitas de más de 5 clientes diferentes.
Q08. Encontrar a los desarrolladores que han trabajado en proyectos con un presupuesto total mayor a $500,000.
Q09. Obtener la lista de clientes que han contratado más de 3 proyectos en diferentes sucursales.
Q10. Encontrar las sucursales que tienen más de 5 desarrolladores especializados en full-stack.
Q11. Transferir todos los empleados de soporte técnico de una sucursal en específico hacia otra sucursal.
Q12. Reemplaza al gerente de una sucursal en específico..
Q13. Cambie un proyecto en específico a otra sucursal, incluyendo la totalidad de participantes en el proyecto .
Q14. Obtener la lista de clientes que nunca han realizado visitas a las sucursales.
Q15. Todos los empleados de una sucursal determinada son transferidos a otra sucursal por cierre de sucursal de origen.



<!-- Modelado -->
# Sucursales
CREATE (s:Sucursal {clave: 'SUC1', nombre: 'Sucursal Nayarit',      direccion: 'Av. Insurgentes 12',    ciudad: 'Tepic',      capacidad: 10}) RETURN s;
CREATE (s:Sucursal {clave: 'SUC2', nombre: 'Sucursal Guadalajara',  direccion: 'Av. Mexico 34',         ciudad: 'Zapopan',    capacidad: 10}) RETURN s;
CREATE (s:Sucursal {clave: 'SUC3', nombre: 'Sucursal CDMX',         direccion: 'Av. Tecnológico 56',    ciudad: 'Iztacalco',  capacidad: 10}) RETURN s;
CREATE (s:Sucursal {clave: 'SUC4', nombre: 'Sucursal Tamaulipas',   direccion: 'Av. Del Ejército 78',   ciudad: 'Reynosa',    capacidad: 10}) RETURN s;
CREATE (s:Sucursal {clave: 'SUC5', nombre: 'Sucursal Monterrey',    direccion: 'Av. De la Cultura 90',  ciudad: 'Apodaca',    capacidad: 10}) RETURN s;


# Empleados - Gerentes
CREATE (e:Empleado {nombre: "Ana Gómez",      CURP: "GOMA901202MDFRRN03", telefono: "555-1234", cuentaBancaria: "1234567890", fechaContratacion: "1990-12-02", tipo: "Gerente"}) RETURN e;  // Sucursal 1
CREATE (e:Empleado {nombre: "Luis Morales",   CURP: "MOLU900101HDFRRR01", telefono: "555-5678", cuentaBancaria: "0987654321", fechaContratacion: "1990-01-01", tipo: "Gerente"}) RETURN e;  // Sucursal 2
CREATE (e:Empleado {nombre: "María López",    CURP: "LOMA890303MDFRTR09", telefono: "555-2345", cuentaBancaria: "5678901234", fechaContratacion: "1989-03-03", tipo: "Gerente"}) RETURN e;  // Sucursal 3
CREATE (e:Empleado {nombre: "Carlos Sánchez", CURP: "SACA910202HDFRLD04", telefono: "555-6789", cuentaBancaria: "4321098765", fechaContratacion: "1991-02-02", tipo: "Gerente"}) RETURN e;  // Sucursal 4
CREATE (e:Empleado {nombre: "Julia Ramírez",  CURP: "RAJU871230MDFRRJ07", telefono: "555-7890", cuentaBancaria: "3210987654", fechaContratacion: "1987-12-30", tipo: "Gerente"}) RETURN e;  // Sucursal 5

# Empleados - Desarrolladores
<!-- Sucursal 1 -->
CREATE (e:Empleado {nombre: "Fernando Hernández", CURP: "HEFE881231HDFRRD02", telefono: "555-3456", cuentaBancaria: "4567890123", fechaContratacion: "1988-12-31", tipo: "Desarrollador", especializacion: "Backend"})    RETURN e;
CREATE (e:Empleado {nombre: "Pedro Torres",       CURP: "TOPE870301HDFRRL08", telefono: "555-5670", cuentaBancaria: "8901234567", fechaContratacion: "1987-03-01", tipo: "Desarrollador", especializacion: "Full-stack"}) RETURN e;
<!-- Sucursal 2 -->
CREATE (e:Empleado {nombre: "Sara Castillo",      CURP: "CASA900201MDFRRC06", telefono: "555-4567", cuentaBancaria: "6789012345", fechaContratacion: "1990-02-01", tipo: "Desarrollador", especializacion: "Frontend"})   RETURN e;
CREATE (e:Empleado {nombre: "Laura Fernández",    CURP: "FELA920101MDFRRN01", telefono: "555-6781", cuentaBancaria: "5678901234", fechaContratacion: "1992-01-01", tipo: "Desarrollador", especializacion: "Backend"})    RETURN e;
<!-- Sucursal 3 -->
CREATE (e:Empleado {nombre: "Roberto Jiménez",    CURP: "JIRO850102HDFRMS05", telefono: "555-7892", cuentaBancaria: "0987654321", fechaContratacion: "1985-01-02", tipo: "Desarrollador", especializacion: "Frontend"})   RETURN e;
CREATE (e:Empleado {nombre: "Cristina Ruiz",      CURP: "RUCR900303MDFRRT03", telefono: "555-8912", cuentaBancaria: "3456789012", fechaContratacion: "1990-03-03", tipo: "Desarrollador", especializacion: "Full-stack"}) RETURN e;
<!-- Sucursal 4 -->
CREATE (e:Empleado {nombre: "Miguel Vargas",      CURP: "VAMI871231HDFRRN04", telefono: "555-9013", cuentaBancaria: "1230984567", fechaContratacion: "1987-12-31", tipo: "Desarrollador", especializacion: "Backend"})    RETURN e;
CREATE (e:Empleado {nombre: "Patricia Peña",      CURP: "PEPA910102MDFRRR09", telefono: "555-1023", cuentaBancaria: "2109876543", fechaContratacion: "1991-01-02", tipo: "Desarrollador", especializacion: "Frontend"})   RETURN e;
<!-- Sucursal 5 -->
CREATE (e:Empleado {nombre: "Javier Gutiérrez",   CURP: "GUJA890203HDFRRR07", telefono: "555-2034", cuentaBancaria: "3456789123", fechaContratacion: "1989-02-03", tipo: "Desarrollador", especializacion: "Full-stack"}) RETURN e;
CREATE (e:Empleado {nombre: "Sandra Mendoza",     CURP: "MESA921230MDFRRM05", telefono: "555-3045", cuentaBancaria: "6789012345", fechaContratacion: "1992-12-30", tipo: "Desarrollador", especializacion: "Frontend"})   RETURN e;

# Empleados - Soporte Técnico
<!-- Sucursal 1 -->
CREATE (e:Empleado {nombre: "Oscar López",          CURP: "LOOS900303HDFRRR01", telefono: "555-4560", cuentaBancaria: "8901234567", fechaContratacion: "1990-03-03", tipo: "Soporte Técnico", tipoSoporte: "Infraestructura"}) RETURN e;
CREATE (e:Empleado {nombre: "Gabriela Ríos",        CURP: "RIGA920101MDFRRJ02", telefono: "555-5671", cuentaBancaria: "6789012345", fechaContratacion: "1992-01-01", tipo: "Soporte Técnico", tipoSoporte: "Software"})        RETURN e;
<!-- Sucursal 2 -->
CREATE (e:Empleado {nombre: "Francisco Domínguez",  CURP: "DOFR870201HDFRRN04", telefono: "555-6782", cuentaBancaria: "1234567890", fechaContratacion: "1987-02-01", tipo: "Soporte Técnico", tipoSoporte: "Hardware"})        RETURN e;
CREATE (e:Empleado {nombre: "Daniela Silva",        CURP: "SIDA900202MDFRRL08", telefono: "555-7893", cuentaBancaria: "0987654321", fechaContratacion: "1990-02-02", tipo: "Soporte Técnico", tipoSoporte: "Infraestructura"}) RETURN e;
<!-- Sucursal 3 -->
CREATE (e:Empleado {nombre: "Ernesto Cruz",         CURP: "CRER881202HDFRRJ03", telefono: "555-8901", cuentaBancaria: "1230984567", fechaContratacion: "1988-12-02", tipo: "Soporte Técnico", tipoSoporte: "Software"})        RETURN e;
CREATE (e:Empleado {nombre: "Monica García",        CURP: "GAMA920303MDFRRL07", telefono: "555-9014", cuentaBancaria: "2109876543", fechaContratacion: "1992-03-03", tipo: "Soporte Técnico", tipoSoporte: "Infraestructura"}) RETURN e;
<!-- Sucursal 4 -->
CREATE (e:Empleado {nombre: "Alejandro Navarro",    CURP: "NAAL900101HDFRRJ06", telefono: "555-1012", cuentaBancaria: "6789012345", fechaContratacion: "1990-01-01", tipo: "Soporte Técnico", tipoSoporte: "Hardware"})        RETURN e;
CREATE (e:Empleado {nombre: "Verónica Delgado",     CURP: "DEVE911230MDFRRN09", telefono: "555-2035", cuentaBancaria: "3456789012", fechaContratacion: "1991-12-30", tipo: "Soporte Técnico", tipoSoporte: "Software"})        RETURN e;
<!-- Sucursal 5 -->
CREATE (e:Empleado {nombre: "Rodrigo Villanueva",   CURP: "VIRO870102HDFRRN02", telefono: "555-3046", cuentaBancaria: "8901234567", fechaContratacion: "1987-01-02", tipo: "Soporte Técnico", tipoSoporte: "Hardware"})        RETURN e;
CREATE (e:Empleado {nombre: "Isabel Flores",        CURP: "FLIS900202MDFRRL03", telefono: "555-4561", cuentaBancaria: "1234567890", fechaContratacion: "1990-02-02", tipo: "Soporte Técnico", tipoSoporte: "Infraestructura"}) RETURN e;


# Relaciones Sucursales-Empleados
<!-- Sucursal 1 -->
MATCH (s:Sucursal {clave: 'SUC1'}), (e:Empleado {CURP: 'GOMA901202MDFRRN03'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC1'}), (e:Empleado {CURP: 'HEFE881231HDFRRD02'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC1'}), (e:Empleado {CURP: 'TOPE870301HDFRRL08'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC1'}), (e:Empleado {CURP: 'LOOS900303HDFRRR01'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC1'}), (e:Empleado {CURP: 'RIGA920101MDFRRJ02'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;

<!-- Sucursal 2 -->
MATCH (s:Sucursal {clave: 'SUC2'}), (e:Empleado {CURP: 'MOLU900101HDFRRR01'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC2'}), (e:Empleado {CURP: 'CASA900201MDFRRC06'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC2'}), (e:Empleado {CURP: 'FELA920101MDFRRN01'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC2'}), (e:Empleado {CURP: 'DOFR870201HDFRRN04'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC2'}), (e:Empleado {CURP: 'SIDA900202MDFRRL08'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;

<!-- Sucursal 3 -->
MATCH (s:Sucursal {clave: 'SUC3'}), (e:Empleado {CURP: 'LOMA890303MDFRTR09'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC3'}), (e:Empleado {CURP: 'JIRO850102HDFRMS05'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC3'}), (e:Empleado {CURP: 'RUCR900303MDFRRT03'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC3'}), (e:Empleado {CURP: 'CRER881202HDFRRJ03'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC3'}), (e:Empleado {CURP: 'GAMA920303MDFRRL07'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;

<!-- Sucursal 4 -->
MATCH (s:Sucursal {clave: 'SUC4'}), (e:Empleado {CURP: 'SACA910202HDFRLD04'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC4'}), (e:Empleado {CURP: 'VAMI871231HDFRRN04'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC4'}), (e:Empleado {CURP: 'PEPA910102MDFRRR09'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC4'}), (e:Empleado {CURP: 'NAAL900101HDFRRJ06'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC4'}), (e:Empleado {CURP: 'DEVE911230MDFRRN09'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;

<!-- Sucursal 5 -->
MATCH (s:Sucursal {clave: 'SUC5'}), (e:Empleado {CURP: 'RAJU871230MDFRRJ07'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC5'}), (e:Empleado {CURP: 'GUJA890203HDFRRR07'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC5'}), (e:Empleado {CURP: 'MESA921230MDFRRM05'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC5'}), (e:Empleado {CURP: 'VIRO870102HDFRRN02'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;
MATCH (s:Sucursal {clave: 'SUC5'}), (e:Empleado {CURP: 'FLIS900202MDFRRL03'})
CREATE (s)-[:TIENE_EMPLEADO]->(e) RETURN s,e;



# Proyectos
<!-- Proyecto 1 -->
CREATE (p:Proyecto {codigo: 'Proyecto1', nombre: 'Proyecto 1', descripcion: 'Algo algo este es el proyecto 1', fecha_inicio: date('2024-01-01'), fecha_fin: date('2024-08-11'), presupuesto: 50000}) RETURN p;
<!-- Relaciones de proyecto - Gerente 1, Desarrollador 1-1, Soporte 2-1 -->
MATCH (p:Proyecto {codigo: 'Proyecto1'}), (e:Empleado:Gerente {CURP: 'GOMA901202MDFRRN03'})
CREATE (e)-[:GESTIONA]->(p) RETURN p,e;
MATCH (p:Proyecto {codigo: 'Proyecto1'}), (e:Empleado:Desarrollador {CURP: 'HEFE881231HDFRRD02'})
CREATE (e)-[:TRABAJA_EN]->(p) RETURN p,e;
MATCH (p:Proyecto {codigo: 'Proyecto1'}), (e:Empleado:Soporte {CURP: 'DOFR870201HDFRRN04'})
CREATE (e)-[:TRABAJA_EN]->(p) RETURN p,e;
<!-- Relación Proyecto - Sucursal -->
MATCH (s:Sucursal {clave: 'SUC1'}), (p:Proyecto {codigo: 'Proyecto1'})
CREATE (p)-[:UBICADO_EN]->(s) RETURN s,p;


<!-- Proyecto 2 -->
CREATE (p:Proyecto {codigo: 'Proyecto2', nombre: 'Proyecto 2', descripcion: 'Algo algo este es el proyecto 2', fecha_inicio: date('2024-02-02'), fecha_fin: date('2024-09-12'), presupuesto: 60000}) RETURN p;
<!-- Relaciones de proyecto - Gerente 2, Desarrollador 2-1, Soporte 3-1 -->
MATCH (p:Proyecto {codigo: 'Proyecto2'}), (e:Empleado:Gerente {CURP: 'MOLU900101HDFRRR01'})
CREATE (e)-[:GESTIONA]->(p) RETURN p,e;
MATCH (p:Proyecto {codigo: 'Proyecto2'}), (e:Empleado:Desarrollador {CURP: 'CASA900201MDFRRC06'})
CREATE (e)-[:TRABAJA_EN]->(p) RETURN p,e;
MATCH (p:Proyecto {codigo: 'Proyecto2'}), (e:Empleado:Soporte {CURP: 'CRER881202HDFRRJ03'})
CREATE (e)-[:TRABAJA_EN]->(p) RETURN p,e;
<!-- Relación Proyecto - Sucursal -->
MATCH (s:Sucursal {clave: 'SUC2'}), (p:Proyecto {codigo: 'Proyecto2'})
CREATE (p)-[:UBICADO_EN]->(s) RETURN s,p;


<!-- Proyecto 3 -->
CREATE (p:Proyecto {codigo: 'Proyecto3', nombre: 'Proyecto 3', descripcion: 'Algo algo este es el proyecto 3', fecha_inicio: date('2024-03-03'), fecha_fin: date('2024-10-13'), presupuesto: 70000}) RETURN p;
<!-- Relaciones de proyecto - Gerente 3, Desarrollador 3-1, Soporte 4-1 -->
MATCH (p:Proyecto {codigo: 'Proyecto3'}), (e:Empleado:Gerente {CURP: 'LOMA890303MDFRTR09'})
CREATE (e)-[:GESTIONA]->(p) RETURN p,e;
MATCH (p:Proyecto {codigo: 'Proyecto3'}), (e:Empleado:Desarrollador {CURP: 'JIRO850102HDFRMS05'})
CREATE (e)-[:TRABAJA_EN]->(p) RETURN p,e;
MATCH (p:Proyecto {codigo: 'Proyecto3'}), (e:Empleado:Soporte {CURP: 'NAAL900101HDFRRJ06'})
CREATE (e)-[:TRABAJA_EN]->(p) RETURN p,e;
<!-- Relación Proyecto - Sucursal -->
MATCH (s:Sucursal {clave: 'SUC3'}), (p:Proyecto {codigo: 'Proyecto3'})
CREATE (p)-[:UBICADO_EN]->(s) RETURN s,p;


<!-- Proyecto 4 -->
CREATE (p:Proyecto {codigo: 'Proyecto4', nombre: 'Proyecto 4', descripcion: 'Algo algo este es el proyecto 4', fecha_inicio: date('2024-04-04'), fecha_fin: date('2024-11-14'), presupuesto: 80000}) RETURN p;
<!-- Relaciones de proyecto - Gerente 4, Desarrollador 4-1, Soporte 5-1 -->
MATCH (p:Proyecto {codigo: 'Proyecto4'}), (e:Empleado:Gerente {CURP: 'SACA910202HDFRLD04'})
CREATE (e)-[:GESTIONA]->(p) RETURN p,e;
MATCH (p:Proyecto {codigo: 'Proyecto4'}), (e:Empleado:Desarrollador {CURP: 'VAMI871231HDFRRN04'})
CREATE (e)-[:TRABAJA_EN]->(p) RETURN p,e;
MATCH (p:Proyecto {codigo: 'Proyecto4'}), (e:Empleado:Soporte {CURP: 'VIRO870102HDFRRN02'})
CREATE (e)-[:TRABAJA_EN]->(p) RETURN p,e;
<!-- Relación Proyecto - Sucursal -->
MATCH (s:Sucursal {clave: 'SUC4'}), (p:Proyecto {codigo: 'Proyecto4'})
CREATE (p)-[:UBICADO_EN]->(s) RETURN s,p;


<!-- Proyecto 5 -->
CREATE (p:Proyecto {codigo: 'Proyecto5', nombre: 'Proyecto 5', descripcion: 'Algo algo este es el proyecto 5', fecha_inicio: date('2024-05-05'), fecha_fin: date('2024-12-15'), presupuesto: 90000}) RETURN p;
<!-- Relaciones de proyecto - Gerente 5, Desarrollador 5-1, Soporte 1-1 -->
MATCH (p:Proyecto {codigo: 'Proyecto5'}), (e:Empleado:Gerente {CURP: 'RAJU871230MDFRRJ07'})
CREATE (e)-[:GESTIONA]->(p) RETURN p,e;
MATCH (p:Proyecto {codigo: 'Proyecto5'}), (e:Empleado:Desarrollador {CURP: 'GUJA890203HDFRRR07'})
CREATE (e)-[:TRABAJA_EN]->(p) RETURN p,e;
MATCH (p:Proyecto {codigo: 'Proyecto5'}), (e:Empleado:Soporte {CURP: 'LOOS900303HDFRRR01'})
CREATE (e)-[:TRABAJA_EN]->(p) RETURN p,e;
<!-- Relación Proyecto - Sucursal -->
MATCH (s:Sucursal {clave: 'SUC5'}), (p:Proyecto {codigo: 'Proyecto5'})
CREATE (p)-[:UBICADO_EN]->(s) RETURN s,p;


# Clientes
CREATE (c:Cliente {nombre: 'Acme Corp',           empresa: 'Acme Corp',           telefono: '5598765432', correo: 'contacto@acmecorp.com'})         RETURN c;
CREATE (c:Cliente {nombre: 'Global Solutions',    empresa: 'Global Solutions',    telefono: '5587654321', correo: 'info@globalsolutions.com'})      RETURN c;
CREATE (c:Cliente {nombre: 'Innovatech',          empresa: 'Innovatech',          telefono: '5576543210', correo: 'contacto@innovatech.com'})       RETURN c;
CREATE (c:Cliente {nombre: 'NextGen Industries',  empresa: 'NextGen Industries',  telefono: '5565432109', correo: 'support@nextgenindustries.com'}) RETURN c;
CREATE (c:Cliente {nombre: 'Prime Services',      empresa: 'Prime Services',      telefono: '5554321098', correo: 'hello@primeservices.com'})       RETURN c;


# Relaciones Cliente-Proyecto
<!-- Cliente 1 - Proyecto 1 -->
MATCH (c:Cliente {nombre: 'Acme Corp'}), (p:Proyecto {codigo: 'Proyecto1'})
CREATE (c)-[:CONTRATA]->(p) RETURN c,p;

<!-- Cliente 2 - Proyecto 2 -->
MATCH (c:Cliente {nombre: 'Global Solutions'}), (p:Proyecto {codigo: 'Proyecto2'})
CREATE (c)-[:CONTRATA]->(p) RETURN c,p;

<!-- Cliente 3 - Proyecto 3 -->
MATCH (c:Cliente {nombre: 'Innovatech'}), (p:Proyecto {codigo: 'Proyecto3'})
CREATE (c)-[:CONTRATA]->(p) RETURN c,p;

<!-- Cliente 4 - Proyecto 4 -->
MATCH (c:Cliente {nombre: 'NextGen Industries'}), (p:Proyecto {codigo: 'Proyecto4'})
CREATE (c)-[:CONTRATA]->(p) RETURN c,p;

<!-- Cliente 5 - Proyecto 5 -->
MATCH (c:Cliente {nombre: 'Prime Services'}), (p:Proyecto {codigo: 'Proyecto5'})
CREATE (c)-[:CONTRATA]->(p) RETURN c,p;



# Reuniones Sucursal - Cliente
<!-- Reunion Sucursal 1 - Cliente 1 - Proyecto 1 -->
CREATE (r:Reunion {fecha: date('2024-02-10'), hora: time('12:00'), motivo: 'Reunion para Proyecto 1'})
MATCH (c:Cliente {nombre: 'Acme Corp'})
MATCH (s:Sucursal {clave: 'SUC1'})
MATCH (e1:Empleado {CURP: 'GOMA901202MDFRRN03'})
MATCH (e2:Empleado {CURP: 'HEFE881231HDFRRD02'})
MATCH (e3:Empleado {CURP: 'DOFR870201HDFRRN04'})
MERGE (r)-[r:REUNION_EN]->(s)
MERGE (c)-[a:ASISTENCIA]->(r)
MERGE (e1)-[a:ASISTENCIA]->(r)
MERGE (e2)-[a:ASISTENCIA]->(r)
MERGE (e3)-[a:ASISTENCIA]->(r)
RETURN s,r,c,e1,e2,e3;

<!-- Reunion Sucursal 2 - Cliente 2 - Proyecto 2 -->
CREATE (r:Reunion {fecha: date('2024-03-11'), hora: time('13:00'), motivo: 'Reunion para Proyecto 2'})
MATCH (c:Cliente {nombre: 'Global Solutions'})
MATCH (s:Sucursal {clave: 'SUC2'})
MATCH (e1:Empleado {CURP: 'MOLU900101HDFRRR01'})
MATCH (e2:Empleado {CURP: 'CASA900201MDFRRC06'})
MATCH (e3:Empleado {CURP: 'CRER881202HDFRRJ03'})
MERGE (r)-[r:REUNION_EN]->(s)
MERGE (c)-[a:ASISTENCIA]->(r)
MERGE (e1)-[a:ASISTENCIA]->(r)
MERGE (e2)-[a:ASISTENCIA]->(r)
MERGE (e3)-[a:ASISTENCIA]->(r)
RETURN s,r,c,e1,e2,e3;

<!-- Reunion Sucursal 3 - Cliente 3 - Proyecto 3 -->
CREATE (r:Reunion {fecha: date('2024-04-12'), hora: time('14:00'), motivo: 'Reunion para Proyecto 3'})
MATCH (c:Cliente {nombre: 'Innovatech'})
MATCH (s:Sucursal {clave: 'SUC3'})
MATCH (e1:Empleado {CURP: 'LOMA890303MDFRTR09'})
MATCH (e2:Empleado {CURP: 'JIRO850102HDFRMS05'})
MATCH (e3:Empleado {CURP: 'NAAL900101HDFRRJ06'})
MERGE (r)-[r:REUNION_EN]->(s)
MERGE (c)-[a:ASISTENCIA]->(r)
MERGE (e1)-[a:ASISTENCIA]->(r)
MERGE (e2)-[a:ASISTENCIA]->(r)
MERGE (e3)-[a:ASISTENCIA]->(r)
RETURN s,r,c,e1,e2,e3;

<!-- Reunion Sucursal 4 - Cliente 4 - Proyecto 4 -->
CREATE (r:Reunion {fecha: date('2024-05-13'), hora: time('15:00'), motivo: 'Reunion para Proyecto 4'})
MATCH (c:Cliente {nombre: 'NextGen Industries'})
MATCH (s:Sucursal {clave: 'SUC4'})
MATCH (e1:Empleado {CURP: 'SACA910202HDFRLD04'})
MATCH (e2:Empleado {CURP: 'VAMI871231HDFRRN04'})
MATCH (e3:Empleado {CURP: 'VIRO870102HDFRRN02'})
MERGE (r)-[r:REUNION_EN]->(s)
MERGE (c)-[a:ASISTENCIA]->(r)
MERGE (e1)-[a:ASISTENCIA]->(r)
MERGE (e2)-[a:ASISTENCIA]->(r)
MERGE (e3)-[a:ASISTENCIA]->(r)
RETURN s,r,c,e1,e2,e3;

<!-- Reunion Sucursal 5 - Cliente 5 - Proyecto 5 -->
CREATE (r:Reunion {fecha: date('2024-06-14'), hora: time('16:00'), motivo: 'Reunion para Proyecto 5'})
MATCH (c:Cliente {nombre: 'Prime Services'})
MATCH (s:Sucursal {clave: 'SUC5'})
MATCH (e1:Empleado {CURP: 'RAJU871230MDFRRJ07'})
MATCH (e2:Empleado {CURP: 'GUJA890203HDFRRR07'})
MATCH (e3:Empleado {CURP: 'LOOS900303HDFRRR01'})
MERGE (r)-[r:REUNION_EN]->(s)
MERGE (c)-[a:ASISTENCIA]->(r)
MERGE (e1)-[a:ASISTENCIA]->(r)
MERGE (e2)-[a:ASISTENCIA]->(r)
MERGE (e3)-[a:ASISTENCIA]->(r)
RETURN s,r,c,e1,e2,e3;


# Visitas
CREATE (v:Visita {fecha: date('2024-03-15'), hora: time('10:00'), motivo: 'Revisión de instalaciones'})
MATCH (s:Sucursal {clave: 'SUC1'}), (c:Cliente {nombre: 'Acme Corp'})
CREATE (s)-[v:VISITADA_POR]->(v);
CREATE (v)-[r:REALIZADA_POR]->(c);
