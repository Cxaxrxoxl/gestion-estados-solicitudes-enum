# gestion-estados-solicitudes-enum
Sistema en C# para la gestión de solicitudes de clientes utilizando enumeradores (enum) para controlar y estandarizar los estados del proceso, aplicando Programación Orientada a Objetos y listas dinámicas.
namespace ConsoleApp11
{ 
    enum EstadoSolicitud
{
    Pendiente,
    EnProceso,
    Completada,
    Cancelada
}

class Solicitud
{
    public int Id { get; set; }
    public string Cliente { get; set; }
    public string Descripcion { get; set; }
    public EstadoSolicitud Estado { get; set; }

    public void Mostrar()
    {
        Console.WriteLine($"ID: {Id}");
        Console.WriteLine($"Cliente: {Cliente}");
        Console.WriteLine($"Descripción: {Descripcion}");
        Console.WriteLine($"Estado: {Estado}");
        Console.WriteLine("--------------------------");
    }
}

    class Program
    {
        static List<Solicitud> solicitudes = new List<Solicitud>();
        static int contadorId = 1;

        static void Main()
        {
            int opcion;

            do
            {
                Console.WriteLine("\n--- SISTEMA DE SOLICITUDES ---");
                Console.WriteLine("1. Registrar solicitud");
                Console.WriteLine("2. Mostrar solicitudes");
                Console.WriteLine("3. Cambiar estado");
                Console.WriteLine("4. Buscar por ID");
                Console.WriteLine("5. Salir");
                Console.Write("Seleccione una opción: ");
                opcion = int.Parse(Console.ReadLine());

                switch (opcion)
                {
                    case 1:
                        Registrar();
                        break;
                    case 2:
                        Mostrar();
                        break;
                    case 3:
                        CambiarEstado();
                        break;
                    case 4:
                        Buscar();
                        break;
                }

            } while (opcion != 5);
        }

        static void Registrar()
        {
            Solicitud s = new Solicitud();

            s.Id = contadorId++;
            Console.Write("Cliente: ");
            s.Cliente = Console.ReadLine();

            Console.Write("Descripción: ");
            s.Descripcion = Console.ReadLine();

            s.Estado = EstadoSolicitud.Pendiente;

            solicitudes.Add(s);

            Console.WriteLine("Solicitud registrada.");
        }

        static void Mostrar()
        {
            foreach (var s in solicitudes)
            {
                s.Mostrar();
            }
        }

        static void CambiarEstado()
        {
            Console.Write("Ingrese ID: ");
            int id = int.Parse(Console.ReadLine());

            var solicitud = solicitudes.Find(s => s.Id == id);

            if (solicitud != null)
            {
                Console.WriteLine("Seleccione nuevo estado:");
                foreach (var estado in Enum.GetValues(typeof(EstadoSolicitud)))
                {
                    Console.WriteLine($"{(int)estado} - {estado}");
                }

                int opcion = int.Parse(Console.ReadLine());
                solicitud.Estado = (EstadoSolicitud)opcion;

                Console.WriteLine("Estado actualizado.");
            }
            else
            {
                Console.WriteLine("Solicitud no encontrada.");
            }
        }

        static void Buscar()
        {
            Console.Write("Ingrese ID: ");
            int id = int.Parse(Console.ReadLine());

            var solicitud = solicitudes.Find(s => s.Id == id);

            if (solicitud != null)
            {
                solicitud.Mostrar();
            }
            else
            {
                Console.WriteLine("No encontrada.");
            }
        }
    }



}
    
