# Actividad 028 - CRUD anidado con asociación

- Para poder realizar este actividad debes haber realizado los cursos previos junto con los videos online correspondientes a la experiencia 14.

### El objetivo de esta actividad es la implementación de un CRUD anidado de Empresa, Empleados y Departamentos, donde cada Empresa puede tener N cantidad de empleados y un empleado solo puede pertenecer a 1 empresa (relación 1 a N), y cada empleado pertenece a un departamento y un departamento tiene muchos empleados (relación 1 a N).

## Ejercicio 1:

- Iniciar un nuevo proyecto en Rails 5.1 :heavy_check_mark:

- Añadir el **CDN de Boostrap** al layout :heavy_check_mark:

- Añadir el **CDN de jQuery** al layout :heavy_check_mark:

- Crear un scaffold **Company** con el campo *name* (string) :heavy_check_mark:

- Revisar y correr la migración :heavy_check_mark:

- Crear un scaffold **Area** con el campo *name* (string) :heavy_check_mark:

- Revisar y correr la migración :heavy_check_mark:

- Convertir el *index* de *companies* en la página de inicio. :heavy_check_mark:

- Crear un modelo **Employee** con los campos *first_name* (string), *last_name* (string), email (string), *company:references* y *area:references*. :heavy_check_mark:

- Revisar y correr la migración. :heavy_check_mark:

- En los modelos *Company* y *Area* agregar la relación con *Employee* (**has_many**) y verificar que el modelo *Employee* se haya creado con las relaciones correctas (**belongs_to**) :heavy_check_mark:

    > Recordar las relaciones entre empresa - empleado y empleado - area en el enunciado.

- Crear el controller **employees**. :heavy_check_mark:

- Generar la ruta para la creación de un empleado asociado a una empresa. :heavy_check_mark:

    - Para ello modificar la ruta resources de companies que ahora recibirá un bloque y dentro crearemos la ruta que apuntará al método create de employees. :heavy_check_mark:
    
    ~~~ruby
    resources :employees, only: [:create]
    ~~~

- En la terminal ejecutar **rails routes** para corroborar la ruta creada. La ruta generada debe contener el **:company_id** y apuntar al método **employees#create**. :heavy_check_mark:

- Para poder almacenar un registro en el método create primero debemos generar el filtro de parámetros conocido como **strong params**, para ello: :heavy_check_mark:

    - En el controller **employees** crear el método **employee_params**. Este método debe permitir y retornar los campos necesarios para la creación de un nuevo empleado, es decir, first_name, last_name y email. :heavy_check_mark:

- En el controller **employees** crear el método **create**. Este método debe generar una nueva instancia de *Employee* recibiendo como argumento **employee_params** y almacenarlo en la BD. Luego redireccionar a la vista *show* de la empresa involucrada. :heavy_check_mark:

- En la vista *Show* de *companies* además del detalle de la empresa, se debe agregar un formulario que permita ingresar un nuevo empleado a la empresa seleccionada. :heavy_check_mark:

    - El formulario debe ser generado utilizando el helper *form_with* anidando los dos modelos y debe implementar las clases de bootstrap (revisar docs). :heavy_check_mark:

    ~~~ruby
    <%= form_with(model: [ @company, @employee ]) do |form| %>
    ~~~

    - Donde **@employee** debe ser declarado en el método correspondiente como una nueva instancia de **Employee**. :heavy_check_mark:

    - El formulario debe tener campos para *first_name*, *last_name*, *email*, *area*. :heavy_check_mark:
    
    	> Recordar que el campo area debe ser un select.

- En la vista *show*, bajo el formulario, se deben listar todos los empleados correspondientes a esa empresa en una tabla con los campos *first_name*, *last_name*, *email* y *area*. :heavy_check_mark:

- Junto a cada registro de empleado en la tabla se debe añadir un botón para eliminar el empleado. Para ello: :heavy_check_mark:

    - Agregar el método *destroy* a la ruta anidada. :heavy_check_mark:

     ~~~ruby
     resources :employees, only: [:create, :destroy]
     ~~~

     - Crear el método correspondiente en el controller. :heavy_check_mark:

     - Agregar el botón con el *method: :delete* a cada registro de empleados en la tabla. :heavy_check_mark:

- En la vista *Index* de *companies*: 
    - Los registros deben estar listados en una tabla (bootstrap) que contenga el nombre de la empresa y la cantidad de empleados que existe por área (**count**). :x:

    - Al hacer click en el nombre de la empresa debe redireccionar a la vista *show* de esa empresa. :x:

    - Cada categoría ademas debe ir acompañada de botones para *Edit* y *Destroy* utilizando la clases de bootstrap. :x:

- En *application.html.erb*:
	- En una vista parcial, agregar un navbar (**fixed**) con bootstrap con los link para acceder al home (index de empresas), para agregar nueva empresa y para agregar nueva área. :x: