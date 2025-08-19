
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



## 💡 Reflexión final  
Con este proyecto aprendí que las **expresiones regulares** no son solo para buscar textos, también son súper útiles para:  
- Validar datos (códigos, correos, teléfonos).  
- Segmentar clientes por ciudades o dominios de correo.  
- Analizar reseñas con hashtags, emojis o palabras clave.  

