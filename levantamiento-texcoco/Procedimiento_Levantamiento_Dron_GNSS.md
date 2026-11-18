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

# 1-bis. Fundamento en el Manual Catastral 2024 (IGECEM)
Fuente: Gaceta del Gobierno, 29 de mayo de 2024, Sección Segunda, No. 95. Abroga el manual de 2014.

- **LT014. Quién puede levantar:** la persona debe estar **certificada en la NICL "Funciones del Proceso Catastral"** por la Comisión Certificadora de Competencia Laboral **e inscrita en el padrón de especialistas en levantamiento topográfico catastral del IGECEM**. La acreditación del ayuntamiento **no basta**: tramita ambas cosas antes de firmar planos.
- **LT020 y III.1.4.2-I. Cuándo se exige instrumento de precisión:** predios mayores de 2,000 m², topografía accidentada, configuración muy irregular o **cuando no exista cartografía** en la cual apoyarse. Los predios menores de 2,000 m² se pueden medir con cinta apoyándose en cartografía 1:500 o 1:1000. En ex-parcelas sin cartografía, el método de precisión es el que corresponde, y además es el más defendible.
- **III.1.4.2-XVII. Métodos admitidos para linderos:** **geodésico-topográfico, fotogramétrico o su combinación.** GNSS más dron está expresamente previsto.
- **LT019. Vértices de común acuerdo:** se ubican en presencia del solicitante y los colindantes, sobre los puntos que **de común acuerdo** señalen. Si los vértices son desconocidos, **se suspende la diligencia**: no se replantea.
- **LT006. Limitación legal:** los resultados del levantamiento topográfico catastral *"sólo se podrán utilizar para trámites administrativos"*. Ver la sección 12 por sus efectos en el juicio de usucapión.

# 2. Marco de referencia

| Concepto | Valor |
|---|---|
| Marco geodésico | ITRF2008, época 2010.0 (oficial INEGI) |
| Liga | Red Geodésica Nacional Activa (RGNA) de INEGI |
| Proyección | UTM zona 14 Norte (código EPSG:6369, *México ITRF2008 / UTM 14N*) |
| Alturas | Ortométricas, convertidas con el modelo geoidal de INEGI (GGM10 o el vigente) |
| Unidades | metros, 3 decimales en coordenadas y distancias |

**Manual III.1.4.2-XI y XV:** los trabajos deben estar **ligados al sistema geodésico de referencia oficial** (RGNA o RGNP, o red local ligada a ellas). Las alturas GPS se convierten a **ortométricas con el modelo geoidal** vigente, según la Norma Técnica para el Sistema Geodésico Nacional. El manual remite a esa norma de INEGI, que fija el marco oficial (ITRF2008 época 2010.0). Si el catastro municipal todavía trabaja en ITRF92 o en coordenadas locales, pide sus parámetros de transformación.

# 3. Equipo y materiales (lista de revisión)

**GNSS**

- [ ] **Dos receptores GNSS de doble frecuencia** (Manual XIV), base y rover, con antena, tripié y base nivelante o bastón con bípode
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
- [ ] Clavos de acero tipo *PK* o varilla con tapón y pintura para marcar los vértices de los predios
- [ ] Para la línea de control: **2 monumentos de concreto con placa metálica** (ver 5.1) y formato *Cédula de Estaciones de Control Geodésico*
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
6. **Aviso a vecinos y colindantes:** el ayuntamiento debe citar a propietarios y colindantes para el día del levantamiento, porque los vértices se marcan **en presencia de ambos colindantes**. Usa los formatos anexos del Manual 2024: notificación, citatorio y relación de colindantes.

# 4-bis. Expediente previo por predio (NICL de 2022)
Antes de programar la diligencia, el expediente de cada lote debe contener:
- [ ] **Solicitud por escrito** del servicio, en el formato anexo del Manual Catastral vigente
- [ ] **Identificación oficial vigente** del propietario o poseedor (o de la persona autorizada)
- [ ] **Documento que acredite la propiedad o posesión** (contrato privado, constancia ejidal, título, etc., según el manual)
- [ ] **Comprobante del pago predial** o certificación de clave catastral
- [ ] **Relación actualizada de colindantes** con nombres y domicilios (de aquí salen los nombres que van en el plano y los citatorios)
- [ ] **Croquis de localización** del inmueble
- [ ] **Recibo de pago** del servicio
- [ ] Registro en el **Control de Levantamientos Topográficos Catastrales**: número progresivo, folio de la orden de trabajo y fecha de ejecución notificada

