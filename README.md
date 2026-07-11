# psicolumen1

Guia para instalar, ejecutar y probar este proyecto Jekyll.

## Requisitos

- Linux (probado en entorno Linux)
- Ruby 3.1+ (recomendado 3.2, acorde a vendor/bundle del proyecto)
- RubyGems (incluido con Ruby)
- Bundler

Verifica versiones:

	ruby -v
	gem -v
	bundle -v

Si Bundler no esta instalado:

	gem install bundler

## Instalacion del proyecto

Desde la carpeta del proyecto:

	cd /home/marti/proy/jekyll/psicolumen1

Instala dependencias del Gemfile:

	bundle install

Opcional: instalar gems dentro del proyecto para no usar rutas globales:

	bundle config set --local path vendor/bundle
	bundle install

## Ejecutar en local (modo desarrollo)

Inicia el servidor Jekyll:

	bundle exec jekyll serve --livereload

Abre en navegador:

	http://127.0.0.1:4000/

Para detener el servidor, presiona Ctrl+C.

## Build de produccion

Genera el sitio estatico en _site:

	bundle exec jekyll build

Salida esperada:

- Carpeta _site actualizada
- Sin errores en consola

## Pruebas recomendadas

Este proyecto no incluye tests unitarios por defecto, pero puedes validar la integridad del sitio con estas pruebas.

### 1) Validacion de configuracion y contenido

	bundle exec jekyll doctor

Debe terminar sin errores criticos.

### 2) Prueba de compilacion limpia

	bundle exec jekyll clean
	bundle exec jekyll build

Debe compilar sin errores.

### 3) Smoke test en local

Con el servidor activo, prueba endpoints principales:

	curl -I http://127.0.0.1:4000/
	curl -I http://127.0.0.1:4000/blog/
	curl -I http://127.0.0.1:4000/categories/
	curl -I http://127.0.0.1:4000/about/

Resultado esperado: codigo HTTP 200 en paginas existentes.

### 4) Revision manual minima

- Home carga y muestra navegacion.
- Blog lista posts.
- Categories carga correctamente.
- About carga correctamente.
- No hay errores en la consola del navegador.

## Comandos utiles

- Desarrollo:

	  bundle exec jekyll serve --livereload

- Build:

	  bundle exec jekyll build

- Limpiar salida:

	  bundle exec jekyll clean

- Diagnostico:

	  bundle exec jekyll doctor

## Solucion de problemas

### Error de permisos al instalar gems

Evita usar sudo si es posible. Usa un gestor de Ruby (rbenv/asdf) o instala en ruta local con Bundler:

	bundle config set --local path vendor/bundle
	bundle install

### Cambiaste _config.yml y no se refleja

Jekyll no recarga automaticamente _config.yml. Reinicia el servidor:

	Ctrl+C
	bundle exec jekyll serve --livereload

### Puerto 4000 ocupado

Inicia en otro puerto:

	bundle exec jekyll serve --port 4001 --livereload

## Estructura clave del proyecto

- _config.yml: configuracion principal del sitio.
- _posts/: entradas del blog.
- _includes/: fragmentos reutilizables.
- assets/: recursos estaticos.
- _site/: salida generada (no editar manualmente).
