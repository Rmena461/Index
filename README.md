# Index
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formulario de Cliente</title>
    <style id="theme-style">
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: white;
            color: black;
        }
        form {
            width: 300px;
            margin: auto;
        }
        label {
            display: block;
            margin-top: 10px;
        }
        input, textarea {
            width: 100%;
            padding: 5px;
            margin-top: 5px;
        }
        button {
            margin-top: 20px;
            padding: 10px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>

<h2>Formulario de Cliente</h2>

<button onclick="toggleTheme()">Cambiar Tema</button>

<form id="clienteForm">
    <label for="nombre">Nombre:</label>
    <input type="text" id="nombre" name="nombre" required>

    <label for="pedido">Pedido:</label>
    <input type="text" id="pedido" name="pedido" required>

    <label for="sku">SKU:</label>
    <input type="text" id="sku" name="sku" required>

    <label for="status">Status:</label>
    <input type="text" id="status" name="status" required>

    <label for="telefono">Teléfono:</label>
    <input type="tel" id="telefono" name="telefono" required>

    <label for="observacion">Observación:</label>
    <textarea id="observacion" name="observacion" rows="4"></textarea>

    <button type="button" onclick="guardarDatos()">Guardar</button>
    <button type="button" onclick="descargarDatos()">Descargar Todos</button>
</form>

<script>
    function toggleTheme() {
        const themeStyle = document.getElementById('theme-style');
        const darkTheme = `
            body {
                font-family: Arial, sans-serif;
                margin: 20px;
                background-color: black;
                color: white;
            }
            form {
                width: 300px;
                margin: auto;
            }
            label {
                display: block;
                margin-top: 10px;
            }
            input, textarea {
                width: 100%;
                padding: 5px;
                margin-top: 5px;
                background-color: #333;
                color: white;
                border: 1px solid #555;
            }
            button {
                margin-top: 20px;
                padding: 10px;
                background-color: #4CAF50;
                color: white;
                border: none;
                cursor: pointer;
            }
            button:hover {
                background-color: #45a049;
            }
        `;
        const lightTheme = `
            body {
                font-family: Arial, sans-serif;
                margin: 20px;
                background-color: white;
                color: black;
            }
            form {
                width: 300px;
                margin: auto;
            }
            label {
                display: block;
                margin-top: 10px;
            }
            input, textarea {
                width: 100%;
                padding: 5px;
                margin-top: 5px;
                background-color: white;
                color: black;
                border: 1px solid #ccc;
            }
            button {
                margin-top: 20px;
                padding: 10px;
                background-color: #4CAF50;
                color: white;
                border: none;
                cursor: pointer;
            }
            button:hover {
                background-color: #45a049;
            }
        `;

        if (themeStyle.innerHTML === lightTheme) {
            themeStyle.innerHTML = darkTheme;
        } else {
            themeStyle.innerHTML = lightTheme;
        }
    }

    function guardarDatos() {
        let nombre = document.getElementById('nombre').value;
        let pedido = document.getElementById('pedido').value;
        let sku = document.getElementById('sku').value;
        let status = document.getElementById('status').value;
        let telefono = document.getElementById('telefono').value;
        let observacion = document.getElementById('observacion').value;

        let datosCliente = `Nombre: ${nombre}\nPedido: ${pedido}\nSKU: ${sku}\nStatus: ${status}\nTeléfono: ${telefono}\nObservación: ${observacion}\n\n`;

        let datosGuardados = localStorage.getItem('datosClientes');
        if (datosGuardados) {
            datosCliente = datosGuardados + datosCliente;
        }

        localStorage.setItem('datosClientes', datosCliente);
        alert("Datos guardados correctamente");

        // Limpiar el formulario
        document.getElementById('clienteForm').reset();
    }

    function descargarDatos() {
        let datosCliente = localStorage.getItem('datosClientes');
        if (!datosCliente) {
            alert("No hay datos para descargar");
            return;
        }

        let blob = new Blob([datosCliente], { type: "text/plain" });
        let link = document.createElement("a");
        link.href = URL.createObjectURL(blob);

        let nombreArchivo = prompt("Introduce el nombre del archivo:", "datos_cliente.txt");
        if (nombreArchivo) {
            link.download = nombreArchivo;
            link.click();
            URL.revokeObjectURL(link.href);
            alert("Datos descargados correctamente en " + nombreArchivo);

            // Limpiar el almacenamiento local
            localStorage.removeItem('datosClientes');
        }
    }
</script>

</body>
</html>
