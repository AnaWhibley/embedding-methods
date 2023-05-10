Certainly, here is an example of how you could create a React app using TypeScript and Webpack, with a form component that can be embedded in a parent project that lives in a different repository:

1. Create a new React project with TypeScript:

   ```
   npx create-react-app my-form --template typescript
   ```

2. Install the necessary dependencies:

   ```
   cd my-form
   npm install --save-dev webpack webpack-cli webpack-dev-server ts-loader html-webpack-plugin
   ```

3. Create a new directory named `src/components` and add a new file named `MyForm.tsx` inside it:

   ```tsx
   import React, { useState } from 'react';

   interface FormProps {
     firstName: string;
     lastName: string;
     onSubmit: (firstName: string, lastName: string) => void;
   }

   const MyForm: React.FC<FormProps> = ({ firstName, lastName, onSubmit }) => {
     const [values, setValues] = useState({ firstName, lastName });

     const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
       setValues({ ...values, [e.target.name]: e.target.value });
     };

     const handleSubmit = (e: React.FormEvent<HTMLFormElement>) => {
       e.preventDefault();
       onSubmit(values.firstName, values.lastName);
     };

     return (
       <form onSubmit={handleSubmit}>
         <div>
           <label htmlFor="firstName">First Name:</label>
           <input type="text" name="firstName" value={values.firstName} onChange={handleChange} />
         </div>
         <div>
           <label htmlFor="lastName">Last Name:</label>
           <input type="text" name="lastName" value={values.lastName} onChange={handleChange} />
         </div>
         <button type="submit">Submit</button>
       </form>
     );
   };

   export default MyForm;
   ```

4. Install the `react-web-component` package:

   ```
   npm install --save react-web-component
   ```

5. Update the `MyForm.tsx` file to export a web component:

   ```tsx
   import React, { useState } from 'react';
   import { defineWebComponent } from 'react-web-component';

   interface FormProps {
     firstName: string;
     lastName: string;
     onSubmit: (firstName: string, lastName: string) => void;
   }

   const MyForm: React.FC<FormProps> = ({ firstName, lastName, onSubmit }) => {
     const [values, setValues] = useState({ firstName, lastName });

     const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
       setValues({ ...values, [e.target.name]: e.target.value });
     };

     const handleSubmit = (e: React.FormEvent<HTMLFormElement>) => {
       e.preventDefault();
       onSubmit(values.firstName, values.lastName);
     };

     return (
       <form onSubmit={handleSubmit}>
         <div>
           <label htmlFor="firstName">First Name:</label>
           <input type="text" name="firstName" value={values.firstName} onChange={handleChange} />
         </div>
         <div>
           <label htmlFor="lastName">Last Name:</label>
           <input type="text" name="lastName" value={values.lastName} onChange={handleChange} />
         </div>
         <button type="submit">Submit</button>
       </form>
     );
   };

   defineWebComponent(MyForm, 'my-form');
   ```
6. Create a new directory in the root of your project and name it `src`.
7. Inside the `src` directory, create a new file named `index.tsx`.
8. Open the `index.tsx` file and add the following code:

```tsx
import React from 'react';
import ReactDOM from 'react-dom';
import MyForm from '../components/MyForm';

// Render the MyForm component to the #root element
ReactDOM.render(
  <MyForm />,
  document.getElementById('root')
);
```

9. This code imports the `MyForm` component from the `../components/MyForm` path and renders it to the `#root` element in the HTML file.

10. Save the `index.tsx` file.

At this point, you should have a complete setup for your React application with the `MyForm` component wrapped as a web component and ready to be embedded in other applications.

Sure! After updating the `MyForm.tsx` file to export a web component, here are the next steps:

11. Install the `webpack` and `webpack-cli` packages as dev dependencies using the following command:
   
   ```
   npm install --save-dev webpack webpack-cli
   ```

12. Create a new `webpack.config.js` file in the root of the `my-form` project with the following configuration:

   ```javascript
   const path = require('path');

   module.exports = {
     entry: './src/index.tsx',
     output: {
       filename: 'my-form.js',
       path: path.resolve(__dirname, 'dist'),
       library: 'MyForm',
       libraryTarget: 'umd',
     },
     module: {
       rules: [
         {
           test: /\.(ts|tsx)$/,
           exclude: /node_modules/,
           use: {
             loader: 'ts-loader',
           },
         },
       ],
     },
     resolve: {
       extensions: ['.ts', '.tsx', '.js', '.jsx'],
     },
   };
   ```

   This configuration tells webpack to take the `index.tsx` file in the `src` directory, transpile it using the TypeScript loader, and output the result to a `my-form.js` file in the `dist` directory. The `library` and `libraryTarget` options are used to generate a universal module definition (UMD) that can be used in various environments.

13. Add a new script to the `package.json` file in the `my-form` project to build the web component using webpack:

   ```json
   {
     "name": "my-form",
     "version": "1.0.0",
     "scripts": {
       "build": "webpack --mode production"
     },
     "devDependencies": {
       "@types/react": "^17.0.15",
       "react": "^17.0.2",
       "react-dom": "^17.0.2",
       "ts-loader": "^9.2.6",
       "typescript": "^4.3.5",
       "webpack": "^5.38.1",
       "webpack-cli": "^4.7.2"
     }
   }
   ```

14. Run the following command to build the web component:

   ```
   npm run build
   ```

15. After the build completes, you will find a `my-form.js` file in the `dist` directory of the `my-form` project. You can now include this file in your parent project and use the `my-form` component as a web component.
