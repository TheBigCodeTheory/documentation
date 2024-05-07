# Docs API

## Introducción

Este documento proporciona una guía completa para utilizar la API de "The Big Code Theory". Aquí encontrarás detalles sobre los endpoints disponibles, su lógica subyacente y cómo interactuar con ellos.

---

## Base URL

La URL base para todos los endpoints de la API es: `https://api.bigcodetheory.com/api/v1`

---

## Endpoints

### AUTH

#### `POST /auth/register`

Este endpoint se utiliza para registrar un nuevo usuario en la plataforma.

Si el correo electrónico no está asociado con una cuenta existente, se generará un código de verificación de 6 dígitos y se enviará al correo electrónico proporcionado. Este código de verificación deberá utilizarse para completar el proceso de registro.

#### Parámetros de consulta

```json
{
  "email": "correo@example.com",
  "firstname": "Nombre",
  "lastname": "Apellido"
}
```

#### Respuesta exitosa

```json
{
  "status": true,
  "path": "/api/v1/auth/register",
  "statusCode": 201,
  "result": {
    "_id": "ObjectId",
    "firstname": "Nombre",
    "lastname": "Apellido",
    "email": "correo@example.com",
    "auth": "ObjectId",
    "createdAt": "Date",
    "updatedAt": "Date"
  }
}
```

#### `POST /auth/code`

Este endpoint se utiliza para generar un nuevo código de verificación y enviarlo por correo electrónico al usuario correspondiente. También se puede utilizar para reenviar el código de verificación si el usuario no ha recibido el correo electrónico inicial.

#### Parámetros de consulta

```json
{
  "email": "correo@example.com"
}
```

#### Respuesta exitosa

```json
{
  "status": true,
  "path": "/api/v1/auth/code",
  "statusCode": 201
}
```

#### `POST /auth/token`

Este endpoint se utiliza para generar un token de autenticación válido utilizando un código de verificación previamente enviado al usuario por correo electrónico.

Este token de autenticación generado debe ser incluido como parte de la cabecera Authorization en las solicitudes posteriores a otros endpoints de la API para autenticar al usuario.

#### Parámetros de consulta

```json
{
  "email": "correo@example.com",
  "code": "123456"
}
```

#### Respuesta exitosa

```json
{
  "status": true,
  "path": "/api/v1/auth/token",
  "statusCode": 201,
  "result": {
    "token": "token",
    "user": {
      "id": "ObjectId",
      "name": "Nombre"
    }
  }
}
```
