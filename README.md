# Clopy!

Simple copy-to-clipboard button.

## Installation and Usage

Install the package

```
yarn add clopy
// or
npm install clopy --save
```

Import the clopy element:

```javascript
import Vue from 'vue';
import { Clopy } from 'clopy';

Vue.component('clopy', Clopy);

// Alternatively
import Clopy from 'clopy';

Vue.use(Clopy);
```

Add the element to the HTLM

```html
<clopy input=".some-input">
```

Make sure that the `input` parameter is pointed to the input element you wish to copy from.  
Click the `clopy` icon/button and copy the content of the input!

### Customizing

By default the clopy button has the `clopy-button` class, it can be changed by setting another class to it with the standard `class` attribute, which will then ignore the default class.  
If the default icon does not suit you, just set the `use-icon` attribute to `false` (boolean, so bind it with `:use-icon`) and it will be ignored.


## Credits

Font-awesome (default icon).  
Bootstrap (default button class, slightly modified).  

## License

MIT