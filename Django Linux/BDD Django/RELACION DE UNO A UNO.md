
---

## ✅ 1. Modelo `Place`

```python
class Place(models.Model):
    name = models.CharField(max_length=50)
    address = models.CharField(max_length=80)

    def __str__(self):
        return f"{self.name} the place"
```

### 🔍 Qué representa:

- Es un **lugar físico**.
- Tiene campos de texto para el nombre (`name`) y dirección (`address`).
- El método `__str__` devuelve una representación como `"Nombre the place"`, útil para el admin y el shell de Django.

---

## ✅ 2. Modelo `Restaurant`

```python
class Restaurant(models.Model):
    place = models.OneToOneField(
        Place,
        on_delete=models.CASCADE,
        primary_key=True,
    )
    serves_hot_dogs = models.BooleanField(default=False)
    serves_pizza = models.BooleanField(default=False)

    def __str__(self):
        return "%s the restaurant" % self.place.name
```

### 🔍 Qué representa:

- Un **restaurante**, que **ocupa un lugar específico** (relación uno a uno con `Place`).

### 📌 Detalles clave:

- `OneToOneField` → Relación **1:1** con `Place`.  
    Es decir: **un lugar = un restaurante** (y viceversa).
- `primary_key=True` → Usa el campo `place_id` como clave primaria del restaurante.  
    Esto significa que el restaurante **comparte la misma clave primaria** que el `Place` relacionado.
- `serves_hot_dogs` y `serves_pizza` → Campos booleanos que indican si el restaurante sirve esos alimentos.

📌 `__str__` devuelve:

```python
"%s the restaurant" % self.place.name
```

Ejemplo: `"Pizza Hut the restaurant"`

---

## ✅ 3. Modelo `Waiter`

```python
class Waiter(models.Model):
    restaurant = models.ForeignKey(Restaurant, on_delete=models.CASCADE)
    name = models.CharField(max_length=50)

    def __str__(self):
        return "%s the waiter at %s" % (self.name, self.restaurant)
```

### 🔍 Qué representa:

- Un **mesero** que trabaja en un restaurante.

### 📌 Detalles clave:

- `ForeignKey(Restaurant)` → Relación **muchos a uno**:
    - Muchos meseros pueden trabajar en un mismo restaurante.
    - Pero cada mesero solo pertenece a **un** restaurante.
- `on_delete=models.CASCADE` → Si se elimina el restaurante, también se eliminan los meseros relacionados.
- `__str__` devuelve algo como:  
    `"Juan the waiter at Pizza Hut the restaurant"`

---

## 🔁 Relación entre modelos (resumen)

- **Place ↔️ Restaurant**:  
    `OneToOne` (un lugar es exactamente un restaurante).
    
- **Restaurant ↔️ Waiter**:  
    `ForeignKey` (un restaurante tiene muchos meseros).
    

---

## 📌 ¿Qué puedes hacer en el shell?

```python
# Crear un lugar
p = Place.objects.create(name="La Pizzería", address="Calle 123")

# Crear un restaurante en ese lugar
r = Restaurant.objects.create(place=p, serves_hot_dogs=False, serves_pizza=True)

# Crear un mesero
w = Waiter.objects.create(name="Carlos", restaurant=r)

# Ver representación
print(w)  # Carlos the waiter at La Pizzería the restaurant
```

---

