---
title: "Procedimiento de campo y gabinete — Levantamiento catastral con dron + GNSS"
subtitle: "Regularización de predios, Texcoco, Estado de México"
---

> **Documento de trabajo.** Es un procedimiento técnico práctico, no sustituye al *Manual Catastral del Estado de México* (IGECEM) vigente. Antes de entregar, contrasta el formato del plano, las tolerancias y los requisitos administrativos contra el manual y contra lo que pida la Dirección de Catastro de Texcoco. Los puntos marcados con **[VERIFICAR]** dependen de esa revisión.

# 1. Alcance

Obtener, para cada lote de una manzana o colonia en regularización:

- Coordenadas UTM de los vértices del predio y cuadro de construcción (rumbos, distancias, coordenadas).
- Superficie del terreno y perímetro.
- Colindancias por lado.
- Superficie construida (planimetría de construcciones sobre ortofoto).
- Curvas de nivel.
- Plano catastral firmado por el técnico acreditado.

**Estrategia:** se levanta **una manzana o un sector completo por jornada**, no lote por lote. Un vuelo y una sesión de base sirven para decenas de predios.

**Equipo de referencia:** dron DJI Mini 3, receptores GNSS base + rover RTK (propios o rentados), WebODM, QGIS/AutoCAD y la plantilla `Plantilla_Cuadro_de_Construccion.xlsx`.

# 2. Marco de referencia

| Concepto | Valor |
|---|---|
| Marco geodésico | ITRF2008, época 2010.0 (oficial INEGI) |
| Liga | Red Geodésica Nacional Activa (RGNA) de INEGI |
| Proyección | UTM zona 14 Norte (código EPSG:6369, *México ITRF2008 / UTM 14N*) |
| Alturas | Ortométricas, convertidas con el modelo geoidal de INEGI (GGM10 o el vigente) |
| Unidades | metros, 3 decimales en coordenadas y distancias |

**[VERIFICAR]** que el manual vigente y el catastro municipal pidan este mismo marco. Algunos catastros todavía trabajan en ITRF92 o en coordenadas locales. Si es así, pide al municipio sus parámetros de transformación.

# 3. Equipo y materiales (lista de revisión)

**GNSS**

- [ ] Receptor base + antena + tripié + base nivelante o bastón con bípode
- [ ] Rover + bastón de 2 m con nivel de burbuja calibrado
- [ ] Radio (LoRa/UHF) o datos móviles para las correcciones RTK
- [ ] Baterías cargadas y power bank; celular o colectora con la app (Emlid Flow, SW Maps, etc.)
- [ ] Cinta métrica de 30 m o distanciómetro láser (para vértices excéntricos)

**Dron**

- [ ] DJI Mini 3 con 3 baterías como mínimo y cargador para coche
- [ ] Microsd vacía (64 GB o más)
- [ ] App de vuelo automático compatible con tu modelo (Dronelink, Litchi u otra; **confirma la compatibilidad**)

**Señalización**

- [ ] 8 a 12 dianas de puntos de control (lona de 50×50 cm con patrón de damero blanco y negro, o pintura en aerosol sobre el pavimento)
- [ ] Clavos de acero tipo *PK* o varilla con tapón y pintura para marcar la base y los vértices
- [ ] Marcador, libreta de campo y formatos de acta de colindancia

**Documentos**

- [ ] Oficio del ayuntamiento que te acredita
- [ ] Croquis de la manzana con la lotificación de catastro
- [ ] Lista de propietarios y poseedores

# 4. Gabinete previo (1–2 días antes)

1. **Información base:** pide al ayuntamiento la cartografía catastral existente, las claves y el padrón de la zona. Descarga la ortofoto o la imagen satelital más reciente para planear.
2. **Delimitar el polígono de vuelo** con un margen de 20 a 30 m alrededor de la manzana.
3. **Espacio aéreo:** revisa las zonas GEO de DJI y las restricciones de la AFAC. Texcoco está en la zona de aproximación del AICM, así que algunas áreas pueden requerir desbloqueo o permiso. Lleva el oficio del ayuntamiento.
4. **Plan de puntos de control:**
   - Mínimo **5 puntos de control**: uno en cada esquina del polígono y uno al centro. Para más de 3 ha, uno más cada 1 a 2 ha.
   - Agrega **3 puntos de verificación** que **no** entran al procesamiento y sirven para medir la precisión.
   - Colócalos en lugares abiertos, sin sombra de árboles ni aleros, visibles desde el aire y estables (banqueta o calle).
5. **Plan de vuelo** (ver sección 6).
6. **Aviso a vecinos y colindantes:** el ayuntamiento debe citar a propietarios y colindantes para el día del levantamiento, porque los vértices se marcan **en presencia de ambos colindantes**. **[VERIFICAR]** en el manual el formato de citatorio o acta de verificación de linderos.

# 5. Base GNSS