Para el programa de regularización, propón al ayuntamiento recibir y revisar los expedientes **por manzana completa** antes del día de campo.

# 5. Control geodésico y base GNSS (Manual III.1.4.2, XI a XVI)

## 5.1 Línea de control acimutal y lineal (una vez por sector o colonia)
El manual pide ligarse a la RGNA mediante **estaciones GPS de control** (opción XI-c):

1. **Dos vértices de control** separados **al menos 500 m**, de preferencia **intervisibles** (XII). Elígelos en lugares despejados y seguros (camellones, plazas, bordes de banqueta) que cubran la colonia.
2. **Monumentación (XIII):**
   - Bloque de concreto de 40 × 40 cm en planta y 40 cm de alto (50 × 50 × 60 cm en terreno blando), sobre una cama de arena de 15 cm, con **varilla testigo** de ½" alineada al centro.
   - **Placa de aluminio** con la leyenda "ESTADO DE MÉXICO", municipio, institución, siglas CAT, número de vértice y fecha. En zona urbana la placa queda **al ras**.
   - Llena la **Cédula de Estaciones de Control Geodésico**: croquis, itinerario para llegar, descripción del entorno, coordenadas y datos técnicos.
3. **Observación (XIV):**
   - **Método estático**, con los dos receptores **observando al mismo tiempo**, uno en cada vértice.
   - Equipo de **doble frecuencia**, **4 satélites como mínimo**, **máscara de elevación de 10°** e **intervalo de registro de 15 s**.
   - Duración según la distancia a la estación RGNA: **60 min si está a menos de 100 km** (Texcoco cumple). Se recomienda observar 2 horas para tener margen.
   - El manual permite receptores de **una sola frecuencia** solo a menos de 40 km de la RGNA. Los ZED-F9P, Emlid y los receptores chinos de gama media son de doble frecuencia.
4. **Posproceso (XI-c y XXI):**
   - Procesa las líneas base RGNA → V1, RGNA → V2 y V1 → V2 en **tiempos comunes**.
   - Haz un **ajuste por mínimos cuadrados**. Usa el software de posproceso de la marca de tu receptor con ajuste de red, o equivalente; con dos estaciones RGNA el ajuste es más robusto.
   - **Exactitud exigida:** CEP95 ≤ **0.10 m** para los vértices de control GPS (XIX).
5. Conserva los archivos crudos, los RINEX de la RGNA, el reporte de procesamiento y el de ajuste. Forman parte de la memoria técnica.

## 5.2 Base RTK del día (propagación de coordenadas, XVI)
1. Instala la base **sobre uno de los vértices de control**, con su coordenada ajustada ya capturada. Centra, nivela y anota la **altura de antena** y cómo la mediste.
2. **Comprobación al inicio y al final de la jornada:** mide con el rover el **otro vértice de control**. La diferencia con su coordenada ajustada debe ser de 3 cm o menos. Esto sirve como liga y como comprobación de orientación.
3. Deja la base **registrando datos crudos** toda la jornada; así puedes reprocesar puntos dudosos (PPK).
4. **Antes de tener la línea de control ajustada** (primera visita), puedes iniciar con una coordenada provisional de la base. Al final, aplica el desplazamiento según 8.1.

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

## 7.3 Diligencia y acta circunstanciada (según la NICL de 2022)
En cada predio, y en este orden:
1. **Antes de medir**, explica a todos los presentes los **alcances administrativos y las limitaciones legales** del levantamiento y en qué consisten los trabajos. Conviene decir que el levantamiento catastral **no otorga ni resuelve propiedad**.
2. **Verifica que los colindantes presentes acrediten** su propiedad o posesión con un documento y una identificación oficial.
3. **Localiza los vértices limítrofes que, de común acuerdo, indiquen el solicitante y los colindantes** (LT019).
   - Si **no se conocen** los vértices, **suspende la diligencia** y anótalo en el acta. **No replantees.**
   - Si hay **desacuerdo**, no midas ese lindero como si estuviera acordado. Asienta en el acta las manifestaciones de cada parte y consulta con el director de catastro si procede suspender o reprogramar.
