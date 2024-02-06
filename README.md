# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

### Rodando em container Docker

Em todos os casos ha a necessidade de rodar instalação das dependências e build nos stages de CI, devido as tasks de QA e Sonar.

#### OPÇÃO 1 - Podemos instalar as dependências, buildar a aplicação, e após copiamos os aterfatos para uma imagem nginx para rodar o web server.

Gerando imagem:

`
docker build -t demo-nodejs-react:1 -f Dockerfile-Nginx .
`

Subindo o container:

`
docker run -it -p 3000:3000  demo-nodejs-react:1
`

*Neste exemplo a imagem ficou com: 41.7MB*

#### OPÇÃO 2 - Podemos utilizar um Dockerfile multi stage, onde será copiado todo o código para dentro da imagem base node, e após instalado as dependências e buildado a aplicação, copiamos os aterfatos para uma imagem nginx para rodar o web server.

Gerando imagem:

`
docker build -t demo-nodejs-react:2 -f Dockerfile-Multistage-Node-Nginx .
`

Subindo o container:

`
docker run -it -p 3000:3000  demo-nodejs-react:2
`

*Neste exemplo a imagem ficou com: 41.7MB*

#### OPÇÃO 3 - Podemos utilizar um Dockerfile com uma imagem Node, copiar todo código para a imagem, e nela rodamos os comandos de instalação das dependências e o execumos o node diretamente via npm start

Gerando imagem:

`
Usando o NPM
docker build -t demo-nodejs-react:3 -f Dockerfile-Node-npm .

OU YARN

docker build -t demo-nodejs-react:3 -f Dockerfile-Node-yarn .
`

Subindo o container:

`
docker run -it -p 3000:3000  demo-nodejs-react:3
`

*Neste exemplo a imagem ficou com: 466MB*


## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).