1. **Ubicación:** un punto despejado (sin edificios ni árboles por encima de 15° de elevación), lejos de transformadores y antenas, donde no estorbe y quede seguro. Material: clavo PK en el concreto o una mojonera nueva.
2. **Instalación:** centra y nivela sobre el punto. Mide y anota la **altura de antena** y cómo la mediste (vertical o inclinada, a qué parte de la antena).
3. **Registro estático:** activa el registro bruto (RINEX u otro formato nativo) a 1 s, o a 5 s si solo usarás PPP. Deja la base fija **mínimo 2 horas, idealmente 4**, durante toda la jornada.
4. **Coordenada provisional:** arranca el RTK con la posición autónoma promediada de la base (con un error de unos metros). Al terminar la jornada esa coordenada se corrige (ver 8.1).
5. **Si ya tienes la base calculada de una visita anterior**, captura su coordenada ajustada y omite la corrección.
6. **Comprobación:** al inicio y al final de la jornada mide con el rover un punto fijo de control (por ejemplo, otro clavo PK a 20 m). Las dos lecturas deben coincidir en 2 cm o menos.

# 6. Vuelo con DJI Mini 3

| Parámetro | Valor recomendado |
|---|---|
| Altura | 50–60 m sobre el terreno (≈ 1.8–2.2 cm/píxel) |
| Traslape frontal / lateral | 80 % / 75 % |
| Velocidad | 3–5 m/s (el obturador es *rolling shutter*) |
| Cámara | Nadir (−90°), foto JPEG 12 MP, enfoque fijo a infinito |
| Exposición | Velocidad de obturación de 1/500 s o más rápida |
| Pasada adicional | Misma manzana en cruz o con la cámara a −60° (oblicua) para muros y fachadas |
| Horario | 10:00–14:00 h (sombras cortas), sin viento fuerte |
| Batería | Aterrizar con 25 % como mínimo |

- Dianas colocadas **antes** del despegue.
- Revisa en el sitio 5 o 6 fotos al azar para descartar imágenes movidas, quemadas o fuera de foco antes de retirarte.
- Copia la microSD a la laptop y a un disco o la nube el mismo día.

# 7. Medición con el rover

## 7.1 Puntos de control y de verificación
- Solo con solución **FIX**.
- Ocupa cada punto **dos veces** (levanta y reposiciona el bastón), registrando de 10 a 30 épocas cada vez. Las dos lecturas deben coincidir en 2 cm o menos en planta y 3 cm o menos en altura.
- Nombre: `GCP01, GCP02…` y `CHK01…` para los de verificación.
- Mide **el centro exacto** de la diana. Toma una foto de cada una.

## 7.2 Vértices de lotes
- Recorre la manzana con los colindantes. Cada vértice se **acuerda en sitio** y se marca (pintura o clavo).
- Nombre: `M{manzana}-L{lote}-V{n}`, por ejemplo `M05-L12-V1`. Si un vértice es compartido por varios lotes, mídelo **una sola vez** y anótalo como compartido en la libreta.
- Vértice con solución FLOAT o sin señal (pegado a barda alta, bajo árbol o alero), usa una de estas soluciones:
  - **Excéntrico:** mide dos puntos despejados alineados con el lindero y la distancia de cinta al vértice; luego calcúlalo en gabinete.
  - **Cinta de dos puntos:** mide 2 puntos con FIX y las distancias de cinta de cada uno al vértice; la posición sale por intersección de distancias.
  - Con IMU (si tu rover tiene compensación de inclinación): inclina el bastón hacia el vértice desde una posición despejada.
- Llena en la libreta, por cada lote: el croquis a mano, quién colinda por cada lado, el tipo de lindero (barda, malla, mojonera, imaginario) y si hay **diferencias o conflictos** con el vecino.
- Toma una foto de cada vértice con el letrero del nombre.

## 7.3 Acta de colindancias
Al terminar cada lote, firma con el propietario y los colindantes presentes el croquis o acta de reconocimiento de linderos. **[VERIFICAR]** el formato oficial que exige el ayuntamiento o IGECEM.

# 8. Gabinete posterior

## 8.1 Calcular la coordenada definitiva de la base
**Opción A (posproceso contra la RGNA):**

1. Consulta en el portal de INEGI cuáles estaciones RGNA están activas cerca de Texcoco.
2. Descarga sus archivos RINEX del mismo día y horario.
3. Procesa la línea base estación–base con RTKLIB (gratuito), Emlid Studio (gratuito) o el software de tu receptor.

**Opción B (PPP en línea):**

1. Sube el RINEX de la base (4 horas o más) al servicio PPP de INEGI, si está disponible, o al CSRS-PPP de NRCan (Canadá).
2. Si el resultado sale en ITRF2020 / época actual, **transfórmalo a ITRF2008 época 2010.0** con la herramienta de transformación de INEGI.

**Aplicar el desplazamiento:**

1. Calcula la diferencia entre la coordenada definitiva y la provisional de la base: ΔN, ΔE, Δh.
2. Suma ese desplazamiento a todos los puntos medidos con el rover ese día (en una hoja de cálculo o con la función de *localización/shift* de tu software).
3. Documenta los valores en la memoria técnica.

