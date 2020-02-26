# helpers

### isObjectLike

注意 `typeof null === 'object'` ,要加上 `value !== null` 的判断.

    
    function isObjectLike(value) {
      return typeof value === 'object' && value !== null
    }

### getTag

注意函数的 `arguments` 进行getTag的时候,返回 '[Object Arguments]', 见下面

    function getTag(value) {
      if (value == null) {
        return value === undefined ? '[object Undefined]' : '[object Null]'
      }
      return toString.call(value)
    }

### isLength

    function isLength(value) {
      return typeof value === 'number' &&
        value > -1 && value % 1 == 0 && value <= MAX_SAFE_INTEGER
    }