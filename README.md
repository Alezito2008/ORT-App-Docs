# ORT App Docs

## Generar Token
- **Ruta**: ```/WcfSecundarioRest_v2.0/SecundarioRest.svc/GenerateToken```
- **Método**: POST
-**Respuesta**
```json
{
  "Codigo": 200,
  "Descripcion": "",
  "ResetPassPage": "http://extranet.ort.edu.ar/on_line/asp_html/Usuarios/mobile/Reseteo_Password.asp",
  "Token": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
```

***HAY QUE PONER EN HEADERS EL TOKEN EN EL ATRIBUTO "Authorization"*** PARA TODOS LOS REQUESTS

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

