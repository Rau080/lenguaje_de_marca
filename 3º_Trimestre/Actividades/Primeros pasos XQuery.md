# XQuery

## Actividad XML - XQuery 1.
Ejercicio 1

Dado el siguiente documento XML realiza las siguientes consultas con XQuery:

```
<?xml version="1.0" encoding="UTF-8"?>
<bookstore>
  <book category="COOKING">
    <title lang="en">Everyday Italian</title>
    <author>Giada De Laurentiis</author>
    <year>2005</year>
    <price>30.00</price>
  </book>
  <book category="CHILDREN">
    <title lang="en">Harry Potter</title>
    <author>J K. Rowling</author>
    <year>2005</year>
    <price>29.99</price>
  </book>
  <book category="WEB">
    <title lang="en">XQuery Kick Start</title>
    <author>James McGovern</author>
    <author>Per Bothner</author>
    <author>Kurt Cagle</author>
    <author>James Linn</author>
    <author>Vaidyanathan Nagarajan</author>
    <year>2003</year>
    <price>49.99</price>
  </book>
  <book category="WEB">
    <title lang="en">Learning XML</title>
    <author>Erik T. Ray</author>
    <year>2003</year>
    <price>39.95</price>
  </book>
</bookstore> 
```

1.Mostrar los títulos de los libros con la etiqueta "titulo"

```
for $book in /bookstore/book
return $book/title/text()
```

2.Mostrar los libros cuyo precio sea menor o igual a 30. Primero incluyendo la condición en la cláusula "where" y luego en la ruta del XPath.

for $book in /bookstore/book
where $book/price <= 30
return $book

3.Mostrar sólo el título de los libros cuyo precio sea menor o igual a 30.

for $book in /bookstore/book
where $book/price <= 30
return $book/title/text()

4.Mostrar sólo el título sin atributos de los libros cuyo precio sea menor o igual a 30.

for $book in /bookstore/book
where $book/price <= 30
return $book/title/text()

5.Mostrar el título y el autor de los libros del año 2005, y etiquetar cada uno de ellos con "lib2005".

for $book in /bookstore/book
where $book/year = 2005
return <lib2005>{$book/title}{$book/author}</lib2005>

6.Mostrar los años de publicación, primero con "for" y luego con "let" para comprobar la diferencia entre ellos. Etiquetar la salida con "publicacion".

for $book in /bookstore/book
return <publicacion>{$book/year}</publicacion>

let $book := /bookstore/book
return <publicacion>{$book/year}</publicacion>

7.Mostrar los libros ordenados primero por "category" y luego por "title" en una sola consulta.

for $book in /bookstore/book
order by $book/@category,$book/title
return $book

8.Mostrar cuántos libros hay, y etiquetarlo con "total".

for $book in count(/bookstore/book)
return <tolal>{$book}</tolal>

9.Mostrar los títulos de los libros y al final una etiqueta con el número total de libros.

let $contar := count (/bookstore/book),
    $titulo := (
      for $book in /bookstore/book/title 
      return <titulo>{$book/text()}</titulo>) 
return 
      <resultado>
        {$titulo}
        <total>{$contar}</total>
      </resultado>

10.Mostrar el precio mínimo y máximo de los libros.

for $min in min(/bookstore/book/price)
  return $min

for $max in max(/bookstore/book/price)
  return $max

11.Mostrar el título del libro, su precio y su precio con el IVA incluido, cada uno con su propia etiqueta. Ordénalos por precio con IVA.

for $titulo in /bookstore/book
let $iva := ($titulo/price*1.21)
order by $iva
   return <result>
          <titulo>{$titulo/title/text()}</titulo>
          <precio>{$titulo/price/text()}</precio>
          <result_iva>{$iva}</result_iva>
          </result>

12.Mostrar la suma total de los precios de los libros con la etiqueta "total".

for $titulo in sum(/bookstore/book/price)
   return <total>{$titulo}</total>

13.Mostrar cada uno de los precios de los libros, y al final una nueva etiqueta con la suma de los precios.

<libro>
{for $titulo in /bookstore/book
return $titulo/price}

{let $precio := sum(/bookstore/book/price)
return <total>{$precio}</total>}
</libro>

14.Mostrar el título y el número de autores que tiene cada título en etiquetas diferentes.

for $titulo in /bookstore/book
return <libro>
       <titulo>{$titulo/title/text()}</titulo>
       <autor>{count($titulo/author)}</autor>
       </libro>

15.Mostrar en la misma etiqueta el título y entre paréntesis el número de autores que tiene ese título.

for $titulo in /bookstore/book
return <libro>
       {$titulo/title/text()}
       ({count($titulo/author)})
       </libro>s

16.Mostrar los libros escritos en años que terminen en "3".

for $titulo in /bookstore/book
where matches($titulo/year, "3$")
return $titulo

17.Mostrar los libros cuya categoría empiece por "C".`

for $titulo in /bookstore/book
where matches($titulo/@category, "^C")
return $titulo

18.Mostrar los libros que tengan una "X" mayúscula o minúscula en el título.

for $titulo in /bookstore/book
where contains($titulo/title, "X") or contains($titulo/title, "x") order by $titulo/title descending
return $titulo

19.Mostrar el título y el número de caracteres que tiene cada título, cada uno con su propia etiqueta.

for $titulo in /bookstore/book
return <libro>
          {$titulo/title}
          <str_contar>{string-length($titulo/title)}</str_contar>
        </libro>

20.Mostrar todos los años en los que se ha publicado un libro eliminando los repetidos. Etiquétalos con "año".

for $titulo in distinct-values(/bookstore/book/year)
return <año>{$titulo}</año>

21.Mostrar todos los autores eliminando los que se repiten y ordenados por el número de caracteres que tiene cada autor.

for $titulo in distinct-values(/bookstore/book/author)
order by string-length($titulo)
return <autor>{$titulo}</autor

22.Mostrar los títulos en una tabla de HTML.

<table>
{for $libro in /bookstore/book
  return <tr><td>{$libro/title/text()}</td></tr>}
</table>