4. Mide (GNSS o cinta) y **registra los datos en papel** durante la diligencia, en libreta o croquis de campo, aunque el equipo guarde los datos digitalmente.
5. **Llena el acta circunstanciada** con:
   - el folio consecutivo del *Control de Levantamientos*;
   - el nombre del solicitante, cotejado con la solicitud;
   - los fundamentos legales;
   - la fecha de la solicitud o notificación;
   - el desarrollo de la diligencia, los resultados y los incidentes;
   - las **manifestaciones de los colindantes**;
   - el domicilio de la oficina de catastro donde se consultan los resultados;
   - los nombres y **firmas** de todos los que intervinieron.
6. **Lee el acta en voz alta** ante los presentes antes de que la firmen.

**Croquis de campo** (para cada predio, según la NICL): clave catastral, responsable asignado por orden de trabajo, fecha, distancias medidas, orientación al norte magnético como referencia, colindancias según la relación del solicitante, ubicación según el documento de propiedad y notas aclaratorias.

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

## 8.4 Control de calidad: tolerancias oficiales del Manual 2024 (CEP95)
| Elemento | Exactitud exigida | Referencia | Lo esperable con este método |
|---|---|---|---|
| Vértices de control GPS | ≤ 0.10 m | XIX | 1–2 cm |
| Vértices de apoyo | ≤ 0.20 m | XIX | 1–3 cm |
| **Vértices prediales**, horizontal | **≤ 0.30 m** | XX | 1–3 cm (RTK) |
| Vértices prediales, vertical | < 0.50 m | XX | 2–5 cm |
| Puntos de control fotogramétrico (vuelo < 1:5,000) | ≤ 0.10 m | XXIV | 1–3 cm |
| Imagen para predios **urbanos**: tamaño de píxel | ≤ 0.20 m | XXVI | ≈ 0.02 m (Mini 3 a 60 m) |
| Imagen para predios urbanos: exactitud | < 0.40 m | XXVII | 3–5 cm con puntos de control |

- Sobre la ortofoto, mide los puntos de verificación (CHK) y compáralos con las coordenadas GNSS. Calcula el RMSE y el **CEP95 ≈ 2.45 × RMSE por eje** (aproximación cuando los errores en X e Y son parecidos). Anótalo en la memoria técnica.
- **Criterio interno**, mucho más estricto que el oficial: 5 cm o menos en planta y 8 cm o menos en altura. Así te queda margen frente a cualquier perito.
- Los **vértices prediales salen del GNSS** (método geodésico-topográfico). Los tomados de la ortofoto solo se usan si el vértice es **fotoidentificable** (XXII), y se integran a los datos GNSS (XXVIII). En la tabla de vértices anota qué método se usó para cada uno.
- Para comparar: Google Earth no garantiza ni el tamaño de píxel ni la exactitud de XXVI y XXVII para predios urbanos.

## 8.5 Curvas de nivel
- En QGIS: *Ráster → Extracción → Curvas de nivel* sobre el **DTM**, con un intervalo de 0.50 m (o 1.00 m si el terreno es plano). Las maestras se ponen cada 5 curvas.
- Suaviza ligeramente (*Vectorial → Geometría → Suavizar*) y revisa que no aparezcan "curvas fantasma" sobre azoteas.

## 8.6 Dibujo del plano por lote
1. Importa los vértices (CSV) en QGIS o AutoCAD y une el polígono del lote.
2. Captura los vértices en la hoja **Vertices** de `Plantilla_Cuadro_de_Construccion.xlsx`. La plantilla calcula rumbos, distancias, superficie y perímetro.
3. Compara la superficie de la plantilla con la del CAD/QGIS; deben coincidir.
4. Digitaliza las construcciones sobre la ortofoto. Indica niveles y m² construidos por nivel (lo que no se ve desde el aire se toma en sitio).
5. **Contenido obligatorio del plano (Manual LT025 y LT026, igual para plano analógico y digital):**
   - a) Imagen institucional de la autoridad catastral
   - b) Nombre del propietario
   - c) Clave catastral
   - d) Ubicación (calle y número oficial)
   - e) Croquis de localización
   - f) Nombre del municipio
   - g) **Superficie en m² con aproximación a centímetros**
   - h) **Medidas de las colindancias en metros con aproximación a centímetros**
   - i) Puntos de inflexión o radiaciones
   - j) Orientación del dibujo hacia el norte, con simbología convencional
   - k) **Cuadro de construcción congruente con un sistema específico de coordenadas** (lo genera la plantilla)
   - l) Nombres de los colindantes y, en su caso, de las vialidades
   - m) Fecha en que se hizo el levantamiento
   - n) Escala gráfica en metros
   - o) Folio del acta
   - p) Nombres y firmas de los responsables del **levantamiento**, del **cálculo** y de la **autorización**
   - q) Sello de la autoridad catastral
   - r) **Método de medición: "con aparatos de precisión"**. Detállalo así: *GNSS ligado a la RGNA y fotogrametría con puntos de control (Manual III.1.4.2-XVII)*.
   - Opcionales (LT026): croquis de aproximación con las vialidades limítrofes, fundamento legal y folio del recibo de pago.

