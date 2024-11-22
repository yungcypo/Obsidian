# React
[React](https://react.dev/) is a [JavaScript](JavaScript.md) library used for front-end web development  

# Creating new React App
Steps to create a new app in React using [Vite](https://vite.dev/)  

```shell
npm create vite@latest <name>
```

Replace `<name>` with the actual name of your project or just put `.` (dot) here to create it inside current folder  
`npm` will create the app for you  

Go to the folder you created with previous command (if not already)  
```shell
npm install
```

# `npm` Commands
If you check the `package.json` file, you might see available commands in `scripts` section  
By default it's something like this   
```json
"scripts": {
    "dev": "vite --host",
    "build": "tsc -b && vite build",
    "lint": "eslint .",
    "preview": "vite preview",
},
```

So you can `npm run dev` to start the website or `npm run build` to build the website and so on  