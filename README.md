# Generador de Firmas de Correo - Ayuntamiento de Aranda de Duero

Herramienta web para que el personal del Ayuntamiento de Aranda de Duero genere su firma de correo con un formato único y el logo de su concejalía, sin conocimientos técnicos.

**Úsala aquí: <https://arandadeduero.github.io/firmas-correo/>**

## 🚀 Cómo usarla

1. Abre el generador y rellena los campos obligatorios (\*):
   - Nombre completo
   - Puesto/Cargo
   - Concejalía
   - Correo electrónico (debe terminar en `@arandadeduero.es`)
2. Opcionalmente, añade un teléfono.
3. La firma aparece en la vista previa según escribes. Si falta algún dato, el botón **Generar firma** te indica cuál.
4. Copia la firma con uno de los dos botones:
   - **Copiar vista previa (con formato)**: para pegarla directamente en el editor de firmas del cliente de correo.
   - **Copiar código HTML**: para clientes que piden el HTML de la firma.

Los datos se guardan en el navegador (`localStorage`) para no tener que volver a escribirlos; no se envían a ningún servidor.

### Dónde pegarla

- **Gmail**: Ajustes → General → Firma → pegar la vista previa
- **Outlook**: Archivo → Opciones → Correo → Firmas → Nueva → pegar la vista previa
- **Thunderbird**: Configuración de la cuenta → Texto de la firma → marcar «Usar HTML» → pegar el código HTML

### Casos especiales

- Si el puesto empieza por «Alcald…» o «Concejal…», o se elige «Alcaldía + Concejales», la línea de la concejalía no se muestra.
- «Alcaldía + Concejales» usa el logo general del Ayuntamiento en lugar del de una concejalía.

## 🎯 Por qué firmas estandarizadas

- **Imagen institucional coherente**: mismo formato, logo y colores en todos los correos.
- **Contacto siempre presente**: nombre, puesto, correo y teléfono en el mismo sitio.
- **Sin errores ni edición manual**: nadie tiene que maquetar su firma ni buscar el logo correcto.
- **Cambios centralizados**: el diseño se cambia en un solo lugar para todo el Ayuntamiento.

## 🛠️ Descripción técnica

```
firmas-correo/
├── index.html      # Toda la aplicación: HTML, CSS y JavaScript
├── images/
│   ├── blanco/     # Logo de cada concejalía (sobre fondo blanco)
│   └── colores/    # Logo general del Ayuntamiento
├── LICENSE
└── README.md
```

Es una única página estática en HTML, CSS y JavaScript nativo: sin frameworks, sin dependencias y sin paso de compilación. Lo único externo es la tipografía Outfit de Google Fonts, que usa la página del generador.

Se publica con GitHub Pages. Las firmas enlazan los logos por su URL pública (`BASE_URL` en `index.html`), así que las imágenes las sirve este repositorio.

> ⚠️ **No borres ni renombres imágenes.** Las firmas ya enviadas las cargan desde este repositorio; si un fichero desaparece, el logo se rompe en esos correos. Esto incluye los `.jpg` y los logos que ya no aparecen en el desplegable, que usaron versiones anteriores del generador.

### Probarlo en local

Abre `index.html` en el navegador o sirve la carpeta:

```sh
python3 -m http.server
```

Aunque se ejecute en local, las firmas generadas apuntan siempre a los logos publicados.

## 📝 Añadir o cambiar una concejalía

1. Guarda el logo como `images/blanco/<clave>.png` (los actuales miden 640 px de ancho). La clave va en minúsculas, sin tildes ni espacios: `_` separa palabras y `-` separa el área del servicio, por ejemplo `medio_ambiente-parques_y_jardines`.
2. En `index.html`, añade una línea al objeto `CONCEJALIAS` con esa misma clave y el nombre visible, respetando el orden alfabético:

   ```js
   "medio_ambiente-parques_y_jardines": "Medio Ambiente (Parques y Jardines)",
   ```

3. Publica el cambio. El desplegable se rellena solo a partir de `CONCEJALIAS`.

En la firma, el nombre se muestra precedido de «Concejalía de».

Para renombrar una concejalía basta con cambiar su nombre visible. Para retirarla, borra su línea de `CONCEJALIAS` pero conserva la imagen.

## 🎨 Cambiar el diseño de la firma

La firma es la plantilla HTML de la función `buildSignatureHTML()` en `index.html`. Usa una tabla y estilos en línea a propósito: es lo que los clientes de correo muestran de forma fiable, así que no los sustituyas por clases CSS.

El cambio solo afecta a las firmas que se generen a partir de entonces; quien ya tenga la suya debe volver a generarla.

El resto del CSS de `index.html` es el de la página del generador y no influye en la firma.

## 📄 Licencia

[Creative Commons Atribución-CompartirIgual 4.0 Internacional (CC BY-SA 4.0)](LICENSE).

## 👥 Contacto y soporte

Para avisar de un problema o pedir un cambio, contacta con el departamento de Informática del Ayuntamiento de Aranda de Duero o abre una incidencia en este repositorio.
