# Practica de Git, GitHub y SourceTree
----------

1. **¿Qué comando utilizaste en el paso 11? ¿Por qué?**
	
	```
	git reset --hard HEAD~1
	```
	 Empleo este comando por que es el unico que permite mover el puntero de la rama donde estoy al punto donde quiera. Empleando el atriburo *--hard* me permite modificar el *working copy*. **HEAD~1** Me permite restar un commit a la posición **HEAD**. En resumen este comando me permite mover el puntero **HEAD** y el puntero de la rama a una posicion predeterminada en este caso la posición del **HEAD-1**. 

2. **¿Qué comando o comandos utilizaste en el paso 12? ¿Por qué?**
	
	Para poder recuperar los cambios que hemos deshecho. Es necesario recuperar el hash del ultimo commit. Cada commit tiene un hash SHA1 que lo identifica de forma unica. Para ello primeramente he empleado el comando:
	
	```
	git reflog
	```
	Mediante este comando vemos todas las acciones que se hemos realizado sobre nuestro repositorio local, para recuperar el ultimo commit. 
	> c6649dd HEAD@{0}: reset: moving to HEAD~1 
	
	> 277f84d HEAD@{1}: commit: Htmlify
	
	> c6649dd HEAD@{2}: checkout: moving from master to htmlify
	
	> c6649dd HEAD@{3}: commit (initial): Añadido poem
	
	Podemos ver que el hemos realizado sobre el repositorio. Podemos ver el hash (corto) del commit de haber modificado el poem.md y cambiado el color por las etiquetas *HTML*. 
	
	```
	git reset --hard 277f84d
	```
	El comando reset aparte de adminitir posiciones sobre **HEAD** también admite hash.

3. **El merge del paso 13, ¿Causó algún conflicto? ¿Por qué?**

	No causa ningún conflicto al realizar el comando:
	
	```
	git merge master 
	```
	El porque no causa ningún error es que no se puede hacer un merge de **htmlify** a **master** ya que **htmlify** ya contine lo que tiene **master** por eso el mensaje que sale es:
	
	> Already up-to-date.
	
	**htmlify** esta más avanzada y contiene los *Hunks* de la rama **master**

4. **El merge del paso 19, ¿Causó algún conflicto? ¿Por qué?**

	Al ejecutar el paso 19, el cual se resuelve con el comando:
	
	```
	git merge matrix
	```
	
	Si generan conflictos, aunque git es bastante inteligente a la hora de crear y eliminar filas, no es capaz de hacerlo cuando se modifican en las dos ramas las mismas lineas, por esa razón debemos modificar los conflictos a mano. En este estado Git se queda realizando el merge a la espare que hagamos un commit con los cambios resueltos. 

5. **El merge del paso 21, ¿Causó algún conflicto? ¿Por qué?**

	Al ejecutar el comando

	```	
	git merge htmlify
	```
	No causa ningun conflicto ya que el merge que esta realizando es un *fast forward* quiere decir que el grafo de git se puede simplificar en una lista, por lo tanto para realizar el *merge* lo unico que debemos hacer es mover la *branch* de master a htmlify, quedando master y htmlify en el mismo *commit* 

6. **¿Qué comando o comandos utilizaste en el paso 25?**

	El diagrama que he salido por pantalla es el siguiente:
	<pre>
	·   31adfc2863d7fc4d430450646651befc6d226873 (HEAD -> master, htmlify) Merge branch 'matrix' into htmlify
	|\
	| · 895117abd3782a24e6fdd6830711acb90a1e282f (matrix) Modificado poem para matrix
	· | 277f84da5f0221713c2f18593f5700d08dc51c09 Htmlify
	|/
	· c6649dd4c05f8e485f7703eb602a2ab869beb9b3 Añadido poem
	</pre>
	
	Primeramente he añadido un alias, dicho alias me permite un comando de git ejecutar un comando mas complejo, para añadir un alias debemos realizar el siguiente comando:
	
	```
	git config alias.graph "log --graph --decorate --pretty=oneline"
	```
	La descripción del contenido del git que se añade a la configuración un nuevo alias, que es nombrado **graph** y que es el comando git **log --graph --decorate --pretty=oneline** 
	
	Una vez que hemos ejecutado el comando debemos ejecutar el comando: 
	
	```
	git graph
	```
	Para que nos aparezca la otra información. 

