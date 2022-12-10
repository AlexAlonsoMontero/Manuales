# GUÍA PHP

- Declaración de una variable

```php
$nombrevariable
```

- Declaracińo de una función

```php
function nombreFuncion( $parametro){
            echo "texto de la función $parametro </br>";
        }
```

- Incluir funciones de otros ficheros php

```php
include ('nombreFichero.php');
```

## VARIABLES

### Ámbito de las variables

- Local: Declarada dentro de una función visible dentro de esea función
- Global: Declarada en cualquier lugar del código y visible desde cualquier lugar de código. Se declara como global siempre dentro de la función en la que se llama.

```php
<?php
        $nombre = "María";

        function cambiarNombre(){
            global $nombre;
            $nombre = "El nombre nuevo es " . $nombre;
        }
        cambiarNombre();
        echo $nombre;
    ?>
```

- Superglobal: Visible y accesible desde fuera del script PHP, se declara como Array.

### Variales estáticas:

- Se declaran usando static, y esto provoca que cuando la función finalice el valor de la variable se conserve en memoria.

```php
function incrementaVariable(){
    static $contador =0; // valor de la variable la primera vez que se llama la función
    $contador++;
    echo "$contador </br>";
}
incrementaVariable();
incrementaVariable();
incrementaVariable();
```

### Manejo de strings:

- strcmp() -> Función que compara dos cadenas. Devuelve 1 si no son iguales y 0 si son iguales.

```php
$v1 = "casa";
$v2 = "CASA";
$resultado = strcmp($v1, $v2);
```

## OPERADORES DE COMPARCIÓN

| Ejemplo   | Nombre | Resultado                                                                                                                                                           |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| $a == $b  |        | true si $a es igual a $b después de la manipulación de tipos.                                                                                                       |
| $a === $b |        | true si $a es igual a $b, y son del mismo tipo.                                                                                                                     |
| $a != $b  |        | true si $a no es igual a $b después de la manipulación de tipos.                                                                                                    |
| $a <> $b  |        | true si $a no es igual a $b después de la manipulación de tipos.                                                                                                    |
| $a !== $b |        | idéntico true si $a no es igual a $b, o si no son del mismo tipo.                                                                                                   |
| $a < $b   |        | que true si $a es estrictamente menor que $b.                                                                                                                       |
| $a > $b   |        | que true si $a es estrictamente mayor que $b.                                                                                                                       |
| $a <= $b  |        | o igual que true si $a es menor o igual que $b.                                                                                                                     |
| $a >= $b  |        | o igual que true si $a es mayor o igual que $b.                                                                                                                     |
| $a <=> $b |        | espacial Un integer menor que, igual a, o mayor que cero cuando $a es respectivamente menor que, igual a, o mayor que $b. Disponible a partir de PHP 7.             |
| $a ?? $b  |        | $c Fusión de null El primer operando de izquierda a derecha que exista y no sea null. null si no hay valores definidos y no son null. Disponible a partir de PHP 7. |

## CONSTANTES:

```php
define ("AUTOR", "alex");
echo AUTOR . "<br>";
echo "el autor es " . AUTOR;
```

### Constatnte predefinidas:

- Se pueden consultar en aquí: https://www.php.net/manual/es/language.constants.predefined.php

## FORMULARIOS:

- Ejemplo formulario y método isset

```php
    <?php
    echo "Bienvenido.</br>";
    include('01-funciones.php');
    dameDatos("el dato es </br>");

    echo "Este es el segundo mensaje</br>";
    ?>
    <h1>Constantes</h1>
    <?php
        define ("AUTOR", "alex");
        echo AUTOR . "<br>";
        echo "el autor es " . AUTOR;
    ?>
    <h1>Practicas operadores</h1>
    <form name="form1" method="post" action="">
        <label for="num1"></label>
        <input type="text" name="num1" id="num1">
        <label for="num2"></label>
        <input type="text" name="num2" id="num2">
        <label for="operacion"></label>
        <select name="operacion" id="operacion">
            <option value="Suma">Suma</option>
            <option value="Resta">Resta</option>
            <option value="Multipliacion">Multiplicación</option>
            <option value="Division">División</option>
            <option value="Modulo">Módulo</option>
        </select>
    </p>
    <button type="submit" name="button" id="button" onClick="prueba" value="Enviar">
        Enviar
    </button>
    </form>
    <?php
    echo "<br>";
        if(isset($_POST["button"])){
            $numero1 = $_POST["num1"];
            $numero2 = $_POST["num2"];
            $operacion = $_POST["operacion"];
            calcular($operacion, $numero1, $numero2);

        }
    function calcular ($operacion, $numero1, $numero2){
        if(!strcmp("Suma", $operacion)){
            echo "El resultado es " . ($numero1 + $numero2);
        }else if(!strcmp("Resta", $operacion)){
            echo "El resultado es " . ($numero1 - $numero2);

        }else if(!strcmp("Multipliacion", $operacion)){
            echo "El resultado es " . ($numero1 * $numero2);

        }else if(!strcmp("Division", $operacion)){
            echo "El resultado es " . ($numero1 / $numero2);

        }else if(!strcmp("Modulo", $operacion)){
            echo "El resultado es " . ($numero1 % $numero2);

        }
    }

    ?>
```

