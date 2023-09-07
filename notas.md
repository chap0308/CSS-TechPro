## Colocar un atributo más al img:
```bash
img {
    max-width: 100%;
    display: block;
    height: auto;/*! auto o 100%, con esto arreglamos el tamaño de las imagenes */
}
```
## line-height: Otro factor de separacion entre etiquetas, es diferente al padding y al margin.
Lo quitamos colocando el que mejor se ajuste:
```bash
line-height: 1;
line-height: 0;
```
## Tener en cuenta sobre background-image y background-color: background-repeat, background-position, background-size solo se aplicarán a background-image
```bash
<div class="modelo modelo-x">
    <h3>TechPRO X</h3>
    <p class="precio">$299</p>
</div>
```
Si background-image y sus estilos están en diferentes clases. No habrá ningun problema, igualmente los tomará. Pero recuerda que background-color no depende de los otros.
```bash
.modelo {
    background-color: var(--grisClaro);
    background-repeat: no-repeat;
    background-position: 90% center;
    background-size: 15rem;
}

.modelo-x {
    background-image: url(../img/modelo-x.svg);
}
```
## background-clip: esto hace que pase el contenido del background(imagen, color, etc) al texto. Se necesitan los dos.
```bash
-webkit-background-clip: text;/*! necesita del prefijo "-webkit-" para que funcione */
background-clip: text;
```
## Nota sobre linear-gradient.
```bash
- normalmente: linear-gradient( to bottom, transparent 50%, var(--primario) 50%, (--primario) 100% )
- tambien se puede: linear-gradient( to bottom, transparent 50%, var(--primario) 0% )
```
Por qué 0%? Colocarle al 0% significa que le colocamos a todo el div el color azul, pero como tiene un degradado, mientras siga aumentando tendrá el color más fuerte. Pero en este caso, tenemos que el transparent es hasta el 50% y lo demás será el degradado del color azul

## De flex a grid: No se necesita colocar primero unset y luego el grid
```bash
.listado-modelos {
    display: flex;
    flex-direction: column-reverse;
}

@media (min-width: 992px) { 
    .listado-modelos {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        grid-template-rows: repeat(2, 20rem);
        gap: 4rem;
    }
}
```
## Animacion: Se usa transition-property para elegir los estilos QUE QUEREMOS ANIMAR.
La diferencia principal entre que si colocamos el estilo o no, es que no será animado. Sí aparecerá el efecto, pero será instantáneo; no de manera animada.
```bash
.modelo {
    transition-property: transform background-size;
    transition-duration: .3s;
}
.modelo:hover {
    transform: scale(1.1) rotate(8deg);
    background-size: 30rem;
    background-color: red;
}
```
## Forma corta de usar transition
```bash
.modelo {
    transition: transform 300ms, background-size 300ms;
}
.modelo:hover {
    transform: scale(1.1) rotate(8deg);
    background-size: 30rem;
    background-color: red;
}
```
## Nota sobre background-position:
Los valores deben ser colocados de x a y, pero si colocas primero un valor como top y luego left; automaticamente se colocaran en sus respectivas posiciones.
```bash
background-position: center, top left;
```
Pero si colocas algo como top top. Generará un error.
```bash
background-position: center, top top;
```
## Usar siempre: todos los submits tienen border, por eso lo quitamos.
![Alt text](usar-esto.PNG)
```bash
.formulario input[type="submit"] {
    border: none;/*! none o unset */
}
```
## El script hará que se vea en la primera linea del html de la consola esta clase: class=" avif webp notjxl notjpx notjp2". Esto indicará que extensiones soporta el navegador, las que comiencen con "not" no serán soportadas. Por eso, hacemos las siguientes clases:
![Alt text](script.PNG)

Si el navegador no es compatible con avif ni con webp, entonces se usará .jpg
```bash
.notavif.notwebp .newsletter {
    background-image: linear-gradient( to bottom, transparent 50%, var(--blanco) 0% ), url(../img/newsletter.jpg) ;
}
```
Si es compatible con webp entonces usaremos webp, pero en segunda opcion, ya que como css es en cascada tomará el siguiente valor
```bash
.webp .newsletter {
    background-image: linear-gradient( to bottom, transparent 50%, var(--blanco) 0% ), url(../img/newsletter.webp) ;
}
```
Si es compatible con avif se usará como primera opcion este:
```bash
.avif .newsletter {
    background-image: linear-gradient( to bottom, transparent 50%, var(--blanco) 0% ), url(../img/newsletter.avif) ;
}
```