7. **El merge del paso 26, ¿Podría ser fast forward? ¿Por qué?**

	Si podria ser *fast forward*, la razon de ello es que se pueden traducir el grafo de git como una lista. Solo añadiendo los *hunks* del title quedaria modificado el head. 
	
	<pre>
	·   79bf1ba0377ee3c44b200ed962480bbdf9de992c (HEAD -> master) Merge branch 'title'
	|\
	| · 7884d58c33065284517d4f07118bd79a6b0e6445 (title) Añado titulo al poema
	|/
	·   31adfc2863d7fc4d430450646651befc6d226873 (htmlify) Merge branch 'matrix' into htmlify
	|\
	| · 895117abd3782a24e6fdd6830711acb90a1e282f (matrix) Modificado poem para matrix
	· | 277f84da5f0221713c2f18593f5700d08dc51c09 Htmlify
	|/
	· c6649dd4c05f8e485f7703eb602a2ab869beb9b3 Añadido poem
	</pre>
	
	Podemos ver que realizando el comando
	
	```
	git merge title
	```
	
	Git realizaria el siguiente proceso y quedaria este grafo el cual esta realizado de manera fast forward:
	<pre>
	· 7884d58c33065284517d4f07118bd79a6b0e6445 (HEAD -> master,title) Añado titulo al poema
	|
	·   31adfc2863d7fc4d430450646651befc6d226873 (htmlify) Merge branch 'matrix' into htmlify
	|\
	| · 895117abd3782a24e6fdd6830711acb90a1e282f (matrix) Modificado poem para matrix
	· | 277f84da5f0221713c2f18593f5700d08dc51c09 Htmlify
	|/
	· c6649dd4c05f8e485f7703eb602a2ab869beb9b3 Añadido poem
	</pre>
	
8. **¿Qué comando o comandos utilizaste en el paso 27?**

	Para deshacer el merge tenemos que realizar un *git reset* exactamente:
	
	```
	git reset HEAD~1
	```
	
	En este paso debemos obiar el parametro *--hard* por que queremos mantener el los cambios del *working copy*. El comando es *HEAD~1* por que sin nos fijamos en el grafo debemos reducir el paso anterior
	<pre>
	·   79bf1ba0377ee3c44b200ed962480bbdf9de992c (HEAD -> master) Merge branch 'title'
	|\
	| · 7884d58c33065284517d4f07118bd79a6b0e6445 (title) Añado titulo al poema
	|/
	·   31adfc2863d7fc4d430450646651befc6d226873 (htmlify) Merge branch 'matrix' into htmlify
	|\
	| · 895117abd3782a24e6fdd6830711acb90a1e282f (matrix) Modificado poem para matrix
	· | 277f84da5f0221713c2f18593f5700d08dc51c09 Htmlify
	|/
	· c6649dd4c05f8e485f7703eb602a2ab869beb9b3 Añadido poem
	</pre>
	
	Para quedar de la siguiente manera:
	
	<pre>
	·   31adfc2863d7fc4d430450646651befc6d226873 (HEAD -> master,htmlify) Merge branch 'matrix' into htmlify
	|\
	| · 895117abd3782a24e6fdd6830711acb90a1e282f (matrix) Modificado poem para matrix
	· | 277f84da5f0221713c2f18593f5700d08dc51c09 Htmlify
	|/
	· c6649dd4c05f8e485f7703eb602a2ab869beb9b3 Añadido poem
	</pre>
	
	Como seguimos en la rama **master**, no podemos ver la rama **title** por esa razón el grafo queda de la forma de arriba.
	