## 8.2 Alturas
- Convierte las alturas elipsoidales (h) en ortométricas (H) con el modelo geoidal de INEGI: H = h − N.
- En una manzana pequeña N es prácticamente constante, así que basta un solo valor de N para todo el sector.

## 8.3 Procesamiento en WebODM
1. Crea el proyecto y carga las fotos de ambas pasadas.
2. **Archivo de puntos de control** (`gcp_list.txt`). La primera línea indica la proyección y cada línea siguiente es una observación:
   ```
   EPSG:6369
   512634.218 2157812.412 2245.310 2010 1504 DJI_0123.JPG GCP01
   ```
   (Este, Norte, altura, píxel x, píxel y, foto, nombre). Marca cada punto de control en 3 a 6 fotos usando la interfaz de GCP de WebODM. **No incluyas los CHK.**
3. Opciones recomendadas:
   - `dsm: true`, `dtm: true`
   - `dem-resolution: 5` (cm), `orthophoto-resolution: 2` (cm)
   - `rolling-shutter: true`
   - `feature-quality: high`, `pc-quality: high`
   - `pc-classify: true` (ayuda a separar el terreno de construcciones y árboles para el DTM)
4. Exporta: ortofoto (GeoTIFF), DSM, DTM, nube de puntos (LAZ) y el reporte de calidad.

## 8.4 Control de calidad (obligatorio)
- Sobre la ortofoto y el DTM, mide las coordenadas de los puntos CHK y compáralas con las medidas por GNSS.
- Calcula el RMSE en planta y en altura y anótalo en la memoria técnica.
- **Criterio interno sugerido:** 5 cm o menos en planta y 8 cm o menos en altura. Si no se cumple, revisa el marcado de los puntos de control o agrega más. **[VERIFICAR]** la tolerancia oficial del manual.
- Las **coordenadas de los vértices de lotes salen del GNSS**, no de la ortofoto. La ortofoto sirve para dibujar construcciones, vialidades y vértices que no se pudieron ocupar (dejándolo anotado).

## 8.5 Curvas de nivel
- En QGIS: *Ráster → Extracción → Curvas de nivel* sobre el **DTM**, con un intervalo de 0.50 m (o 1.00 m si el terreno es plano). Las maestras se ponen cada 5 curvas.
- Suaviza ligeramente (*Vectorial → Geometría → Suavizar*) y revisa que no aparezcan "curvas fantasma" sobre azoteas.

## 8.6 Dibujo del plano por lote
1. Importa los vértices (CSV) en QGIS o AutoCAD y une el polígono del lote.
2. Captura los vértices en la hoja **Vertices** de `Plantilla_Cuadro_de_Construccion.xlsx`. La plantilla calcula rumbos, distancias, superficie y perímetro.
3. Compara la superficie de la plantilla con la del CAD/QGIS; deben coincidir.
4. Digitaliza las construcciones sobre la ortofoto. Indica niveles y m² construidos por nivel (lo que no se ve desde el aire se toma en sitio).
5. **Contenido mínimo sugerido del plano** **[VERIFICAR contra el formato del manual]:**
   - Cuadro de construcción (EST–PV, rumbo, distancia, V, coordenadas Y, X)
   - Superficie del terreno y superficie construida
   - Medidas y colindancias por orientación (Norte, Sur, Oriente, Poniente)
   - Croquis de localización con calles y referencias
   - Norte, escala gráfica y numérica, y curvas de nivel
   - Clave catastral, propietario o poseedor y ubicación
   - Sistema de referencia y proyección, y equipo y método empleados
   - Fecha, nombre, cédula profesional y firma del técnico; sello o visto bueno del ayuntamiento

# 9. Entregables por lote
1. Plano catastral en PDF firmado y en DWG/DXF y SHP.
2. Cuadro de construcción en XLSX/PDF.
3. Archivo CSV de vértices en ITRF2008 / UTM 14N.
4. Acta o croquis de colindancias firmado.
5. Memoria técnica del sector (una por manzana): equipo, base y su cálculo, puntos de control, RMSE de los CHK, fecha y responsables.

# 10. Rendimiento estimado (manzana de unos 30 lotes)
| Actividad | Tiempo |
|---|---|
| Instalar base y dianas | 1 h |
| Vuelo (2 pasadas) | 30–45 min |
| Puntos de control y verificación | 45 min |
| Vértices con colindantes | 6–10 min por lote → 3–5 h |
| Procesamiento WebODM | 2–6 h (desatendido) |
| Dibujo y plano por lote | 20–40 min por lote |

Con este método un equipo de 2 personas puede levantar en campo una manzana completa por jornada. El factor que más limita es la coordinación con los colindantes.

# 11. Errores frecuentes
- Medir vértices con solución FLOAT y no darse cuenta.
- Olvidar o medir mal la altura de antena de la base, lo que mete un error vertical en todo el sector.
- Mezclar puntos de días distintos que tienen correcciones de base diferentes.
- Marcar la diana del punto de control en la orilla y no en el centro.
- Tomar la parte de arriba de la barda en la ortofoto como si fuera el lindero.
- No dejar puntos de verificación: sin ellos no puedes demostrar la precisión.
