import React from 'react';
import ReactDOM from 'react-dom';
import Form from '../components/form';

class FormWebComponent extends HTMLElement {
  constructor() {
    super();
  }

  connectedCallback() {
    const mountPoint = document.createElement('div');
    this.attachShadow({ mode: 'open' }).appendChild(mountPoint);
    ReactDOM.render(<Form {...this.attributes} />, mountPoint);
  }
}

customElements.define('my-form', FormWebComponent);