9. **¿Qué comando o comandos utilizaste en el paso 28?**

	Para descartar los cambios podemos realizar dos formas diferentes:
	
	1. Podemos realizar un *reset* de la rama actual con el parametro *--hard*. 
		
		```
		git reset --hard HEAD
		```
		Este comando restaurara todos los ficheros y dejara el *working copy* como estuviera en el repositorio.
		
	2. Podemos realizar un *checkout* de cada archivo que queramos para poder descartar los cambios.  
		
		```
		git checkout -- poem.md
		```		
		Este comando permite devolver cada uno de los archivos de forma independiente el estado en el cual estuviera en el repositorio. 

10. **¿Qué comando o comandos utilizaste en el paso 29?**

	El comando para eliminar la rama es el siguiente:
	
	```
	git branch -D title
	```
	
	Dicho comando borra la rama, pero no es un borrado normal sino un borrado forzoso ya que si se realia este comando con el parametro *-d* no borrara la rama por que no esta mergueada y podriamos perder datos.

11. **¿Qué comando o comandos utilizaste en el paso 30?**

	Primeramente necesitamos realizar un comando para ver que hemos hecho sobre el repositorio. Para ello debemos ejecutar el comando:
	
	```
	git reflog
	```
	Este comando permite mirar las acciones realizadas sobre el repositorio:
	
	<pre>
	31adfc2 HEAD@{0}: reset: moving to HEAD~1
	79bf1ba HEAD@{1}: merge title: Merge made by the 'recursive' strategy.
	31adfc2 HEAD@{4}: checkout: moving from title to master
	7884d58 HEAD@{5}: commit: Añado titulo al poema
	31adfc2 HEAD@{6}: checkout: moving from master to title
	31adfc2 HEAD@{7}: merge htmlify: Fast-forward
	c6649dd HEAD@{8}: checkout: moving from htmlify to master
	31adfc2 HEAD@{9}: commit (merge): Merge branch 'matrix' into htmlify
	277f84d HEAD@{10}: checkout: moving from matrix to htmlify
	895117a HEAD@{11}: commit: Modificado poem para matrix
	c6649dd HEAD@{12}: checkout: moving from master to matrix
	c6649dd HEAD@{13}: checkout: moving from htmlify to master
	277f84d HEAD@{14}: reset: moving to 277f84d
	c6649dd HEAD@{15}: reset: moving to HEAD~1
	277f84d HEAD@{16}: commit: Htmlify
	c6649dd HEAD@{17}: checkout: moving from master to htmlify
	c6649dd HEAD@{18}: commit (initial): Añadido poem
	</pre>
	
	Estas son las acciones realizadas sobre el repositorio, como podemos ver las acciones interesantes para recuperar el *merge* del title es el siguiente:
	
	> 79bf1ba HEAD@{1}: merge title: Merge made by the 'recursive' strategy.
	
	Si despues ejecutamos el comando *reset* y movernos a dicho commit.
	
	```
	git reset --hard 79bf1ba
	```  
	Una vez realizado el comando podemos ver como en el grafo se muestra el estado anterior sin mantener la branch **title**:
	
	<pre>
	·   79bf1ba0377ee3c44b200ed962480bbdf9de992c (HEAD -> master) Merge branch 'title'
	|\
	| · 7884d58c33065284517d4f07118bd79a6b0e6445 Añado titulo al poema
	|/
	·   31adfc2863d7fc4d430450646651befc6d226873 (htmlify) Merge branch 'matrix' into htmlify
	|\
	| · 895117abd3782a24e6fdd6830711acb90a1e282f (matrix) Modificado poem para matrix
	· | 277f84da5f0221713c2f18593f5700d08dc51c09 Htmlify
	|/
	· c6649dd4c05f8e485f7703eb602a2ab869beb9b3 Añadido poem
	</pre>
	
