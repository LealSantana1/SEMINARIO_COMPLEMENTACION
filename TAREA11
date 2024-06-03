# TAREA11
**TAREA11**

	
**EJERCICIO1**
>¿Cuáles son los identificadores y nombres de todos los proyectos existentes en la empresa?
```
SELECT IDProyecto,NombreProyecto
FROM Proyecto;
```
	
**EJERCICIO2**
>¿Cuáles son los proyectos que se desarrollan en 'CHICAGO'?
```
SELECT NombreProyecto,Ubicacion
FROM Proyecto
WHERE Ubicacion = 'CHICAGO';
```
	
**EJERCICIO3**
>¿Cuáles son los empleados que tienen un jefe, están asignados a más de un proyecto, y han trabajado más de 15 horas en total en todos los proyectos combinados?
```
SELECT NombreProyecto, Ubicacion, IDDepartamento
FROM Proyecto
WHERE IDDepartamento = 2;
```
	
**EJERCICIO4**
>¿Cuáles son los nombres y ubicaciones de los proyectos junto con los nombres de sus departamentos asociados?
```
SELECT p.NombreProyecto, p.Ubicacion, d.IDDepartamento AS Departamento
FROM Proyecto p
JOIN Departamento d ON p.IDDepartamento = d.IDDepartamento;
```
	
**EJERCICIO5**
>¿Qué empleados están asignados al proyecto identificado con el número 4, y cuáles son sus nombres?
```
SELECT e.IDEmpleado, e.NombreEmpleado, p.IDProyecto
FROM Empleado e
JOIN EmpleadoProyecto pe ON e.IDEmpleado = pe.IDEmpleado
JOIN Proyecto p ON pe.IDProyecto = p.IDProyecto
WHERE p.IDProyecto = 4;
```
**EJERCICIO6**
>¿En qué proyectos está participando el empleado con el identificador 4, y cuáles son los nombres de esos proyectos?
```
SELECT P.NombreProyecto
FROM EmpleadoProyecto EP
JOIN Proyecto P ON EP.IDProyecto = P.IDProyecto
WHERE EP.IDProyecto = 4;
```
**EJERCICIO7**
>¿Cuántas horas han trabajado en total los empleados en el proyecto con identificador 2?
```
SELECT SUM(HorasTrabajadas) AS TotalHorasTrabajadas
FROM EmpleadoProyecto
WHERE IDEmpleado IN (
SELECT IDEmpleado
FROM EmpleadoProyecto
WHERE IDProyecto = 2);
```
**EJERCICIO8**
>¿Cuáles son los empleados que han trabajado más de 10 horas en el proyecto con identificador 2?
```
SELECT e.IDEmpleado, e.NombreEmpleado
FROM Empleado e
JOIN (
SELECT IDEmpleado, SUM(HorasTrabajadas) AS HorasTrabajadas
FROM EmpleadoProyecto
WHERE IDProyecto = 2
GROUP BY IDEmpleado
HAVING SUM(HorasTrabajadas) > 10) AS t ON e.IDEmpleado = t.IDEmpleado;
```

**EJERCICIO9**
>¿Cuál es el total de horas trabajadas por cada empleado en todos los proyectos?
```
SELECT e.IDEmpleado, e.NombreEmpleado, SUM(t.HorasTrabajadas) AS HorasTrabajadas
FROM Empleado e
JOIN EmpleadoProyecto t ON e.IDEmpleado = t.IDEmpleado
GROUP BY e.IDEmpleado, e.NombreEmpleado;
```
**EJERCICIO10**
>¿Cuáles son los empleados que trabajan en más de un proyecto?
```
SELECT e.IDEmpleado, e.NombreEmpleado
FROM Empleado e
JOIN EmpleadoProyecto pe ON e.IDEmpleado = pe.IDEmpleado
GROUP BY e.IDEmpleado, e.NombreEmpleado
HAVING COUNT(DISTINCT pe.IDProyecto) > 1;
```
**EJERCICIO11**
>¿Cuáles son los empleados que han trabajado más de 30 horas en total en todos los proyectos?
```
SELECT e.IDEmpleado, e.NombreEmpleado, SUM(ht.HorasTrabajadas) AS HorasTrabajadas
FROM Empleado e
JOIN EmpleadoProyecto ht ON e.IDEmpleado = ht.IDEmpleado
GROUP BY e.IDEmpleado, e.NombreEmpleado
HAVING SUM(ht.HorasTrabajadas) > 30;
```
**EJERCICIO12**
>¿Cuál es el promedio de horas trabajadas por proyecto?
```
SELECT AVG(ht.HorasTrabajadas) AS HorasTrabajadas
FROM EmpleadoProyecto ht
JOIN Proyecto p ON ht.IDProyecto = p.IDProyecto
GROUP BY p.IDProyecto;
```
**EJERCICIO13**
>¿Cuáles son los empleados que trabajan en proyectos ubicados en 'CHICAGO' y que tienen un salario (con o sin comisión) superior a 2000?
```
SELECT E.IDEmpleado, E.NombreEmpleado, E.Salario, E.Comision, P.NombreProyecto
FROM Empleado E
JOIN EmpleadoProyecto EP on E.IDEmpleado = EP.IDEmpleado
JOIN Proyecto P ON EP.IDProyecto = P.IDProyecto
WHERE P.Ubicacion = 'CHICAGO' AND (E.Salario + COALESCE(E.Comision, 0)) > 2000;
```

```
SELECT e.IDEmpleado, e.NombreEmpleado, Ubicacion, e.Salario, e.Comision
FROM Empleado e
JOIN Empleado a ON e.IDEmpleado = a.IDEmpleado
JOIN Proyecto p ON a.IDEmpleado = p.IDProyecto
WHERE p.Ubicacion = 'CHICAGO' AND (e.Salario + COALESCE(e.Comision, 0)) > 2000;
```
**EJERCICIO14**
>¿Cuáles son los empleados que tienen un jefe, están asignados a más de un proyecto, y han trabajado más de 15 horas en total en todos los proyectos combinados?
```
SELECT e.IDEmpleado, e.NombreEmpleado
FROM Empleado e
JOIN(SELECT IDEmpleado
FROM EmpleadoProyecto
GROUP BY IDEmpleado
HAVING COUNT(DISTINCT IDProyecto) > 1
AND SUM(HorasTrabajadas) > 15)
pe ON e.IDEmpleado = pe.IDEmpleado
WHERE e.IDJefe IS NOT NULL;
```

**EJERCICIO15**
>¿Cuáles son los empleados que no reciben comisión y trabajan en departamentos ubicados en 'DALLAS' o 'NEW YORK'?
```
SELECT E.IDEmpleado, E.NombreEmpleado, D.NombreDepartamento, D.Ubicacion
FROM Empleado E
JOIN Departamento D ON E.IDDepartamento = D.IDDepartamento
WHERE  E.Comision IS NULL AND (D.Ubicacion = 'NEW YORK' OR D.Ubicacion = 'DALLAS');
```
