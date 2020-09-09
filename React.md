# React

**This** cheat sheet **is NOT complete!**

## PropTypes

```javascript
import PropTypes from 'prop-types';

...

MyComponent.propTypes = {
  optionalBool: PropTypes.array, // All primitives: `array`, `bool`, `func`, `number`, `object`, `string`, `symbol`
  optionalArrayOf: PropTypes.arrayOf(PropTypes.number), // An array of a certain type
  optionalNode: PropTypes.node, // Anything that can be rendered
  optionalElement: PropTypes.element, // A React element
  optionalElementType: PropTypes.elementType, // A React element type
  optionalMessage: PropTypes.instanceOf(Message), // An instance of a class
  optionalObjectOf: PropTypes.objectOf(PropTypes.number), // An object with property values of a certain type
  optionalEnum: PropTypes.oneOf(['One', 'Two']), // An enumeration
  optionalUnion: PropTypes.oneOfType([PropTypes.string, PropTypes.instanceOf(Message)]), // An union
  optionalObjectWithShape: PropTypes.shape({optionalProperty: PropTypes.string, requiredProperty: PropTypes.number.isRequired}), // An object shape
  optionalObjectWithStrictShape: PropTypes.exact({optionalProperty: PropTypes.string, requiredProperty: PropTypes.number.isRequired}), // Exact
  requiredFunc: PropTypes.func.isRequired, // Required prop
  requiredAny: PropTypes.any.isRequired, // A value of any data type
  customProp: function(props, propName, componentName) { ... return new Error (errorMessage);}, // Custom validator
  customArrayProp: PropTypes.arrayOf(function(propValue, key, componentName, location, propFullName) { ... return new Error (errorMessage);}) // A custom validator to `arrayOf` and `objectOf`
}

PropTypes.checkPropTypes(myPropTypes, props, 'prop', 'MyComponent'); // Manual PropTypes check without React
```

## Sources

- [React - Documentation](https://reactjs.org/docs/getting-started.html)
- [PropTypes - Documentation](https://github.com/facebook/prop-types)