12. **¿Qué comando o comandos usaste en el paso 32?**

	Para volver al commit inicial debemos realizar un *reset* y movernos a la primera posición para ello debemos ejecutar el comando:
	
	```
	git log
	```
	
	Con el resultado del comando es el siguiente:
	
	<pre>
	commit 79bf1ba0377ee3c44b200ed962480bbdf9de992c
	Merge: 31adfc2 7884d58
	Author: Adrian Polo Alcaide <“a.whole.dev@gmail.com”>
	Date:   Tue Sep 8 23:25:34 2015 +0200

    	Merge branch 'title'

	commit 7884d58c33065284517d4f07118bd79a6b0e6445
	Author: Adrian Polo Alcaide <“a.whole.dev@gmail.com”>
	Date:   Tue Sep 8 23:08:40 2015 +0200

   		Añado titulo al poema

	commit 31adfc2863d7fc4d430450646651befc6d226873
	Merge: 277f84d 895117a
	Author: Adrian Polo Alcaide <“a.whole.dev@gmail.com”>
	Date:   Tue Sep 8 23:03:14 2015 +0200

    	Merge branch 'matrix' into htmlify

     	Conflicts:
        	poem.md: Nos quedamos con la parte de htmlify

	commit 895117abd3782a24e6fdd6830711acb90a1e282f
	Author: Adrian Polo Alcaide <“a.whole.dev@gmail.com”>
	Date:   Tue Sep 8 22:57:15 2015 +0200

    	Modificado poem para matrix

	commit 277f84da5f0221713c2f18593f5700d08dc51c09
	Author: Adrian Polo Alcaide <“a.whole.dev@gmail.com”>
	Date:   Tue Sep 8 21:40:45 2015 +0200

    	Htmlify

	commit c6649dd4c05f8e485f7703eb602a2ab869beb9b3
	Author: Adrian Polo Alcaide <“a.whole.dev@gmail.com”>
	Date:   Tue Sep 8 21:38:24 2015 +0200

    	Añadido poem
	</pre>

	Si queremos volver al primer estado deberemos realizar el comando *reset* con el parametro *--hard*
	
	```
	git reset --hard c6649dd4c05f8e485f7703eb602a2ab869beb9b3
	```
	
	Mediante el comando que hemos realizado ya nos permite estar en la posición deseada, como se muestra en el grafo a continuación:
	
	<pre>
	· c6649dd4c05f8e485f7703eb602a2ab869beb9b3 (HEAD -> master) Añadido poem
	</pre>


13. **¿Qué comando o comandos usaste en el punto 33?**

	Primeramente debemos conocer los hash, primeramente debemos el log. Para ello empleamos el comando: 
	
	```
	git reflog
	```
	Los datos que me aparecen los siguientes:
	
	```
	c6649dd HEAD@{0}: reset: moving to c6649dd4c05f8e485f7703eb602a2ab869beb9b3
	79bf1ba HEAD@{1}: reset: moving to 79bf1ba
	31adfc2 HEAD@{2}: reset: moving to HEAD~1
	79bf1ba HEAD@{3}: merge title: Merge made by the 'recursive' strategy.
	31adfc2 HEAD@{6}: checkout: moving from title to master
	7884d58 HEAD@{7}: commit: Añado titulo al poema
	31adfc2 HEAD@{8}: checkout: moving from master to title
	31adfc2 HEAD@{9}: merge htmlify: Fast-forward
	c6649dd HEAD@{10}: checkout: moving from htmlify to master
	31adfc2 HEAD@{11}: commit (merge): Merge branch 'matrix' into htmlify
	277f84d HEAD@{12}: checkout: moving from matrix to htmlify
	895117a HEAD@{13}: commit: Modificado poem para matrix
	c6649dd HEAD@{14}: checkout: moving from master to matrix
	c6649dd HEAD@{15}: checkout: moving from htmlify to master
	277f84d HEAD@{16}: reset: moving to 277f84d
	c6649dd HEAD@{17}: reset: moving to HEAD~1
	277f84d HEAD@{18}: commit: Htmlify
	c6649dd HEAD@{19}: checkout: moving from master to htmlify
	c6649dd HEAD@{20}: commit (initial): Añadido poem
	```
	
	Una vez realizado debemos emplear logica para descubrir en que accion debemos recuperar, si miramos el log podemos ver que nos hemos movidocuando hemos empleado el merge era el hash **79bf1ba**, por esa razón una vez realizado el *reset* a dicha posicion tendremos el estado anterior: 
	
	```
	git reset --hard 79bf1ba
	```
	
	Debemos añadir el comando *--hard* ya que se debe actualizar el *working directory*.
	