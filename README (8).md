
# 🧚‍♀️ Comily • Taller de Expresiones Regulares en MongoDB  

## ✨ Mi proyecto  
Este trabajo hace parte del **taller de expresiones regulares en MongoDB**.  
Elegí como temática **Comily**, mi tienda online de maquillaje y skincare, porque es algo que me inspira mucho y me encanta.  

Comily nació de la idea de **dos hermanas** que siempre soñamos con compartir la belleza desde un estilo **angelical, delicado y auténtico**.  
Más que cosméticos, queremos transmitir confianza, cuidado y ese brillo que cada persona tiene en su interior. 💖  

---

## 📂 Colecciones de mi base de datos  

Para organizar la tienda, creé varias colecciones:  

- **categorias** → tipos de productos (labios, ojos, skincare, etc.).  
- **productos** → todo el catálogo (nombre, marca, tonos, ingredientes, precio).  
- **usuarios** → clientes y también personas del equipo.  
- **cupones** → códigos de descuento y promociones.  
- **comentarios** → reseñas de los clientes (muchas con emojis y hashtags).  
- **pedidos** → compras realizadas con items, pagos y estado.  

Cada colección tiene más de 10 documentos, y en total la tienda quedó muy realista.  

---

## ⚙️ Cómo cargué los datos en MongoDB  

1. Guardé todos los archivos `.json` en una carpeta del proyecto.  
2. Abrí MongoDB (yo usé Compass, pero también se puede con terminal).  
3. Creé la base de datos con el nombre **comily**.  
4. Importé cada colección.  

Ejemplo de importación en terminal:  

```bash
mongoimport --db comily --collection categorias --file coleccion_categorias.json --jsonArray --drop
mongoimport --db comily --collection productos  --file coleccion_productos.json  --jsonArray --drop
mongoimport --db comily --collection usuarios   --file coleccion_usuarios.json   --jsonArray --drop
mongoimport --db comily --collection cupones    --file coleccion_cupones.json    --jsonArray --drop
mongoimport --db comily --collection comentarios --file coleccion_comentarios.json --jsonArray --drop
mongoimport --db comily --collection pedidos    --file coleccion_pedidos.json    --jsonArray --drop
```

En Compass fue parecido, solo que con el botón **IMPORT DATA** y seleccionando **JSON Array**.  

---

## 🔎 Consultas con expresiones regulares  

La parte central del taller fue practicar con `$regex`.  
En total realicé más de **25 consultas**, todas con un propósito real en la tienda.  
Aquí dejo algunas de las que más me gustaron:  

### 1. Buscar productos que empiecen con “Pro” (autocompletar)  
```js
db.productos.find({ "nombre": { "$regex": "^pro", "$options": "i" } })
```  
Sirve para que el buscador sugiera productos como “Protector solar”.  

---

### 2. Usuarios de Bucaramanga o Floridablanca  
```js
db.usuarios.find({ "ciudad": { "$regex": "^(buca|flori)", "$options": "i" } })
```  
Me permite segmentar clientes de esas ciudades.  

---

### 3. Comentarios con hashtags  
```js
db.comentarios.find({ "contenido": { "$regex": "#\\w+" } })
```  
Identifica reseñas donde los clientes usan hashtags como `#ComilyLover`.  

---

### 4. Validar el formato de SKU (`COM-####-###`)  
```js
db.productos.find({ "codigo_sku": { "$regex": "^COM-\\d{4}-\\d{3}$" } })
```  
Con esto reviso que los códigos de inventario estén correctos.  

---

### 5. Buscar cupones que empiecen con “PRO” o “GLOW”  
```js
db.cupones.find({ "codigo": { "$regex": "^(PRO|GLOW)" } })
```  
Filtra promociones relacionadas con esas campañas.  

---

### 6. Productos con ingredientes populares de skincare  
```js
db.productos.find({ "ingredientes": { "$regex": "(ácido\\s+hialurónico|vitamina\\s*c|niacinamida)", "$options": "i" } })
```  
Me ayuda a encontrar rápido los productos más buscados por clientes.  

---

### 7. Pedidos con código tipo `CO-YYMM-####`  
```js
db.pedidos.find({ "codigo": { "$regex": "^CO-\\d{4}-\\d{4}$" } })
```  
Sirve para verificar que los pedidos sigan el formato correcto.  

---

## 💡 Reflexión final  
Con este proyecto aprendí que las **expresiones regulares** no son solo para buscar textos, también son súper útiles para:  
- Validar datos (códigos, correos, teléfonos).  
- Segmentar clientes por ciudades o dominios de correo.  
- Analizar reseñas con hashtags, emojis o palabras clave.  
- Mejorar la experiencia de búsqueda en una tienda online.  

Y lo más bonito es que pude unir algo que me apasiona, **la belleza y el maquillaje**, con la programación y las bases de datos. 🌸  


Ahora voy a poiner las consultas detalladamente

1.Autocompletar por prefijo ("Pro…")
![alt text](<Screenshot (21).png>)
Sugerencias en la barra de búsqueda.

2.Productos con etiquetas “vegano” o “sin parabenos”
![alt text](image.png)
Filtro rápido de cosmética más limpia.

3.SKU con formato COM-####-###
![alt text](image-1.png)
Validación/diagnóstico de integridad de catálogo.

4.Código de barras entre 8 y 13 dígitos
![alt text](image-3.png)
Detección de EAN potencialmente válidos.

5.Marcas que contengan 'pro' (p. ej., "Comily Pro", "ProXa")
![alt text](image-4.png)
Campañas por línea “pro”.

6.Descripción que mencione “resistente al agua” u “oil-free”
![alt text](image-5.png)
Comunicar beneficios específicos.

7.Usuarios del dominio corporativo @mi.comily.co
![alt text](image-6.png)
Usuarios del dominio corporativo @mi.comily.co

8.Usuarios cuyo nombre o apellido empiecen por “Ca”
![alt text](image-7.png)
Búsqueda rápida en CRM.

9.Teléfonos con indicativo +57 y operador 300–399
![alt text](image-8.png)
Verificar formato local de contacto.

10.Usuarios de Bucaramanga/Floridablanca (inicio por “Buca|Flori”)
![alt text](image-9.png)
Segmentación geográfica para campañas.

11.Comentarios con hashtags (#ComilyLover)
![alt text](image-11.png)
Detección de UGC aprovechable en marketing.

12.Comentarios con check o emoticonios (caracteres Unicode)
13.Comentarios que contengan “defectuoso|golpead”
14.Productos “Protector Solar … SPF(\s)\d+”*
15.Productos con tonos “Rosa|Coral|Durazno|Vino”
16.Slugs con guiones (ver URL amigables)
17.Ingredientes que incluyan “ácido hialurónico|niacinamida|vitamina C”
18.Cupones activos cuyo código empiece por “PRO|GLOW”
19.Cupones con descripción que mencione “promocional|descuento”
20.Pedidos con código tipo CO-YYMM-####
21.Pedidos con ciudad de envío que termine en “-manga” o “-lanca”
22.Métodos de pago PSE o tarjeta (insensible a mayúsculas)
23.Productos en rebaja o con etiqueta “oferta|rebaja” en etiquetas
24.Usuarios que aceptaron marketing (correo de Gmail)
25.Productos “Comily Pro …” o marca exacta “Comily Pro”