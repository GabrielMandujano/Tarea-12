# Tarea-12
### EJERCICIO 1
DECLARE @fecha_inicio_2009 datetime = '2009-01-01';
DECLARE @fecha_fin_2009 datetime = '2009-12-31';

SELECT SUM(total) AS Total_Ventas 
FROM ve.documento 
WHERE fechaMovimiento BETWEEN @fecha_inicio_2009 AND @fecha_fin_2009;

### EJERCICIO 2
SELECT p.* 
FROM ma.persona p 
LEFT JOIN ma.personaDestino pd ON p.persona = pd.persona 
WHERE pd.persona IS NULL;

### EJERCICIO 3
SELECT FORMAT(AVG(total), 'C', 'es-PE') AS [Promedio del Monto Total en Soles] 
FROM [ve.documento];

### EJERCICIO 4
SELECT *
FROM ve.documento
WHERE total > (SELECT AVG(total) FROM ve.documento);

### EJERCICIO 5
SELECT d.*
FROM ve.documentoPago dp
INNER JOIN ve.documento d ON dp.documento = d.documento
INNER JOIN pa.pago p ON dp.pago = p.pago
WHERE p.formaPago = 10; -- 1 es pago al Contado

### EJERCICIO 6
SELECT d.*, dc.*
FROM ve.documento d
INNER JOIN ve.documentosCanjeados dc ON d.documento = dc.documento01 AND d.documento = dc.documento02;

### EJERCICIO 7
SELECT almacen, SUM(costoSoles) AS Saldo_Total
FROM ma.saldosIniciales
GROUP BY almacen;

### EJERCICIO 8
SELECT d.*
FROM ve.documento d
INNER JOIN ve.documentoDetalle dd ON d.documento = dd.documento
WHERE d.vendedor = 3;

### EJERCICIO 9
SELECT vendedor, YEAR(fechaMovimiento) AS Año, FORMAT(SUM(total), 'C', 'es-PE') AS Total_Ventas
FROM ve.documento
GROUP BY vendedor, YEAR(fechaMovimiento)
HAVING SUM(total) > 100000
ORDER BY SUM(total) ASC;

### EJERCICIO 10
SELECT vendedor, MONTH(fechaMovimiento) AS Mes, YEAR(fechaMovimiento) AS Año, FORMAT(SUM(total), 'C', 'es-PE') AS Total_Ventas
FROM ve.documento
GROUP BY vendedor, MONTH(fechaMovimiento), YEAR(fechaMovimiento)
HAVING SUM(total) > 100000
ORDER BY SUM(total) ASC;

### EJERCICIO 11
SELECT persona, YEAR(fechaMovimiento) AS Año, FORMAT(COUNT(*), 'C', 'es-PE') AS Compras
FROM ve.documento
WHERE tipoMovimiento = 1
GROUP BY persona, YEAR(fechaMovimiento)
HAVING COUNT(*) > 10
ORDER BY Año ASC;

### EJERCICIO 12
SELECT vendedor, FORMAT(SUM(descto01 + descto02 + descto03), 'C', 'es-PE') AS Descuentos_Acumulados
FROM ve.documento
GROUP BY vendedor
HAVING SUM(descto01 + descto02 + descto03) > 5000
ORDER BY vendedor ASC;

### EJERCICIO 13
SELECT persona, YEAR(fechaMovimiento) AS Año, FORMAT(SUM(total), 'C', 'es-PE') AS Total_Anual
FROM ve.documento
WHERE tipoMovimiento = 1
GROUP BY persona, YEAR(fechaMovimiento)
HAVING SUM(total) > 10000
ORDER BY Año ASC;

### EJERCICIO 14
SELECT d.vendedor, COUNT(dd.documentoDetalle) AS Total_Productos_Vendidos
FROM ve.documentoDetalle dd
JOIN ve.documento d ON dd.documento = d.documento
GROUP BY d.vendedor;

### EJERCICIO 15
SELECT MONTH(d.fechaMovimiento) AS Mes, p.formaPago, FORMAT(SUM(d.total), 'C', 'es-PE') AS Total_Ventas
FROM ve.documento d
JOIN pa.pago p ON d.vendedor = p.vendedor
WHERE YEAR(d.fechaMovimiento) = 2009
GROUP BY MONTH(d.fechaMovimiento), p.formaPago;

