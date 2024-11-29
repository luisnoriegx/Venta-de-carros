<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.5.0/font/bootstrap-icons.css">
    <title>Registro de Vehículos</title>
    <style>
        .carrito {
            display: flex;
            align-items: center;
        }

        .carrito button {
            background-color: #f8f9fa;
            border: none;
            padding: 10px;
            border-radius: 50%;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            transition: transform 0.2s, background-color 0.3s;
        }

        .carrito button:hover {
            background-color: #e2e6ea;
            transform: scale(1.1);
        }

        #carrito {
            font-size: 12px;
            color: white;
            background-color: red;
            border-radius: 50%;
            padding: 5px 8px;
        }
    </style>
</head>
<body>
    <div class="container">
        <nav class="navbar navbar-dark bg-dark">
            <div class="container-fluid">
                <a class="navbar-brand" href="#">
                    <img src="https://1000marcas.net/wp-content/uploads/2020/01/Mazda-Logo-2018.png" alt="Logo" width="100" height="60">
                    <h2 class="d-inline-block text-white">CACHARROS LOS AMIGOS</h2>
                </a>
                <div class="carrito" data-bs-toggle="modal" data-bs-target="#factura" onclick="mostrarCarrito()">
                    <button type="button">
                        <i class="bi bi-cart4"></i>
                        <span id="carrito" class="badge rounded-pill">0</span>
                    </button>
                </div>
            </div>
        </nav>

        <div class="row mt-3 justify-content-center">
            <div class="col-6">
                <div class="card bg-success bg-gradient">
                    <div class="card-header">
                        <h2>REGISTRO DE VEHÍCULOS</h2>
                    </div>
                    <div class="card-body">
                        <div class="form-floating mb-3">
                            <input type="text" class="form-control" id="marca" placeholder="Marca">
                            <label for="marca">Marca</label>
                        </div>
                        <div class="form-floating mb-3">
                            <input type="number" class="form-control" id="modelo" placeholder="Modelo">
                            <label for="modelo">Modelo</label>
                        </div>
                        <div class="form-floating mb-3">
                            <input type="number" class="form-control" id="cilindraje" placeholder="Cilindraje">
                            <label for="cilindraje">Cilindraje</label>
                        </div>
                        <div class="form-floating mb-3">
                            <input type="text" class="form-control" id="imagen" placeholder="Imagen URL">
                            <label for="imagen">Imagen URL</label>
                        </div>
                        <div class="form-floating mb-3">
                            <input type="number" class="form-control" id="precio" placeholder="Precio">
                            <label for="precio">Precio</label>
                        </div>
                        <button type="button" onclick="registro()" class="btn btn-primary">Agregar</button>
                    </div>
                </div>
            </div>
        </div>

        <!-- VENTANA MODAL FACTURA -->
        <div class="modal fade" id="factura" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <h1 class="modal-title fs-5">Factura de Compra</h1>
                        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                    </div>
                    <div class="modal-body" id="carritoProductos">
                        <!-- Productos agregados se mostrarán aquí -->
                    </div>
                </div>
            </div>
        </div>

        <script>
            let contadorCarrito = 0;
            let productos = [];

            function registro() {
                const marca = document.getElementById('marca').value;
                const modelo = document.getElementById('modelo').value;
                const cilindraje = document.getElementById('cilindraje').value;
                const imagen = document.getElementById('imagen').value;
                const precio = document.getElementById('precio').value;

                if (marca && modelo && cilindraje && imagen && precio) {
                    // Crear un objeto con los datos del vehículo
                    const producto = { marca, modelo, cilindraje, imagen, precio };
                    productos.push(producto);

                    contadorCarrito++;
                    document.getElementById('carrito').innerText = contadorCarrito;

                    // Limpiar los campos del formulario
                    document.querySelectorAll('.form-control').forEach(input => input.value = '');
                } else {
                    alert('Todos los campos son obligatorios');
                }
            }

            function mostrarCarrito() {
                const carritoProductos = document.getElementById('carritoProductos');
                carritoProductos.innerHTML = ""; // Limpiar contenido previo

                productos.forEach((producto, index) => {
                    carritoProductos.innerHTML += `
                        <div class="mb-2">
                            <strong>${producto.marca} - ${producto.modelo}</strong><br>
                            Cilindraje: ${producto.cilindraje} | Precio: $${producto.precio}
                        </div><hr>
                    `;
                });
            }
        </script>
        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js"></script>
    </div>
</body>
</html>
