# ASP.NET

## Visual Studio Code
* Crear Proyecto ASP (Model View Controller) tildando Config HTTPS

Nota:
Si al correr tira error de certificado SSL, abrir cmd en cualquier ubicacion:

> dotnet dev-certs https --clean
> dotnet dev-certs https --trust
> Cerrar Visual Code

Darle que si a borrar cada uno de los certificados y luego crea nuevos.

## Controller
* Los metodos son las respuestas a las peticiones. 
* Retornan HTML. 
> return View("page.html");
* Si no se especifica el nombre del html, se usa aquel que coincide con el nombre del metodo. 
> View();
* El metodo View() busca los html en las carpetas Shared y Home (dentro de View)
* Se puede tener varios controladores, por topicos.

## Views
La logica de presentacion esta en la vista por ser MVC. Se usa Razor, son archivos con extension cshtml. En ellos se incrusta C# en el HTML:
> Bloque de codigo @{...}
> @If(...) \<p>...\</p>  else  \<p>...\</p>
> @for(...) { ... html ... }

## Comunicacion 

### Entre View y _layout
Se usa ViewData. Por ejemplo en el cshtml:

>@ { ViewData["Title"] = "Home Page"; }

Y, en el HTML:

> \<title>@ViewData["Title"] - QUNAJ\</title>

### Entre Controller y View
Se puede usar ViewBag, pero no es fuertemente tipado. Por ello se recomienda lo siguiente:

* El controlador pasa un objeto
> View( new Persona("Juan") );
* Se declara al comienzo del .cshtml
> @Model Persona
* Se invoca donde se necesite
> @Model.Nombre

Nota: Si el parametro es string, se debe especificar antes el nombre del archivo html.

## Front - wwwroot
Al html se pueden importar los css y js en el archivo **Views/Shared/_layout._cshtml**. 

En el **head**, para el tag **link** se usa **asp-append-version=true** para asegurarse de que si cambia el archivo css el navegador no use lo que tiene en chache.

## Archivos importantes

### Views/Shared/_layout._cshtml
Es un contenedor (header y body) del html retornado por el controlador. El html se incrusta donde aparece @RenderBody, o sea, en _layout hay un div que contiene : 
> \<main role="main" class="pb-3"> 
> @RenderBody() 
> \</main>

### Program.cs
Aqui se especifica las rutas. Por defecto se usa el metodo Index de HomeController con id opcional:

> app.MapControllerRoute(  name: "default"
, pattern:"{controller=Home}/{action=Index}/{id?}"
);

### Views/_ViewStart.cshtml
Aqui se especifica que _layout.cshtml sera el archivo que contiene el encabezado y pie de pagina.

### Archivos JSON
* launchSettings : se configuran los perfiles, o sea, hay varios modos de ejecutar. El perfil principal por defecto esta en "Development". Se le puede colocar "Production" cuando esta terminado.
* appsettings : para modo Production
* appsettings.Development : modo development