### EJERCICIO 16
DECLARE @fecha_inicio_2007 datetime = '2007-01-01';
DECLARE @fecha_fin_2007 datetime = '2007-12-31';

SELECT SUM(total) AS Total_Ventas
FROM ve.documento
WHERE fechaMovimiento BETWEEN @fecha_inicio_2007 AND @fecha_fin_2007;

### EJERCICIO 17
SELECT p.*
FROM ma.persona p
LEFT JOIN ma.personaDestino pd ON p.persona = pd.persona
WHERE pd.persona IS NULL

### EJERCICIO 18
SELECT AVG(total) AS Promedio_Ventas
FROM ve.documento
WHERE YEAR(fechaMovimiento) = 2009;

### EJERCICIO 19
SELECT *
FROM ve.documento
WHERE total > (SELECT AVG(total) FROM ve.documento WHERE YEAR(fechaMovimiento) = 2005);

### EJERCICIO 20
SELECT *
FROM ve.documentoPago dp
INNER JOIN ve.documento d ON dp.documento = d.documento
INNER JOIN pa.pago p ON dp.pago = p.pago
WHERE YEAR(fechaMovimiento) = 2006;

### EJERCICIO 21
SELECT almacen, FORMAT(SUM(costoSoles), 'C', 'es-PE') AS saldo_total
FROM ma.saldosIniciales
WHERE YEAR(periodo) = 2007
GROUP BY almacen;

### EJERCICIO 22
SELECT *
FROM ve.documento
WHERE total > (SELECT AVG(total) FROM ve.documento WHERE YEAR(fechaMovimiento) = 2008);

### EJERCICIO 23
SELECT *
FROM ve.documentoDetalle dd
JOIN ve.documento d ON dd.documento = d.documento
WHERE d.vendedor = 3 AND YEAR(d.fechaMovimiento) = 2009;

### EJERCICIO 24
SELECT YEAR(fechaMovimiento) AS Año, vendedor, FORMAT(SUM(total), 'C', 'es-PE') AS Total_Ventas
FROM ve.documento
WHERE YEAR(fechaMovimiento) = 2008
GROUP BY YEAR(fechaMovimiento), vendedor
HAVING SUM(total) > 100000;

### EJERCICIO 25
SELECT YEAR(fechaMovimiento) AS Año, MONTH(fechaMovimiento) AS Mes, vendedor, FORMAT(SUM(total), 'C', 'es-PE') AS Total_Ventas
FROM ve.documento
WHERE YEAR(fechaMovimiento) = 2009
GROUP BY YEAR(fechaMovimiento), MONTH(fechaMovimiento), vendedor;

### EJERCICIO 26
SELECT persona, COUNT(DISTINCT documento) AS Total_Compras
FROM ve.documento
WHERE YEAR(fechaMovimiento) = 2005
GROUP BY persona
HAVING COUNT(DISTINCT documento) > 10;

### EJERCICIO 27
SELECT vendedor, FORMAT(SUM(descto01 + descto02 + descto03), 'C', 'es-PE') AS Total_Descuentos
FROM ve.documento
WHERE YEAR(fechaMovimiento) = 2005
GROUP BY vendedor
HAVING SUM(descto01 + descto02 + descto03) > 5000;

### EJERCICIO 28
SELECT persona, YEAR(fechaMovimiento) AS Año, FORMAT(SUM(total), 'C', 'es-PE') AS Total_Anual
FROM ve.documento
WHERE tipoMovimiento = 1 AND YEAR(fechaMovimiento) = 2007
GROUP BY persona, YEAR(fechaMovimiento)
HAVING SUM(total) > 10000;

### EJERCICIO 29
SELECT d.vendedor, COUNT(dd.documentoDetalle) AS Total_Productos_Vendidos
FROM ve.documentoDetalle dd
JOIN ve.documento d ON dd.documento = d.documento
WHERE YEAR(d.fechaMovimiento) = 2008
GROUP BY d.vendedor;

### EJERCICIO 30
SELECT YEAR(d.fechaMovimiento) AS Año, MONTH(d.fechaMovimiento) AS Mes, p.formaPago, FORMAT(SUM(d.total), 'C', 'es-PE') AS Total_Ventas
FROM ve.documento d
JOIN pa.pago p ON d.vendedor = p.vendedor
WHERE YEAR(d.fechaMovimiento) = 2009
GROUP BY YEAR(d.fechaMovimiento), MONTH(d.fechaMovimiento), p.formaPago;