6. **Formato de dibujo (Manual III.1.4.3):**
   - **Hoja de 95 × 70 cm** orientada al norte, con el lado largo de oeste a este. Márgenes: 5 cm arriba y abajo, 3 cm a la izquierda y 2 cm a la derecha.
   - **Cuadrícula de 10 × 10 cm** con cruces de 0.5 cm y coordenadas (X, Y) anotadas en el margen.
   - **Escala 1:500 o 1:1000**, según la de los planos catastrales del municipio. Elígela con las coordenadas máximas y mínimas para que el predio quede bien acomodado.
   - Vértices encerrados en un **círculo pequeño y numerados**. Distancias entre vértices al centímetro, y **superficie al centro del predio**.
   - **Tira marginal** con el título "Levantamiento topográfico", propietario, ubicación, municipio, escala, superficie, nombres de quienes hicieron el levantamiento, el cálculo y el dibujo, y la fecha (día/mes/año).
   - En zonas urbanas, identifica el predio con su clave catastral para actualizar la cartografía (punto 13).

   Recomendación adicional para el juicio: incluye también las medidas y colindancias en formato registral y la ubicación del lote dentro de la parcela matriz (sección 12).

   **Redondeo:** las coordenadas van con 3 decimales; las distancias y la superficie del plano, con 2 (centímetros). La superficie se calcula **con las coordenadas** completas y se redondea al final. Usa **las mismas cifras** en el plano, el acta y la demanda.

# 9. Entregables por lote
1. Plano catastral en PDF firmado y en DWG/DXF y SHP.
2. Cuadro de construcción en XLSX/PDF.
3. Archivo CSV de vértices en ITRF2008 / UTM 14N.
4. Acta o croquis de colindancias firmado.
5. Memoria técnica del sector (una por manzana): equipo, base y su cálculo, puntos de control, RMSE de los CHK, fecha y responsables.
6. Para juicio de usucapión: plano de conjunto de la parcela matriz, medidas y colindancias en formato registral, tabla de comparación contra el contrato y respaldo de los datos crudos (ver sección 12).

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

# 12. Uso de los planos en juicio de usucapión

> Nota del director de catastro: los planos se presentarán como prueba en **juicios de usucapión**. Esto sube el nivel de exigencia, porque el plano deja de ser solo un trámite administrativo y pasa a ser **prueba pericial** que el juez y la contraparte pueden revisar. Los criterios de esta sección son técnicos; los jurídicos deben confirmarse con el abogado de cada caso.

## 12.0 Atención: limitación del manual (LT006)
El Manual 2024 dice que los resultados del levantamiento topográfico catastral *"sólo se podrán utilizar para trámites administrativos relacionados con el inmueble de que se trate"*. Por eso **el plano catastral oficial, con sello de catastro, puede ser objetado si se presenta solo como prueba en el juicio.**

**Solución recomendada, que debes confirmar con el abogado y con el director de catastro:**
- **Producto 1. Plano catastral oficial** (formato LT025, sello de catastro), para el padrón y los trámites administrativos.
- **Producto 2. Plano topográfico y dictamen técnico** firmado por ti como **arquitecto con cédula**, con **los mismos datos**, para ofrecerse en el juicio como documental privada o como base de la **prueba pericial en topografía**.

Así los dos documentos se respaldan entre sí y ninguno se usa fuera de su alcance legal.

## 12.1 Por qué importa
En la usucapión el actor debe acreditar, entre otras cosas, la **identidad del inmueble**: que lo que posee es exactamente lo que demanda, y que forma parte del predio inscrito a nombre del demandado (el titular registral). Esa identidad normalmente se prueba con el plano topográfico y, si se ofrece, con la **pericial en topografía**.

