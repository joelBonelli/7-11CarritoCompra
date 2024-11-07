# Diagrama de Clases Carrito de Compras


```mermaid
classDiagram
    %% Clases base y derivadas con herencia
    class Producto {
        -String id
        -String nombre
        -String descripcion
        -float precio
        -int stock
        +disponibilidad() bool
        +calcularPrecioFinal() float
    }

    class ProductoFisico {
        -float peso
        +calcularPrecioFinal() float
    }

    class ProductoDigital {
        -String formato
        +calcularPrecioFinal() float
    }

    Producto <|-- ProductoFisico
    Producto <|-- ProductoDigital

    %% Clases principales
    class CarritoDeCompras {
        -String id
        -Date fechaCreacion
        -List~Item~ items
        +agregarItem(item: Item)
        +eliminarItem(item: Item)
        +calcularTotal() float
        +vaciarCarrito()
    }

    class Item {
        -Producto producto
        -int cantidad
        +calcularSubTotal() float
    }

    class Usuario {
        -String idUsuario
        -String nombre
        -String email
        -String direccion
        +registrar()
        +iniciarSesion()
        +comprarCarrito(carrito: CarritoDeCompras)
    }

    class Pago {
        -String idPago
        -float montoTotal
        -String metodoPago
        -Date fechaPago
        +procesarPago()
    }

    class Envio {
        -String idEnvio
        -String direccionEnvio
        -Date fechaEnvio
        -Date fechaEntrega
        +calcularCostoEnvio() float
    }

    %% Relaciones entre clases
    CarritoDeCompras "1" -- "*" Item : contiene
    Item "1" -- "1" Producto : referencia
    Usuario "1" -- "1" CarritoDeCompras : posee
    CarritoDeCompras "1" -- "1" Pago : asociado a
    Pago "1" -- "1" Envio : genera
