# Actividad XML - XQuery 2.
## Ejercicio 2

Dado el siguiente documento XML realiza las siguientes consultas con XQuery:

```
<?xml version="1.0" encoding="UTF-8"?>
<videojuego>
  <titulo>Valorant</titulo>
  <genero>Juego de disparos en primera persona</genero>
  <plataforma>PC</plataforma>
  <desarrollador>Riot Games</desarrollador>
  <fechaLanzamiento>2 de junio de 2020</fechaLanzamiento>
  <agentes>
    <agente>
      <nombre>Jett</nombre>
      <habilidadPrimaria tipo="Daño" duracion="4s">Cuchillo Arrojadizo</habilidadPrimaria>
      <habilidadSecundaria tipo="Curación" duracion="0s">Vientos Ligeros</habilidadSecundaria>
      <habilidadUltimate tipo="Daño" duracion="6s">Tormenta de Cuchillos</habilidadUltimate>
    </agente>
    <agente>
      <nombre>Brimstone</nombre>
      <habilidadPrimaria tipo="Daño" duracion="6s">Granada Incendiaria</habilidadPrimaria>
      <habilidadSecundaria tipo="Curación" duracion="0s">Estímulo de Combate</habilidadSecundaria>
      <habilidadUltimate tipo="Daño" duracion="4s">Incendiario Orbital</habilidadUltimate>
    </agente>
    <agente>
      <nombre>Viper</nombre>
      <habilidadPrimaria tipo="Daño" duracion="8s">Nube Venenosa</habilidadPrimaria>
      <habilidadSecundaria tipo="Daño" duracion="6s">Pantalla Tóxica</habilidadSecundaria>
      <habilidadUltimate tipo="Curación" duracion="12s">Recolección Táctica</habilidadUltimate>
    </agente>
    <agente>
      <nombre>Phoenix</nombre>
      <habilidadPrimaria tipo="Daño" duracion="4s">Bola Curva de Fuego</habilidadPrimaria>
      <habilidadSecundaria tipo="Curación" duracion="0s">Escudo Curativo</habilidadSecundaria>
      <habilidadUltimate tipo="Daño" duracion="6s">Explosión Cósmica</habilidadUltimate>
    </agente>
    <agente>
      <nombre>Sage</nombre>
      <habilidadPrimaria tipo="Curación" duracion="0s">Orbe de Curación</habilidadPrimaria>
      <habilidadSecundaria tipo="Daño" duracion="4s">Muro de Hielo</habilidadSecundaria>
      <habilidadUltimate tipo="Curación" duracion="5s">Resurrección</habilidadUltimate>
    </agente>
    <agente>
      <nombre>Cypher</nombre>
      <habilidadPrimaria tipo="Daño" duracion="4s">Trampa Cibernética</habilidadPrimaria>
      <habilidadSecundaria tipo="Daño" duracion="7s">Cámara Espía</habilidadSecundaria>
      <habilidadUltimate tipo="Curación" duracion="0s">Ataque de Neurona</habilidadUltimate>
    </agente>
  </agentes>
</videojuego>
``` 

