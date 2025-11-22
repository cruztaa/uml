```mermaid
classDiagram
    direction TB
    
    %% Título del Diagrama
    note "Clases de Control, Entidad y Roles" as TitleNote
    
    %% Clases de Roles (Actores)
    class UsuarioBase {
        -idUsuario: int
        -nombre: string
        -email: string
        -telefono: string
        -contrasena: string
        +verPacksVacantes()
        +iniciarSesion()
    }
    
    class Consumidor {
        -direccionEntrega: string
        -metodoPago: string
        +comprarPack(PackSorpresa)
        +valorarServicio(Valoracion)
    }
    
    class Empleado {
        -cargo: string
        +gestionarInventario()
        +publicarPack(PackSorpresa)
    }
    
    class Repartidor {
        -licencia: string
        -vehiculo: string
        +verRutas(Ruta)
        +actualizarEstadoEntrega(Entrega)
    }
    
    %% Clases de Entidad (Datos del Negocio)
    class Restaurante {
        -nombreContacto: string
        -Rfc: string
        -direccion: string
        -telefono: string
        -email: string
        -descripcion: string
        +Alta()
        +Modificar()
        +VerPacksPublicados()
    }
    
    class PackSorpresa {
        -nombre: string
        -precioVenta: float
        -horaRecogida: string
        -descripcion: string
        -estado: string
        +Alta()
        +Modificar()
        +ConsultarDatos()
        +Eliminar()
    }
    
    class Pedido {
        -fecha: date
        -total: float
        -estado: string
        +Alta()
        +ConfirmarPago()
        +ConsultarEstado()
    }
    
    class Entrega {
        -tiempoEstimado: string
        -estado: string
        +AsignarRepartidor(Repartidor)
        +ActualizarEstado()
    }
    
    class Ruta {
        -distanciaTotal: float
        -tiempoEstimado: string
        +CrearRuta(Entrega)
        +OptimizarRuta()
        +VerUbicacionActual()
    }
    
    class Valoracion {
        -puntuacion: int
        -comentario: string
        -fecha: date
        +Alta()
    }
    
    %% Clase de Control (Simulando Conexión o Lógica Central)
    class Conexion {
        -cadenaConexion: string
        +EstablecerConexion()
    }
    
    %% RELACIONES
    
    %% Herencia (Generalización)
    UsuarioBase <|-- Consumidor
    UsuarioBase <|-- Empleado
    UsuarioBase <|-- Repartidor
    
    %% Roles y Entidades
    Consumidor "1" *-- "0..*" Pedido : realiza
    Pedido "1" -- "0..1" Entrega : requiere
    Repartidor "1" -- "0..*" Entrega : asignadoA
    Restaurante "1" -- "0..*" Empleado : tiene
    Restaurante "1" *-- "0..*" PackSorpresa : publica
    
    %% Packs y Pedidos
    Pedido "1" -- "1..*" PackSorpresa : contiene
    
    %% Valoración
    Consumidor "1" -- "0..*" Valoracion : emite
    Pedido "1" -- "0..1" Valoracion : esValorado

    %% Logística
    Ruta "1" -- "1..*" Entrega : incluye

    %% Asociación con Control (dependencia en lugar de asociación rígida)
    Conexion ..> Consumidor
    Conexion ..> Restaurante
    Conexion ..> Repartidor
```
