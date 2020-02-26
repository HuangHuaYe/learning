# getting a type

[helpers](getting%20a%20type/helpers.md)

### isArguments

    function isArguments(value) {
      return isObjectLike(value) && getTag(value) == '[object Arguments]'
    }

### isArrayLike

**function上存在length**

    function isArrayLike(value) {
      return value != null && typeof value !== 'function' && isLength(value.length)
    }

### isBoolean

    function isBoolean(value) {
      return value === true || value === false ||
        (isObjectLike(value) && getTag(value) == '[object Boolean]')
    }

### isPrototype

    function isPrototype(value) {
      const Ctor = value && value.constructor
      const proto = (typeof Ctor === 'function' && Ctor.prototype) || objectProto
    
      return value === proto
    }

### isObject

    function isObject(value) {
      const type = typeof value
      return value != null && (type === 'object' || type === 'function')
    }