## 12.2 Requisitos adicionales del levantamiento
1. **Ligar el lote al predio de mayor extensión (la parcela matriz):**
   - Consigue el título de dominio pleno, el plano de la parcela del RAN (PROCEDE/FANAR) y el certificado de inscripción del IFREM.
   - Levanta o reconstruye el **polígono de la parcela completa** y muestra cada lote **dentro** de ella.
   - Los planos del RAN suelen estar en ITRF92: transfórmalos a ITRF2008 antes de compararlos y documenta la transformación.
2. **Plano de conjunto por parcela** con todos los lotes, las calles y una tabla de superficies: lotes más vialidades más remanente igual a la superficie de la parcela. Es la mejor prueba de que la fracción pertenece al predio inscrito.
3. **Medidas y colindancias en formato registral**, además del cuadro de construcción. Por ejemplo: *"Al Norte: 18.593 m con Calle Benito Juárez; al Oriente: …"*. Así el abogado las transcribe tal cual en la demanda.
4. **Tabla comparativa por lote:** medidas y superficie del **contrato privado** frente a las del **levantamiento**, con las diferencias. Las discrepancias que no se explican son un motivo común para que se niegue la acción o se pida aclarar la demanda.
5. **Colindantes con nombre completo** según la posesión actual, verificados en campo y firmados en el acta. Pueden servir como testigos.
6. **Evidencia que se pueda reproducir:** conservar los datos crudos GNSS, el RINEX de la base y de la RGNA, las fotos de los vértices con fecha, el reporte de WebODM, el RMSE de los puntos de verificación y las actas firmadas. Un perito de la contraparte debe poder repetir el cálculo.
7. **Memoria técnica firmada por lote** (o por sector, con un anexo por lote): método, equipo con número de serie, certificado de calibración si existe, marco de referencia, precisión obtenida y responsable.
8. Usar **los mismos datos** en el plano, la memoria, el cuadro y la demanda. Ninguna cifra debe variar entre documentos, ni siquiera por redondeo.

## 12.3 Tu papel como técnico
- Puedes ser llamado a **ratificar el plano o dictamen** ante el juzgado y a responder las preguntas de las partes. Ten a la mano la cédula profesional y la acreditación del ayuntamiento.
- Si el juzgado exige **perito registrado**, revisa los requisitos de la lista de peritos del Poder Judicial del Estado de México.
- Mantén la imparcialidad: el plano describe **lo que existe en campo**. Si un vecino no está de acuerdo con un lindero, anótalo como **lindero en conflicto**; no lo resuelvas en el dibujo.
- Define con el ayuntamiento y los interesados **quién paga y para quién trabajas** (ayuntamiento o particular). En un juicio la contraparte puede cuestionarlo.

## 12.4 Coordinar con el abogado o la defensoría antes de empezar
- El formato que espera el juzgado: tamaño del plano, escala, firmas y sellos.
- Si la demanda va contra el titular registral (el ejidatario que obtuvo el dominio pleno) y si hace falta acreditar la **causa generadora de la posesión** (contrato de compraventa o cesión). La fecha y las medidas del contrato deben ser congruentes con el plano.
- Qué pasa con las **calles**: siguen siendo parte de la parcela inscrita hasta que se donen o se municipalicen.

# 13. Referencias normativas
- **Manual Catastral del Estado de México**, Gaceta del Gobierno, 29 de mayo de 2024 (Sección Segunda, Tomo CCXVII, No. 95, pp. 4–177). Abroga el de 2014. Las secciones clave para este trabajo son:
  - III.1.3: políticas LT001 a LT030;
  - III.1.4.2: levantamiento con instrumentos de precisión;
  - III.1.4.3: dibujo;
  - III.2: verificación de linderos;
  - los anexos de formatos: solicitud, relación de colindantes, notificación, citatorio, acta, control y reporte.
- **NICL "Funciones del proceso catastral"**, IHAEM, Gaceta del Gobierno, 6 de julio de 2022. Es obligatoria según la política LT014.
- **INEGI:** Norma Técnica para el Sistema Geodésico Nacional, Norma Técnica de Estándares de Exactitud Posicional, y *Lineamientos y Especificaciones Técnicas para la Generación y Actualización de Información Geográfica* (citados en LT014 y III.1.4.2).
- Código Financiero del Estado de México y Municipios, Título Quinto "Del Catastro", y su Reglamento.
- Código Civil para el Estado de México.

Pendiente de revisar en el texto completo del manual: las políticas LT002 a LT030 que no se transcribieron, III.2 (verificación de linderos) y los formatos anexos.
