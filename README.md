## BIPI - FRONT
Deberá crear un proyecto nuevo en Vue.js + SASS haciendo uso de los datos dentro del fichero `vehicles.json` y usando como guía de estilo las pantallas según los mockups proporcionados [Mobile](https://projects.invisionapp.com/prototype/test-frontend-mobile-ckhc4fvd8015094015hbigyr8/play/75dffa67). El proyecto tiene que incluir:

- Una vista catálogo donde se mostrarán todos los vehículos disponibles.
- En la vista del catálogo se deben añadir unos filtro/s de vehículos en base a los campos que parezcan óptimos para ello. Esta parte no está en el diseño así que sientete libre de añadir los filtros como creas conveniente.
- Al pulsar sobre cada vehículo llevará a la vista de detalle.
- Una vista de "Últimos coches visitados". Esta vista será igual que la del catálogo pero solo aparecerá los últimos 5 vehículos por los que hemos pasado.

### Códigos promocionales

Tendremos otro fichero con un listado de posibles códigos promocionales aplicables al vehículo. `promocodes.json`

```
[
  {
    "_id": "5f77173b76b9921886a8315a",
    "code": "FIAT50",
    "discount": 50,
    "type": "PERCENTAGE",
    "vehicles": ["8374f746-5670-472a-9bc3-a1af886d749c"]
  },
  {
    "_id": "5f77173976b9921886a83159",
    "code": "MERCEDES100",
    "discount": 100,
    "type": "CREDIT",
    "vehicles": ["06576ae0-3bd4-487b-bd4e-c4e246b13d04"]
  },
  {
    "_id": "5f77173976b9921886a83159",
    "code": "ALL10",
    "discount": 10,
    "type": "PERCENTAGE",
    "vehicles": []
  }
]
```
Tendremos 2 tipos de códigos promocionales:
- `PERCENTAGE`: se tomará el valor de `discount` como un porcentaje, si fuera 10, restaríamos al precio del vehículo un 10%.
- `CREDIT`: se tomará el valor de `discount` como un valor absoluto, si fuera 10, restaríamos 10€ al precio del vehículo.

La propiedad `vehicles` define a qué vehículos se puede aplicar cada código, será un array con los ids de los vehículos. ⚠️ En caso de no tener ninguno se podrá aplicar a todos.

En la vista del detalle Tendremos un desplegable como muetra el diseño con el precio desglosado que deberemos calcularlo con los datos que tenemos en el vehículo

- `Precio` Mostraremos el precio base del vehículo
- `Descuento` en caso que el vehículo esté en oferta se mostrará cuánto descuento se le aplica
- `Código promocional`, en caso de haber introducido un código el descuento total que aplica ese código
- `Precio total`, el precio total resultante con descuentos incluidos.

El código promocional puede venir en la url como un query param `?CODE="ALL10"` o podrá introducirse en el input del promocode. Si se introduce en el input tendremos que sincronizarlo con la url añadiendo ese parámetro query.

Si tenemos un código aplicado correcto debe desaparecer el componente del input de añadir código y en su lugar aparecerá un componente indicando el código y el descuento total.

⚠️ En el precio total debemos calcular el precio que resultaría con el código promocional aplicado. Ten en cuenta que en caso de estar en oferta, el descuento del código promocional se debe aplicar sobre el precio de oferta

Se tendrá en cuenta:
- Arquitectura del proyecto.
- Ajuste del desarrollo con el diseño proporcionado.
- Aplicación de store(Vuex) para la gestión del estado y su planteamiento pensando en la escalabilidad (¿Y si además del fichero tuviéramos otro origen de datos? Patrón `repository`).
- Maquetación de la página en móvil.

### EXTRA 1:
- En la página de "Últimos coches visitados", mostrar los últimos vehículos visitados con la fecha que lo visitaste por orden de más recientes primero. Si cierras la página y la vuelves abrir deben seguir apareciendo esos vehículos y sus fechas. Además si visitas varias veces una misma página solo debe contar como una única visita actualizada a la fecha más reciente en que lo visitaste.

### EXTRA 2 - PARA NOTA:
- Crear una API en NODE + EXPRESSJS que devuelva los datos del fichero y haga uso de ella el front.

### EXTRA 3 - SOBRESALIENTE:
- Una vez teniendo el EXTRA 1, hacer que se conecte a una base de datos en MONGODB haciendo uso de MONGOOSE y ese sea el origen de datos de los vehículos, es decir, la base da datos deberá contener el listado de los vehículos, la api accederá a ellos y los devolverá al front.