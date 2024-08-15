# ORT App Docs

## Generar Token
- **Ruta**: ```/WcfSecundarioRest_v2.0/SecundarioRest.svc/GenerateToken```
- **Método**: POST
- **Payload**
```json
{
  "DeviceId": id dispositivo (str) (random) "xxxxxxxxxxxxxxxx",
  "Password": "mob_ORTSecundario2016!",
  "PlatformId": 0
}
```
-**Respuesta**
```json
{
  "Codigo": 200,
  "Descripcion": "",
  "ResetPassPage": "http://extranet.ort.edu.ar/on_line/asp_html/Usuarios/mobile/Reseteo_Password.asp",
  "Token": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
```

HAY QUE PONER EN HEADERS EL TOKEN EN EL ATRIBUTO "Authorization" **PARA TODOS LOS REQUESTS**

## Login
Ruta: ```/WcfSecundarioRest_v2.0/SecundarioRest.svc/User/Login```
- **Método**: POST
- **Payload**
```json
{
  "UserCode": dni (int),
  "UserPass": contraseña (str),
  "Version":"3.4.0"
}
```
- **Respuestas**
**Correcto**:
```json
{
  "Codigo": 200,
  "Descripcion": "",
  "Result": {
    "Alumnos": [
      {
        "Apellidos": apellido (str),
        "CarreraId": 0,
        "Codigo": idUsuario (int),
        "Documento": documento (str),
        "Email": null,
        "EstadoId": 0,
        "FechaNacimiento": "/Date(-62135586000000-0300)/",
        "Folio": null,
        "GeneroId": "\u0000" (genero(?)),
        "Libro": null,
        "Nombres": nombre (str),
        "Orden": null,
        "RutaFoto": null,
        "TipoDocumento": 0
      }
    ],
    "CDSede": "2",
    "CUIL": null,
    "Codigo": dni (str),
    "Email": "",
    "Nombre": nombre con apellido (str),
    "Perfil": sede - nivel (str) Ej: "Belgrano - Secundario",
    "TipoPerfilId": 2
  }
}
```
**Incorrecto**:
```json
{
  "Codigo":512,
  "Descripcion":"Usuario o contraseña incorrecta",
  "Result":null
}
```

