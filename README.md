# TAREA11
**TAREA11**

	
__EJERCICIO1__

SELECT IDProyecto,NombreProyecto
       FROM Proyecto;

	
**EJERCICIO2**

SELECT NombreProyecto,Ubicacion
FROM Proyecto
WHERE Ubicacion = 'CHICAGO';

	
**EJERCICIO3**

SELECT NombreProyecto, Ubicacion, IDDepartamento
FROM Proyecto
WHERE IDDepartamento = 2;
;
	
**EJERCICIO4**

SELECT p.NombreProyecto, p.Ubicacion, d.IDDepartamento AS Departamento
FROM Proyecto p
JOIN Departamento d ON p.IDDepartamento = d.IDDepartamento;

	
**EJERCICIO5**

SELECT e.IDEmpleado, e.NombreEmpleado, p.IDProyecto
FROM Empleado e
JOIN EmpleadoProyecto pe ON e.IDEmpleado = pe.IDEmpleado
JOIN Proyecto p ON pe.IDProyecto = p.IDProyecto
WHERE p.IDProyecto = 4;

**EJERCICIO6**

SELECT P.NombreProyecto
FROM EmpleadoProyecto EP
JOIN Proyecto P ON EP.IDProyecto = P.IDProyecto
WHERE EP.IDProyecto = 4;

**EJERCICIO7**

SELECT SUM(HorasTrabajadas) AS TotalHorasTrabajadas
FROM EmpleadoProyecto
WHERE IDEmpleado IN (
SELECT IDEmpleado
FROM EmpleadoProyecto
WHERE IDProyecto = 2);

**EJERCICIO8**

SELECT e.IDEmpleado, e.NombreEmpleado
FROM Empleado e
JOIN (
SELECT IDEmpleado, SUM(HorasTrabajadas) AS HorasTrabajadas
FROM EmpleadoProyecto
WHERE IDProyecto = 2
GROUP BY IDEmpleado
HAVING SUM(HorasTrabajadas) > 10) AS t ON e.IDEmpleado = t.IDEmpleado;


**EJERCICIO9**

SELECT e.IDEmpleado, e.NombreEmpleado, SUM(t.HorasTrabajadas) AS HorasTrabajadas
FROM Empleado e
JOIN EmpleadoProyecto t ON e.IDEmpleado = t.IDEmpleado
GROUP BY e.IDEmpleado, e.NombreEmpleado;

**EJERCICIO10**

SELECT e.IDEmpleado, e.NombreEmpleado
FROM Empleado e
JOIN EmpleadoProyecto pe ON e.IDEmpleado = pe.IDEmpleado
GROUP BY e.IDEmpleado, e.NombreEmpleado
HAVING COUNT(DISTINCT pe.IDProyecto) > 1;

**EJERCICIO11**

SELECT e.IDEmpleado, e.NombreEmpleado, SUM(ht.HorasTrabajadas) AS HorasTrabajadas
FROM Empleado e
JOIN EmpleadoProyecto ht ON e.IDEmpleado = ht.IDEmpleado
GROUP BY e.IDEmpleado, e.NombreEmpleado
HAVING SUM(ht.HorasTrabajadas) > 30;

**EJERCICIO12**

SELECT AVG(ht.HorasTrabajadas) AS HorasTrabajadas
FROM EmpleadoProyecto ht
JOIN Proyecto p ON ht.IDProyecto = p.IDProyecto
GROUP BY p.IDProyecto;

**EJERCICIO13**

SELECT E.IDEmpleado, E.NombreEmpleado, E.Salario, E.Comision, P.NombreProyecto
FROM Empleado E
JOIN EmpleadoProyecto EP on E.IDEmpleado = EP.IDEmpleado
JOIN Proyecto P ON EP.IDProyecto = P.IDProyecto
WHERE P.Ubicacion = 'CHICAGO' AND (E.Salario + COALESCE(E.Comision, 0)) > 2000;

SELECT e.IDEmpleado, e.NombreEmpleado, Ubicacion, e.Salario, e.Comision
FROM Empleado e
JOIN Empleado a ON e.IDEmpleado = a.IDEmpleado
JOIN Proyecto p ON a.IDEmpleado = p.IDProyecto
WHERE p.Ubicacion = 'CHICAGO' AND (e.Salario + COALESCE(e.Comision, 0)) > 2000;

**EJERCICIO14**

SELECT e.IDEmpleado, e.NombreEmpleado
FROM Empleado e
JOIN(SELECT IDEmpleado
FROM EmpleadoProyecto
GROUP BY IDEmpleado
HAVING COUNT(DISTINCT IDProyecto) > 1
AND SUM(HorasTrabajadas) > 15)
pe ON e.IDEmpleado = pe.IDEmpleado
WHERE e.IDJefe IS NOT NULL;

**EJERCICIO15**

SELECT E.IDEmpleado, E.NombreEmpleado, D.NombreDepartamento, D.Ubicacion
FROM Empleado E
JOIN Departamento D ON E.IDDepartamento = D.IDDepartamento
WHERE  E.Comision IS NULL AND (D.Ubicacion = 'NEW YORK' OR D.Ubicacion = 'DALLAS');
