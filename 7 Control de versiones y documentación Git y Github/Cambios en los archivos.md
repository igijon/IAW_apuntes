
#git #github
# Cambios en los archivos

Si modificamos el fichero `index.html` 

```html
<!doctype html>
<html lang="en">
  <head>
  	<title>Ejemplo GIT</title>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

	<link href="https://fonts.googleapis.com/css?family=Lato:300,400,700,900&display=swap" rel="stylesheet">

	<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
	
	<link rel="stylesheet" href="css/style.css">

	</head>
	<body>
	<section class="ftco-section">
		<div class="container">
			<div class="row justify-content-center">
				<div class="col-md-6 text-center mb-5">
					<h2 class="heading-section">Login #07</h2>
				</div>
			</div>
			<div class="row justify-content-center">
				<div class="col-md-12 col-lg-10">
					<div class="wrap d-md-flex"

....
```

Podemos ver los cambios en VSCode:

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Cambios%20en%20los%20archivos/Untitled.png)

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Cambios%20en%20los%20archivos/Untitled%201.png)

Si hago otra modificación en `index.html`, aparecerá como `M` modificado.

Si no hago commit ni lo añado al stage si hago:

```html
git diff
```

![Untitled](400%20🌋%20Implantación%20de%20aplicaciones%20web/7%20Control%20de%20versiones%20y%20documentación%20Git%20y%20Github/Cambios%20en%20los%20archivos/Untitled%202.png)

Normalmente para ver los cambios podemos utilizar las herramientas de VSCode.