## Inasistencias
- **Ruta**: ```/WcfSecundarioRest_v2.0/SecundarioRest.svc/Assistance/UserCode=idUsuario```
- **Método**: GET
- **Respuesta**
```json
{
  "Codigo": 200,
  "Descripcion": "",
  "Inasistencias": {
    "CreditosTotales": inasistencias totales (default 15) (int),
    "CreditosUtilizados": inasistencias (int) ,
    "FechaLibre": "-",
    "Materias": null,
    "Reincorporacion": 0
  }
}

```
## Inasistencias Detalle
- **Ruta**: ```/WcfSecundarioRest_v2.0/SecundarioRest.svc/InasistenciaDetalle/UserCode=idUsuario/MatterCode=0```
- **Método**: GET
- **Respuesta**
```json
{
  "Codigo": 200,
  "Descripcion": "",
  "InasistenciaDetalle": {
    "DSFalta": null,
    "DTFechaLibre": null,
    "Id": 0,
    "ListInas": [
      {
        "DSFalta": Cantidad (str) Ej: "1",
        "DTFechaLibre": Fecha (str) Ej:"14/08/2024",
        "Id": idFalta (int),
        "ListInas": null,
        "rimd": ""
      },
      {
        "DSFalta": Cantidad (str) Ej: "0.5",
        "DTFechaLibre": Fecha (str) Ej:"12/08/2024",
        "Id": idFalta (int),
        "ListInas": null,
        "rimd": ""
      },
    ],
    "rimd": null
  }
}
```
## Periodos
- **Ruta**: ```/WcfSecundarioRest_v2.0/SecundarioRest.svc/PeriodosAlumno/UserCode=idUsuario```
- **Método**: GET
- **Respuesta**
```json
{
  "Codigo": 200,
  "Descripcion": "",
  "Periodos": {
    "CDCicloLectivo": null,
    "CDPeriodo": 0,
    "DSPeriodo": null,
    "ListPeriodos": [
      {
        "CDCicloLectivo": año (str) Ej: "2024",
        "CDPeriodo": código periodo (int) Ej: 16,
        "DSPeriodo": nombre (str) Ej: "Bimestre 1",
        "ListPeriodos": null
      },
      {
        "CDCicloLectivo": año (str) Ej: "2024",
        "CDPeriodo": código periodo (int) Ej: 20,
        "DSPeriodo": nombre (str) Ej: "Cuatrimestre 1",
        "ListPeriodos": null
      }
    ]
  }
}
```
## Calificaciones
- **Ruta**: ```/WcfSecundarioRest_v2.0/SecundarioRest.svc/Scores/UserCode=idUsuario/CodPeriod=16```
- **Método**: GET
- **Respuesta**
```json
{
  "Codigo": 200,
  "Descripcion": "",
  "Calificaciones": {
    "Ciclo": año (int) Ej: 2024,
    "ListCalificacionesDetalle": [
      {
        "CDPeriodo": codigoPeriodo (int),
        "CDTipoCalificacion": 2,
        "DSCalificacion": "M",
        "Descripcion": "Adeuda tareas y/o no comple con los plazos de entrega.",
        "ListCalificaciones": null
      },
      {
        "CDPeriodo": codigoPeriodo (int),
        "CDTipoCalificacion": 2,
        "DSCalificacion": "N",
        "Descripcion": "Adeuda contenidos de aprendizaje.",
        "ListCalificaciones": null
      },
      {
        "CDPeriodo": codigoPeriodo (int),
        "CDTipoCalificacion": 2,
        "DSCalificacion": "O",
        "Descripcion": "Baja participación en las clases.",
        "ListCalificaciones": null
      },
      {
        "CDPeriodo": codigoPeriodo (int),
        "CDTipoCalificacion": 3,
        "DSCalificacion": "P",
        "Descripcion": "Incrementar la participación activa en las clases.",
        "ListCalificaciones": null
      },
      {
        "CDPeriodo": codigoPeriodo (int),
        "CDTipoCalificacion": 3,
        "DSCalificacion": "Q",
        "Descripcion": "Incrementar el estudio cumpliendo en tiempo y forma con el trabajo en la asignatura.",
        "ListCalificaciones": null
      },
      {
        "CDPeriodo": codigoPeriodo (int),
        "CDTipoCalificacion": 3,
        "DSCalificacion": "R",
        "Descripcion": "Cumplir con las consignas y/o indicaciones  complementarias propuestas por su docente (revisión y entrega de trabajos, resolución de nuevas actividades, asistencia a clases de consulta, entre otras).",
        "ListCalificaciones": null
      }
    ],
    "NotaFinal": 0,
    "NotaFinalDescripcion": null,
    "Periodos": [
      {
        "Materias": [
          {
            "Calificaciones": [
              { "Descripcion": "Nota", "Id": 1, "Nota": numero / letra (str) },
              { "Descripcion": "Obs.", "Id": 2, "Nota": letra (str) },
              { "Descripcion": "Sug.", "Id": 3, "Nota": letra (str) }
            ],
            "Materia": {
              "Id": id materia (int),
              "Nombre": nombre materia (str) Ej: "MATEMATICA",
              "NombreCorto": nombre corto¿? materia (str) Ej: "MATEMATICA"
            }
          },
          {
            "Calificaciones": [
              { "Descripcion": "Nota", "Id": 1, "Nota": numero / letra (str) },
              { "Descripcion": "Obs.", "Id": 2, "Nota": letra (str) },
              { "Descripcion": "Sug.", "Id": 3, "Nota": letra (str) }
            ],
            "Materia": {
              "Id": id materia (int),
              "Nombre": nombre materia (str) Ej: "LENGUA Y LITERATURA",
              "NombreCorto": nombre corto¿? materia (str) Ej: "LENGUA Y LITERATURA"
            }
          }
        ],
        "Periodo": {
            "Codigo": codigoPeriodo (int),
            "Descripcion": bimestre / cuatrimestre (str) Ej: "Cuatrimestre 1"
        }
      }
    ]
  }
}
```
## Sanciones
- **Ruta**: ```/WcfSecundarioRest_v2.0/SecundarioRest.svc/Sanciones/UserCode=idUsuario```
- **Método**: GET
- **Respuesta**
```json
{
  "Codigo": 200,
  "Descripcion": "",
  "Sanciones": {
    "DSMotivo": null,
    "DSTipoSancion": null,
    "DTFecha_Sancion": null,
    "Id": 0,
    "ListSanciones": [
      {
        "DSMotivo": motivo (str),
        "DSTipoSancion": tipo (str) Ej: "Apercibimiento Escrito",
        "DTFecha_Sancion": fecha (str) Ej: "10/3/2024",
        "Id": id sancion (int),
        "ListSanciones": null
      },
      {
        "DSMotivo": motivo (str),
        "DSTipoSancion": tipo (str) Ej: "Apercibimiento Escrito",
        "DTFecha_Sancion": fecha (str) Ej: "10/3/2024",
        "Id": id sancion (int),
        "ListSanciones": null
      }
    ]
  }
}
```
