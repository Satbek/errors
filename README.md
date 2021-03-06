# Convenient error handling in tarantool
[![Build Status][travis-badge]][travis-url]
[![Code Coverage][coverage-badge]][coverage-url]

Because Lua code deserves better error handling. This module helps you
understand what code path lead to creation of a particular exception
object.

## Example

```lua
local errors = require 'errors'

local WTF = errors.new_class("WhataTerribleFailure")

local function foo()
    local failure_condition = true
    local result = "bar"

    if failure_condition then
        return nil, WTF:new("failure_condition is true")
    end

    return result
end

local res, err = foo()

if err ~= nil then
    print(err)
end
```

This code will print:

```lua
WhataTerribleFailure: failure_condition is true
stack traceback:
    test.lua:10: in function 'foo'
    test.lua:16: in main chunk
```

See that you have an exception type, message and traceback recorded
inside the exception object. It can be converted to string using the
`tostring()` function.

[travis-badge]: https://api.travis-ci.org/Satbek/errors.svg?branch=master
[travis-url]: https://travis-ci.org/Satbek/errors
[coverage-badge]: https://coveralls.io/repos/github/Satbek/errors/badge.svg?branch=master
[coverage-url]: https://coveralls.io/github/Satbek/errors