1. Muestra el título del videojuego.
```
let $juego := /videojuego/titulo
return $juego/text()
```
2. Muestra la plataforma del videojuego.
```
let $juego := /videojuego/plataforma
return $juego/text()
```
3. Muestra el nombre de todos los agentes.
```
let $juego := /videojuego/agentes/agente/nombre
return $juego/text()
```
4. Muestra el nombre y la habilidad ultimate de todos los agentes.
```
for $juego in /videojuego/agentes/agente
return <habilidades>
        <nombre>{$juego/nombre/text()}</nombre>
        <ultimate>{$juego/habilidadUltimate/text()}</ultimate>
       </habilidades>
```
5. Muestra los nombres de los agentes cuya habilidad primaria es "Incendiario".
```
for $juego in /videojuego/agentes/agente
where matches($juego/habilidadPrimaria, "Incendiaria")
return <habilidades>
         <nombre>{$juego/nombre/text()}</nombre>
         <primaria>{$juego/habilidadPrimaria/text()}</primaria>
       </habilidades>
```
6. Muestra los nombres de los agentes cuya habilidad ultimate es "Fénix".
```
for $juego in /videojuego/agentes/agente
where matches($juego/habilidadUltimate, "Fénix")
return <habilidades>
         <nombre>{$juego/nombre/text()}</nombre>
         <ultimate>{$juego/habilidadUltimate/text()}</ultimate>
       </habilidades>
```
7. Muestra las habilidades primarias de los agentes cuyo nombre empieza por "J".
```
for $juego in /videojuego/agentes/agente
where matches($juego/nombre, "^J")
return <habilidades>
         <nombre>{$juego/nombre/text()}</nombre>
         <primaria>{$juego/habilidadPrimaria/text()}</primaria>
       </habilidades>
```
8. Muestra los nombres de los agentes cuyas habilidades primarias empiezan por "Bola".
```
for $juego in /videojuego/agentes/agente
where matches($juego/habilidadPrimaria, "^Bola")
return <habilidades>
         <nombre>{$juego/nombre/text()}</nombre>
         <primaria>{$juego/habilidadPrimaria/text()}</primaria>
       </habilidades>
```
9. Muestra los nombres de todos los agentes en orden alfabético.
```
for $juego in /videojuego/agentes/agente
order by $juego/nombre
return $juego/nombre/text()
         
```
10. Muestra las habilidades primarias y secundarias de los agentes cuyo nombre contiene la letra "y".
```
for $juego in /videojuego/agentes/agente
where matches($juego/nombre, "y")
return <habilidades>
         <primaria>{$juego/habilidadPrimaria/text()}</primaria>
         <secundaria>{$juego/habilidadSecundaria/text()}</secundaria>
       </habilidades>
```
11. Muestra los nombres de los agentes cuya habilidad ultimate contiene la palabra "cuchillos".
```
for $juego in /videojuego/agentes/agente
where matches($juego/habilidadUltimate, "Cuchillos")
return $juego/nombre/text()
```
12. Muestra las habilidades primarias de los agentes cuyo nombre contiene la letra "o" y la habilidad secundaria contiene la palabra "humo".
```
for $juego in /videojuego/agentes/agente
where matches($juego/habilidadSecundaria, "humo") or matches($juego/nombre, "o")

return $juego/habilidadPrimaria/text()
```
13. Muestra los nombres de los agentes que tienen exactamente tres habilidades.
```
for $juego in /videojuego/agentes/agente
where $juego/habilidadPrimaria or $juego/habilidadSecundaria or $juego/habilidadUltimate

return $juego/nombre/text()
```
14. Muestra los nombres de los agentes cuya habilidad secundaria no es "Granada Cegadora".
```

```
15. Muestra las habilidades primarias de los agentes cuyos nombres no contienen la letra "e".
```

```
16. Muestra los nombres de los agentes cuyas habilidades primarias contienen la palabra "muro" o la palabra "barrera".
```
for $juego in /videojuego/agentes/agente
where matches($juego/habilidadPrimaria, "Muro") or matches($juego/habilidadPrimaria, "barrera") 

return $juego/nombre/text()
```
17. Muestra las habilidades ultimates de los agentes en orden alfabético inverso.
```
for $juego in /videojuego/agentes/agente
order by nombre descending
return $juego/habilidadUltimate/text()
```
18. Muestra los nombres de los agentes cuya habilidad ultimate tiene una duración mayor a 8 segundos.
```
for $juego in /videojuego/agentes/agente
where $juego/habilidadUltimate/@duracion="8s"
return $juego/nombre/text()
```
19. Muestra el nombre del agente con la habilidad ultimate más corta.
```

```
20. Muestra los nombres de los agentes que tienen habilidades primarias y secundarias con la misma duración.
```

```
21. Muestra el nombre de los agentes que tienen habilidades primarias y secundarias que pertenecen al mismo tipo.
```

```
22. Muestra los nombres de los agentes cuyas habilidades primarias son de tipo "Daño" y sus habilidades secundarias son de tipo "Curación".
```

```
23. Muestra los nombres de los agentes que tienen habilidades primarias y secundarias que contienen la misma palabra.
```

```