## CONDICIONALES PHP

- [IF](https://www.php.net/manual/es/control-structures.if.php)
- [SWITCH CASE](https://www.php.net/manual/es/control-structures.switch.php)

## BUCLES:

- [FOR](https://www.php.net/manual/es/control-structures.for.php)
- [WHILE](https://www.php.net/manual/es/control-structures.while.php)

## FUNCIONES:

- Parametros por referencia:

```php
<?php
        function incremento(&$numero){
            $numero++;
            return $numero;
        }
        $numero1 = 3;
        $numero2 = incremento($numero1);
        echo ($numero1) ."<br>";
        echo ($numero2);
    ?>
```

- En este caso imprimirá 4 ya que al pasar el parametro por referencia afecta al valor de la variable fuera de la función.

## PROGRAMACIÓN ORIENTADA A OBJETOS:

- Declaración e instanciamiento de una clase

```php
<?php
        class Coche{
            public int $ruedas;
            public string $color;
            public int $motor;
            public string $marca; //

            public function __construct($color, $motor, $marca){
                $this->ruedas = 4;
                $this->color = $color;
                $this->motor = $motor;
                $this->marca = $marca;
            }

            public function printCoche (){
                echo "El coche tiene $this->ruedas ruedas, es de color $this->color, con un motor de
                    $this->motor cv y es de la marca $this->marca";
            }
        }

        $coche1 = new Coche("rojo", 1600, "Renault");
        var_dump($coche1);
        echo "<br>";

        //imprimir una propiedad
        echo $coche1->color . " <br>";
        //llamar a una función
        echo $coche1->printCoche();


    ?>
    ```
    - Herencia:
    ```php
     //CLASE PADRE
        class Vehiculo{
            public int $ruedas;
            public string $color;
            public int $motor;
            public string $marca; //

            public function __construct(int $ruedas, string $color, int $motor, string $marca){
                $this->ruedas = $ruedas;
                $this->color = $color;
                $this->motor = $motor;
                $this->marca = $marca;
            }

            public function printVehiculo (){
                echo "El coche tiene $this->ruedas ruedas, es de color $this->color, con un motor de
                    $this->motor cv y es de la marca $this->marca";
            }
        }
        //CLASE HIJA
        class Coche extends Vehiculo{
            public string $tipo;
            public function __construct(int $ruedas, string $color, int $motor, string $marca)
            {
                parent::__construct( $ruedas,  $color, $motor, $marca);
                $this ->tipo ="camión";
            }
            //SOBRESCRITURA DE MÉTODOS
            function printVehiculo(){
                echo "<p>El coche tiene $this->ruedas ruedas, es de color $this->color, con un motor de
                    $this->motor cv y es de la marca $this->marca y es de tipo $this->tipo </p>";
            }

        }

        $coche1 = new Coche(4, "rojo", 1400, "Peugeot");
        var_dump($coche1);
        echo "<br>El coche es de color $coche1->color <br>";
        $coche1->printVehiculo();
```

- Encapsulado:

```php
    class Vehiculo
    {
        protected int $ruedas;
        protected string $color;
        protected int $motor;
        protected string $marca; //

        public function __construct(int $ruedas, string $color, int $motor, string $marca)
        {
            $this->ruedas = $ruedas;
            $this->color = $color;
            $this->motor = $motor;
            $this->marca = $marca;
        }
        public function printVehiculo()
        {
            echo "El coche tiene $this->ruedas ruedas, es de color $this->color, con un motor de
                    $this->motor cv y es de la marca $this->marca";
        }
        /**
         * Set the value of motor
         *
         * @return  self
         */
        public function setMotor($motor)
        {
            $this->motor = $motor;

            return $this;
        }

        /**
         * Get the value of color
         */
        public function getColor()
        {
            return $this->color;
        }

        /**
         * Set the value of color
         *
         * @return  self
         */
        public function setColor($color)
        {
            $this->color = $color;

            return $this;
        }

        /**
         * Get the value of ruedas
         */
        public function getRuedas()
        {
            return $this->ruedas;
        }

        /**
         * Set the value of ruedas
         *
         * @return  self
         */
        public function setRuedas($ruedas)
        {
            $this->ruedas = $ruedas;

            return $this;
        }
        /**
         * Get the value of marca
         */
        public function getMarca()
        {
            return $this->marca;
        }

        /**
         * Set the value of marca
         *
         * @return  self
         */
        public function setMarca($marca)
        {
            $this->marca = $marca;

            return $this;
        }

        /**
         * Get the value of motor
         */
        public function getMotor()
        {
            return $this->motor;
        }
    }
    //CLASE HIJA
    class Coche extends Vehiculo
    {
        public string $tipo;
        public function __construct(int $ruedas, string $color, int $motor, string $marca)
        {
            parent::__construct($ruedas,  $color, $motor, $marca);
            $this->tipo = "camión";
        }
        //SOBRESCRITURA DE MÉTODOS
        function printVehiculo()
        {
            echo "<p>El coche tiene $this->ruedas ruedas, es de color $this->color, con un motor de
                    $this->motor cv y es de la marca $this->marca y es de tipo $this->tipo </p>";
        }

        /**
         * Get the value of tipo
         */
        public function getTipo()
        {
                return $this->tipo;
        }

        /**
         * Set the value of tipo
         *
         * @return  self
         */
        public function setTipo($tipo)
        {
                $this->tipo = $tipo;

                return $this;
        }
    }

    $coche1 = new Coche(4, "rojo", 1400, "Peugeot");
    var_dump($coche1);
    echo $coche1->getTipo();
    echo "<br>El coche es de color " . $coche1->getTipo() . "<br>";
    $coche1->printVehiculo();

    ?>
```

- LLamar a una clase desde un fichero, en este caso pasamos la clase Vehículo y la clase Coche a un fichero 01-claseVehiculo.php. El código en el index desde donde llamammos a la clase queda así.

```php
include('01-claseVehiculo.php');
    $coche1 = new Coche(4, "rojo", 1400, "Peugeot");
    var_dump($coche1);
    echo $coche1->getTipo();
    echo "<br>El coche es de color " . $coche1->getTipo() . "<br>";
    $coche1->printVehiculo();
```

## ARRAYS

- Declaración de un array.

```php
$semana = array("Lunes", "Martes", "Miércoles", "Jueves");
        echo $semana[0];
```

- Arrays clave valor:

```php
$datos = array(
            "nombre"=>"Alejandro",
            "apellido"=> "Alonso,",
            "edad"=> 41
        );
        echo "El nombre es $datos[nombre], y el Apellido " . $datos['apellido'];
```

- Recorrer un array con bucles for y foreach

```php
echo "<p>Foreach</p>";
        foreach ($datos as $dato) {
            echo "<p>$dato</p>";
        }
        echo "<p>For</p>";
        for ($i=0; $i<count($semana); $i++){
            echo "<p>$semana[$i]</p>";
        }
    ?>
```

- Array bidimensional:

```php
<?php
        $ropa = array ("deportiva"=>array(
                            "nike"=>"USA",
                            "adidas"=>"Alemania",
                            "kelme"=>"España"
                        ),
                        "casual"=>array(
                            "levis"=>"usa",
                            "zara"=>"españa"
                        )

                        );
        foreach( $ropa as $marcas =>$marc){
            echo "<br>$marcas</br>";
            while (list($key, $value )=[key($marc), current($marc)]){
                echo "<p>la key $key</p>";
                echo "<p>el value $value </p>";
            }
        }


    ?>
```

## CONEXIÓN A BASE DE DATOS PDO:
- COMO CONEECTAR CON BASE DE DATOSE

- EJEMPLO CON PDO
     - Creamos un archivo config.php. Este archivo devuelve un array con los datos de configuración.
    ```php
    <?php
    return [
      'db' => [
        'host' => 'localhost',
        'user' => 'root',
        'pass' => 'root',
        'name' => 'nombre_bd',
        'options' => [
          PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION
        ]
      ]
    ];
    ```
    -Ahora crea un archivo llamado instalar.php en el directorio raíz del proyecto y, en su interior, incluye el array de configuración y asigna una nueva instancia de la clase PDO a una variable, a la que llamaremos $conexion.  Para crear el objeto PDO usaremos los datos del array de configuración.
    ```php
    $config = include 'config.php';
    $conexion = new PDO('mysql:host=' . $config['db']['host'], $config['db']['user'], $config['db']['pass'], $config['db']['options']);
    ```
    - Como ejecutar sentencias (en el ejemplo usamos un insert pero puede ser cualquier tipo de sentencia):
    ```php
    $consultaSQL = "INSERT INTO alumnos (nombre, apellido, email, edad)";
    $consultaSQL .= "values (:" . implode(", :", array_keys($alumno)) . ")";
    
    $sentencia = $conexion->prepare($consultaSQL);
    $sentencia->execute($alumno);
    ```

#### EVITAR ATAQUES:
- El siguiente código codifica el texto en html, el uso normal es incluirla en un archivo, y con un include llamarlo en cualquier fichero con un formulario. 
    ```php
    function escapar($html) {
    return htmlspecialchars($html, ENT_QUOTES | ENT_SUBSTITUTE, "UTF-8");
    }
    ```
- Luego aplicaremos la función escapar al contenido que vendría en el $_POST
    ```php
    $resultado = [
    'error' => false,
    'mensaje' => 'El alumno ' . escapar($_POST['nombre']) . ' ha sido agregado con éxito'
    ];
    ```

## EJEMPLO FICHERO PHP CON FORMULARIO PAR INSERTAR REGISTRO EN UNA TABLA DE BASE DE DATOS:

- Este es un ejemplo de formulario para insertar un registro en base de datos y el códig php necesario.
- En este código se hacen includes:
    - funciones.php hace refrencia al código explicado en la sección EVITAR ATAQUES.
    ```php
    function escapar($html) {
    return htmlspecialchars($html, ENT_QUOTES | ENT_SUBSTITUTE, "UTF-8");
    }
    ```
    - config.php hace referencia al primer extracto de código explicado en la sección   EJEMPLO CON PDO
    ```php
    <?php
    return [
      'db' => [
        'host' => 'localhost',
        'user' => 'root',
        'pass' => 'root',
        'name' => 'nombre_bd',
        'options' => [
          PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION
        ]
      ]
    ];
    ```
    - El formulario de ingreso esta realizado con bootstrap.

    - CÓDIGO:
    ```php
    <?php
    include 'funciones.php';

    if (isset($_POST['submit'])) {
      $resultado = [
        'error' => false,
        'mensaje' => 'El alumno ' . escapar($_POST['nombre']) . ' ha sido agregado con éxito'
      ];

      $config = include 'config.php';

    try {
        $dsn = 'mysql:host=' . $config['db']['host'] . ';dbname=' . $config['db']['name'];
        $conexion = new PDO($dsn, $config['db']['user'], $config['db']['pass'], $config['db']['options']);

        $alumno = array(
          "nombre"   => $_POST['nombre'],
          "apellido" => $_POST['apellido'],
          "email"    => $_POST['email'],
          "edad"     => $_POST['edad'],
        );

        $consultaSQL = "INSERT INTO alumnos (nombre, apellido, email, edad) values (:" . implode(", :", array_keys($alumno)) . ")";

        $sentencia = $conexion->prepare($consultaSQL);
        $sentencia->execute($alumno);
    } catch(PDOException $error) {
        $resultado['error'] = true;
        $resultado['mensaje'] = $error->getMessage();
        } 
    }
    ?>
    <?php
        if (isset($resultado)) {
    ?>
    <div class="container mt-3">
        <div class="row">
        <div class="col-md-12">
            <div class="alert alert-<?= $resultado['error'] ? 'danger' : 'success' ?>" role="alert">
            <?= $resultado['mensaje'] ?>
            </div>
        </div>
        </div>
    </div>
  
    }
    ?>
    ```

## CONEXIÓN A BASE DE DATOS mysqli:
- [mysqli_connect ](https://www.php.net/manual/es/function.mysqli-connect.php)
- [Sentencias Preparadas](https://www.php.net/manual/es/mysqli.quickstart.prepared-statements.php)
