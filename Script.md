const gastos = []; /* se crea un conjunto vacio para guardar los gastos */

function agregarGasto() { /* aqui la funcion para agregar los gastos */
  const fecha = document.getElementById("fecha").value; /* se obtiene el valor del input fecha */
  const detalle = document.getElementById("detalle").value; /* se obtiene el valor del input detalle */
  const monto = parseFloat(document.getElementById("monto").value); /* se obtiene el valor del input monto y se convierte a numero */

  if (!fecha || !detalle || isNaN(monto)) { /* aqui se valida que los campos no esten vacios y que el monto sea un numero */
    alert("Por favor completa todos los campos.");
    return;
  }

  gastos.push({ fecha, detalle, monto }); /* se agrega el gasto al conjunto de gastos */
  mostrarGastos(); /* se muestra la lista de gastos */
  calcularTotalMes(); /* se recalcula el total de gastos del mes */
}

function mostrarGastos() {  /* aqui la funcion para mostrar los gastos */
  const lista = document.getElementById("listaGastos"); /* se obtiene el elemento listaGastos */
  lista.innerHTML = ""; /* se vacia el contenido de la lista */
  gastos.forEach(g => { /* se recorre el conjunto de gastos */
    const item = document.createElement("li"); /* se crea un elemento li  el elemento li es un elemento de lista */
    item.textContent = `${g.fecha} - ${g.detalle}: $${g.monto.toFixed(2)}`; /* se agrega el contenido al elemento li */
    lista.appendChild(item); /* se agrega el elemento li a la lista */
  });
}

function calcularTotalMes() { /* aqui la funcion para calcular el total de gastos del mes */
  const mesActual = new Date().getMonth(); /* se obtiene el mes actual */
  const total = gastos /* se filtran los gastos del mes actual */
    .filter(g => new Date(g.fecha).getMonth() === mesActual) 
    .reduce((sum, g) => sum + g.monto, 0); /* se suma el monto de cada gasto */
  document.getElementById("totalMes").textContent = `$${total.toFixed(2)}`; /* se muestra el total en el elemento totalMes */
}
