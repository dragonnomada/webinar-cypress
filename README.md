# Seminario Web - Pruebas Web Automatizadas y Scraping usando Cypress (Material generado)

En este seminario hemos aprendido cómo usar Cypress.

La documentación oficial puede encontrarse en https://docs.cypress.io/guides/overview/why-cypress.html#In-a-nutshell

1. Instala Node.js desde https://nodejs.org/es/
2. Verifica que en un símbolo del sistema o terminal este instalado `node -v` y `npm -v`.
3. Crea una carpeta y ubícala en la terminal, luego instala cypress con el comando `npm install cypress`.
4. Ejecuta el comando que abre cypress con `npx cypress open`.
5. Se generará una carpeta llamada *cypress* y dentro una carpeta llamada *integrations*.
6. Dentro de la carpeta `my-project/cypress/integrations` coloca un archivo llamado `demo.spec.js`.
7. En el archivo coloca tus conjuntos de pruebas definidos con `describe` y dentro de estos tus pruebas `it`.
8. Usa `cy.visit("https://my-site.com")` para visitar el sitio web.
9. Usa `cy.get("selector-css")` para ubicar un elemento mediante los selectores CSS.
10. Explora a fondo la documentación para interactuar con tu sitio web.

## Presentación

Puedes consultar la presentación en https://slides.com/dragonnomada123/webinar-cypress

## Código de `demo.spec.js`

```js
describe("Conjunto de pruebas", () => {

    it("Prueba 1 - Hola mundo", () => {
        console.log("Hola mundo");
    });

    it("Prueba 2 - Ir a walmart", () => {
        cy.visit("https://www.walmart.com.mx");
    });

    it("Prueba 3 - Recupera la caja de búsqueda y escribe el texto", () => {
        cy.get("input[data-testid='search-bar']").type("Televisión Samsung");
    });

    it("Prueba 4 - Recupera el botón y da clic", () => {
        cy.get("div.search-bar-desktop_searchBarContainer__eBcmI>button[data-automation-id='search-icon']").click();
    });

    // data-automation-id="product-name"
    const products = [];

    it("Prueba 5 - Extrae todos los elementos de los productos", () => {
        cy.get("p[data-automation-id='product-name']").then(elements => {
            for (let elemento of [...elements]) {
                console.log(elemento);

                const elementLink = elemento.parentElement;
                const cardSumma = elementLink.parentElement;
                const productContainer = cardSumma.parentElement;
                
                console.log(elemento.textContent);
                console.log(elementLink.href);
                
                const img = productContainer.querySelector("img");
                
                if (img) {
                    console.log(img.src);
                }

                products.push({
                    name: elemento.textContent,
                    url: elementLink.href,
                    picture: img.src || "http://placehold.it/200"
                });
            }
        });
    });

    it("Prueba 6 - Descargar la info de los productos como JSON", () => {
        // Promise.all(
        //     test1(),
        //     ...
        //     testN(),
        // )

        // fetch("http://mi-empresa.com/data/file.csv", {
        //     products
        // }).then(() => {

        // })

        const blob = new Blob([JSON.stringify(products, null, 2)], { type: "application/json" })
        const url = window.URL.createObjectURL(blob);
        const a = document.createElement("a");
        a.style.display = "none";
        a.href = url;
        // the filename you want
        a.download = `products-${new Date().toISOString().replace(/[\:\.\s]/g, "-")}.json`;
        document.body.appendChild(a);
        a.click();
        window.URL.revokeObjectURL(url);
    });

});
```

## Enlaces

**Selectores CSS W3Schools** - https://www.w3schools.com/css/css_selectors.asp

**Tutorial de Javascript W3Schools** - https://www.w3schools.com/js/default.asp

**Tutorial de HTML W3Schools** - https://www.w3schools.com/html/default.asp

**Cypress.io** - https://www.cypress.io

**Uso de `get` en Cypress** - https://docs.cypress.io/api/commands/get.html#Syntax

**Alternativa a Cypress con Selenium (Soporta Java, Python y C#)** - https://www.selenium.dev/documentation/en/getting_started/

**NPM oficial de Cypress** - https://www.npmjs.com/package/cypress

## Agradecimientos

Gracias por asistir a este seminario web gratuito, si quieres aprender más o contratar un curso manda un correo a dragonnomada123@gmail.com
