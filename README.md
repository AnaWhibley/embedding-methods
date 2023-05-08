# embedding-methods

Given the requirements, the best approach for this implementation would be to use an external library like Webpack Module Federation, which allows for sharing React components between different applications. With Webpack Module Federation, you can host your form application in a separate repository and share it as a remote module with the other applications.

This approach will allow you to achieve the following:

Create a React application that contains a simple form with two fields.
Host this application in a separate repository.
Use Webpack Module Federation to share the form component with other React applications.
Allow other applications to autopopulate the fields based on props provided by the parent application.
All applications will be used internally within an organization, and no third-party hosting is required.
The implementation time for this approach will depend on your familiarity with Webpack and React. However, it can take anywhere from a few days to a few weeks to implement the entire solution from scratch, depending on the complexity of the form and the number of applications you need to integrate with.

Here's an example of how you can use Webpack Module Federation to share the form component between two React applications:

Create a new React application that contains a simple form with two fields, and host it on a separate repository. Let's call this repository "form-app."

Add Webpack Module Federation to your "form-app" project. You can follow the official documentation to set up Webpack Module Federation.

Export your form component as a remote module in your "form-app" project. You can do this by modifying the webpack configuration file to expose the form component as a remote module.

```
// webpack.config.js in form-app project
const { ModuleFederationPlugin } = require('webpack').container;

module.exports = {
  // ...
  plugins: [
    new ModuleFederationPlugin({
      name: 'form',
      filename: 'remoteEntry.js',
      exposes: {
        './Form': './src/Form',
      },
      shared: {
        react: { singleton: true },
        'react-dom': { singleton: true },
      },
    }),
  ],
};

```

In your parent React application, import the remote form component and use it as a regular React component.

```
// index.js in parent application project
import React from 'react';
import { loadRemoteEntry } from 'webpack-micro-frontend/client';
import Form from 'form/Form';

async function init() {
  const formApp = await loadRemoteEntry('http://localhost:3001/remoteEntry.js', 'form');

  const App = () => (
    <div>
      <Form />
    </div>
  );

  ReactDOM.render(<App />, document.getElementById('root'));
}

init();

```

Pass props to the form component to autopopulate the fields based on the data provided by the parent application.

```
// index.js in parent application project
import React from 'react';
import { loadRemoteEntry } from 'webpack-micro-frontend/client';
import Form from 'form/Form';

async function init() {
  const formApp = await loadRemoteEntry('http://localhost:3001/remoteEntry.js', 'form');

  const App = () => (
    <div>
      <Form field1Value="Some value" field2Value="Another value" />
    </div>
  );

  ReactDOM.render(<App />, document.getElementById('root'));
}

init();
```

By using Webpack Module Federation, you can easily share your form component with other React applications without having to publish to NPM or GitHub packages. This approach also provides better performance compared to using iframe, and you can style the form as part of your parent application's CSS.
