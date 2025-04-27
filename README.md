# proyecto-grupo2-momento1

Rastreador de Gastos Personales
Vamos a desarrollar una aplicación de consola para gestionar gastos personales, siguiendo los pasos solicitados.
Momento 1
1. Definición de Requerimientos
Entradas:
•	Monto del gasto (valor numérico)
•	Categoría del gasto (alimentación, transporte, ocio, hogar, salud, educación, otros)
•	Fecha del gasto (día/mes/año)
•	Descripción del gasto (opcional)
Reportes:
•	Resumen mensual de gastos por categoría
•	Gasto total del mes
•	Gasto promedio diario
•	Listado de gastos por categoría
•	Identificación del día con mayor gasto
•	Comparativa con meses anteriores


•	2. Pseudocódigo
Para registrar un gasto:
FUNCIÓN registrarGasto()
    MOSTRAR "--- Registro de Nuevo Gasto ---"
    
    SOLICITAR monto
    MIENTRAS monto <= 0 HACER
        MOSTRAR "El monto debe ser mayor que cero"
        SOLICITAR monto
    FIN MIENTRAS
    
    MOSTRAR "Categorías disponibles:"
    MOSTRAR lista de categorías numeradas
    SOLICITAR opciónCategoría
    MIENTRAS opciónCategoría fuera de rango HACER
        MOSTRAR "Categoría inválida"
        SOLICITAR opciónCategoría
    FIN MIENTRAS
    categoría = obtenerCategoríaPorOpción(opciónCategoría)
    
    SOLICITAR fecha
    MIENTRAS fecha inválida HACER
        MOSTRAR "Formato de fecha incorrecto (DD/MM/AAAA)"
        SOLICITAR fecha
    FIN MIENTRAS
    
    SOLICITAR descripción
    
    nuevoGasto = CREAR Gasto(monto, categoría, fecha, descripción)
    usuario.agregarGasto(nuevoGasto)
    
    MOSTRAR "Gasto registrado correctamente"
FIN FUNCIÓN
Para generar resumen mensual:
FUNCIÓN generarResumenMensual(mes, año)
    MOSTRAR "--- Resumen Mensual: " + mes + "/" + año + " ---"
    
    gastosDelMes = usuario.obtenerGastosPorMes(mes, año)
    
    SI gastosDelMes está vacío ENTONCES
        MOSTRAR "No hay gastos registrados para este mes"
        RETORNAR
    FIN SI
    
    gastoTotal = 0
    gastosPorCategoría = {} // diccionario vacío
    
    PARA CADA gasto EN gastosDelMes HACER
        gastoTotal = gastoTotal + gasto.monto
        
        SI gastosPorCategoría contiene gasto.categoría ENTONCES
            gastosPorCategoría[gasto.categoría] = gastosPorCategoría[gasto.categoría] + gasto.monto
        SINO
            gastosPorCategoría[gasto.categoría] = gasto.monto
        FIN SI
    FIN PARA
    
    MOSTRAR "Gasto total del mes: $" + gastoTotal
    
    díasEnMes = obtenerDíasEnMes(mes, año)
    gastoPromedioDiario = gastoTotal / díasEnMes
    MOSTRAR "Gasto promedio diario: $" + gastoPromedioDiario
    
    MOSTRAR "Desglose por categoría:"
    PARA CADA categoría, monto EN gastosPorCategoría HACER
        porcentaje = (monto / gastoTotal) * 100
        MOSTRAR categoría + ": $" + monto + " (" + porcentaje + "%)"
    FIN PARA
    
    díaMayorGasto = encontrarDíaMayorGasto(gastosDelMes)
    MOSTRAR "Día con mayor gasto: " + díaMayorGasto.fecha + " - $" + díaMayorGasto.monto
FIN FUNCIÓN


3. Diagrama de clases UML: Gasto, Categoría, Reporte, Usuario.

   gasto: tiene descripcion, monto y fecha
   categoria: tendria el nombre de "libros"
   reporte: debe llevar los gatos, la fecha de los gastos y la descripcion del gasto
   usuario: debe ir guardado en una base de datos, lleva nombre, email
