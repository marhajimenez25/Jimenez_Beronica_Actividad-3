// EmpleadoTest.java

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class EmpleadoTest {

    @Test
    public void testCrearEmpleadoPermanente() {
        EmpleadoPermanente emp = new EmpleadoPermanente("001", "Carlos Ruiz", 4500000);
        assertEquals("001", emp.getId());
        assertEquals("Carlos Ruiz", emp.getNombre());
        assertEquals(4500000, emp.getSalario());
        assertEquals("Permanente", emp.getTipo());
    }

    @Test
    public void testCrearEmpleadoTemporal() {
        EmpleadoTemporal emp = new EmpleadoTemporal("002", "Laura Gómez", 6);
        assertEquals("002", emp.getId());
        assertEquals("Laura Gómez", emp.getNombre());
        assertEquals(6, emp.getDuracionContrato());
        assertEquals("Temporal", emp.getTipo());
    }

    @Test
    public void testAgregarEmpleadoADepartamento() {
        GestorRRHH gestor = new GestorRRHH();
        Empleado emp = new EmpleadoPermanente("003", "Pedro López", 3800000);
        gestor.agregarEmpleado(emp);
        gestor.crearDepartamento("IT");
        gestor.asignarEmpleadoADepartamento("003", "IT");

        Departamento dpto = gestor.buscarDepartamentoPorNombre("IT");
        assertNotNull(dpto);
        assertEquals(1, dpto.getEmpleados().size());
        assertEquals("Pedro López", dpto.getEmpleados().get(0).getNombre());
    }

    @Test
    public void testBuscarEmpleadoPorId() {
        GestorRRHH gestor = new GestorRRHH();
        Empleado emp = new EmpleadoTemporal("004", "Ana Torres", 3);
        gestor.agregarEmpleado(emp);

        Empleado encontrado = gestor.buscarEmpleadoPorId("004");
        assertNotNull(encontrado);
        assertEquals("Ana Torres", encontrado.getNombre());
    }

    @Test
    public void testDepartamentoVacio() {
        Departamento depto = new Departamento("Contabilidad");
        assertEquals(0, depto.getEmpleados().size());
    }
}

