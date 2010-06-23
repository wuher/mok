mok
===

Simple object mocking for tests.

Mock is created by saying:

>   var mymock = test.mymock(objctToBeMocked);

If 'true' is given as optional parameter, mocking is done recursively.

An example use case might be:

// create mock
var mock = require("mok");
var mymock = mock.mock({foo: function () {}, bar: function () {}});


> // lay out the contract before executing tests

> mymock.expect.foo().times(1).withParameters('hello').returns(true);
> mymock.expect.bar().returns("retval");
> mymock.expect.bar().returns("lavter");
>
> // execute tests
> func_to_be_tested(foo, bar);
> another_func_to_be_tested(bar);
>
> // verify the contract
> mock.releaseMocks();

The releaseMocks() function permorms the checks that all the right
functions were called as many times as they were supposed to. Note that
the number of times to be called may either be set explicitly using
times() or the mock module may determine it by counting the
withParameters() and returns() calls.

mock.expect has following functions:

* times():0 means that mocked function can't be invoked
* withParameters(): the code under test should invoke the mocked
  function with these parameters
* returns(): define what the mocked function returns back
  to the code under test
