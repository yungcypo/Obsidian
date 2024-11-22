# Tailwind CSS
[Tailwind CSS](https://tailwindcss.com/) is a [CSS](./CSS.md) framework, which allows you to style your page using HTML classes  

# Adding Tailwind 
There are steps to add Tailwind to your app  
I will be adding it to React TypeScript app created with Vite  

```shell
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

This will generate `tailwind.config.js`, which you need to edit to look something like this  
```js
/** @type {import('tailwindcss').Config} */  
export default {  
  content: [  
      "./src/**/*.{js,jsx,ts,tsx}"  
  ],  
  theme: {  
    extend: {},  
  },  
  plugins: [],  
}
```

# Changing stuff
You can rename `src/index.css` to something like `tw.css` and edit it like this, just for the start  
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

:root {
	scroll-behavior: smooth;
}
```

It's also recommended to add following to `package.json`
```json
{
	// ...
	"sripts" {
		// ...
		"build-css": "tailwind build -i src/tw.css -o src/index.css"
	}
	// ...
}
```

Every time you change something in `tw.css`, you need to run this command  
```shell
npm run build-css
```

