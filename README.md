# BitBucket Pipelines

## Actualizar la "patch version" del package.json con un pipeline de BitBucket.
 
* En la raiz del proyecto (a la misma altura que el fichero `package.json`) debemos crear un fichero llamado: `bitbucket-pipelines.yml`.
* El contenido del fichero debe de ser así:
```yml
pipelines:
  branches:
    develop:
      - step:
          name: Increment Patch Version
          script:
            - npm run version
            - git commit ./package.json -m "[skip ci] Patch version has been incremented"
            - git push origin
```
 Fíjate que este pipeline sólo afecta a la rama "develop". Atención: es importante que el mensaje del commit incluya "[skip ci]". 
* Ahora debes añadir en el packaje.json de la aplicación el siguiente script: `"version": "npm --no-git-tag-version version patch"`.
* Pushealo al remoto y ya debería funcionar.