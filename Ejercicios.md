## Funciones literales/Funciones anónimas
### Ejercicio 1
```scala
/**
 * Calcula el área de un triángulo rectangulo
 * @param Double ladoA
 * @param Double ladoB
 * @return Retorna el cálculo del área
 */
val areaTrianguloRectangulo = (ladoA:Double,ladoB:Double) => { (ladoA * ladoB) / 2 }

areaTrianguloRectangulo(4,3)
```
### Ejercicio 2

```scala
/**
 * Calcula el área de un circulo
 * @param Double radio
 * @return Retorna el cálculo del área
 */
val areaDeUnCirculo = new Function1[Double,Double] {
   def apply(radio:Double) = 3.1416 * radio * radio
}

areaDeUnCirculo(2)
```
---
## Funciones de primera clase y funciones de alto orden
### Ejercicio 3

```scala
/**
 * Función que retorna otra función
 * @param Function Nombre de la función
 * @param Double valorA
 * @param Double valorB
 * @return Retorna la función con los parámetros
 */
def calcular(f:(Double,Double)=>Double,valorA:Double,valorB:Double) = f(valorA,valorB)
/**
 * Se calcula el salario
 * @param Double devengado
 * @param Double deducciones
 * @return Retorna el valor del salario
 */
val calSalario = (devengado:Double,deducciones:Double) => { devengado - deducciones }

calcular(calSalario,15000,4500)
```
### Ejercicio 4

```scala
/**
 * Se calcula el bono del salario
 * @param Double devengado
 * @param Double deducciones
 * @return Retorna el valor del salario con el bono
 */
val calSalarioBono = (devengado:Double,deducciones:Double) => { devengado * 1.10 - deducciones }

calSalarioBono(15000,4500)
```
### Ejercicio 5

```scala
/**
 * Función que retorna otra función
 * @param Function Nombre de la función
 * @param Double devengado
 * @param Double deducciones
 * @return Retorna una función con los dos parámetros
 */
def compSalario(f:(Double,Double)=>Double,devengado:Double,deducciones:Double) = f(devengado,deducciones)

compSalario(calSalario,1000,34) //Calculamos salario

compSalario(calSalarioBono,1000,34) //Calculamos salario + bono
```
### Ejercicio 6

```scala
/**
 * Función que genera otra función para computar bonos
 * @param Double bono
 * @return Retorna el calculo junto con el valor del bono
 */
def genCalSalarioBono(bono:Double):(Double,Double) => Double = (devengado:Double,deduccion:Double) => {devengado * bono - deduccion}
```
### Ejercicio 7

```scala
/**
 * Función que genera un bono del 5%
 */
val calSalario5 = genCalSalarioBono(1.05) 

calSalario5(1000,300)
```
### Ejercicio 8
```scala
/**
 * Función que genera un bono del 20%
 */
val calSalario20 = genCalSalarioBono(1.20) 

calSalario20(1000,300)
```
---
## Clausuras
### Ejercicio 9
```scala
val bono = 1.15
/**
 * Función que calcula salario + bono
 * @param Double devengado
 * @param Double deduccion
 * @return Retorna el salario con bono (el bono se declara externamente)
 */
def calSalarioBonoClausura(devengado:Double,deduccion:Double) = {devengado * bono - deducciones }

```
### Ejercicio 10
```scala
val bono = 1.15

compSalario(calSalarioBonoClausura,1222,12)

compSalario(calSalarioBonoClausura,5000,500)
```
---
## Funciones aplicadas parcialmente
### Ejercicio 11
```scala
/**
 * A traves de genCalSalarioBono se obtiene un bono del 15%
 */
val tmp = genCalSalarioBono(_)

val calSalario15 = tmp(1.15)

calSalario15(2000,150)
```
### Ejercicio 12
```scala
/**
 * A traves de genCalSalarioBono se obtiene un bono del 2%
 */
val tmp = genCalSalarioBono(_)

val calSalario100 = tmp(1.02)

calSalario100(2000,150)
```
---
## Recursividad
### Ejercicio 15
Función Factorial
```scala
/**
 * Función que calcula el factorial
 * @param Int n
 * @return Retorna el factorial de un número
 */
def factorial(n:Int):Int = n match {
    case 0 => 1
    case 1 => 1
    case _ => n * factorial(n-1)
}

factorial(5)
```
### Ejercicio 16
```scala
/**
 * Función que calcula la serie fibonacci de un número
 * @param Int n 
 * @return Retorna el cálculo de la serie
 */
def fibonacci(n:Int):Int = n match {
    case 0 => 0
    case 1 => 1
    case _ => fibonacci(n-1) + fibonacci(n-2)
}

fibonacci(5)
```
### Ejercicio 17
Factorial con recursividad de cola
```scala
/**
 * Función que calcula el factorial de un número usando recursividad de cola, está conformado por otra función interna
 * @param Int n 
 * @return Retorna el factorial
 */
def factorial(n:Int):Int = {
   /**
    * Función que calcula el factorial teniendo en cuenta el acumulador
    * @param Int n 
    * @param Int acumulador 
    * @return Retorna el factorial en memoria
    */
    @annotation.tailrec
    def factorialInterno(n:Int,acumulador:Int):Int = n match {
        case 0 => acumulador
        case 1 => acumulador
        case n => factorialInterno(n-1,n*acumulador)
    }
    factorialInterno(n,1)
}

factorial(5)
```
