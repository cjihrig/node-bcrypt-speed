# bcrypt-speed

Determine the maximum level of rounds for some hardware given the maximum time
that can be spent on login.

Using a fixed amount of time (and thus having an assured user experience) this
module runs a couple of different bcrypt implementations so that the optimum
number of rounds can be found given some hardware and the time that a login
may take (i.e. Apple uses [80ms for unlocking](http://www.darthnull.org/2014/10/06/ios-encryption)).

Note: this package should be run on the target production hardware to get a good
estimate.

The following packages are currently tested:
* [bcrypt-nodejs](https://www.npmjs.org/package/bcrypt-nodejs) (pure js, no deps)
* [twin-bcrypt](https://www.npmjs.org/package/twin-bcrypt) (pure js, no deps, asm.js)
* [bcryptjs](https://www.npmjs.org/package/bcryptjs) (pure js, no deps)
* [bcrypt](https://www.npmjs.org/package/bcrypt) (c++, has deps)
* [bcrypt.wasm](https://www.npmjs.org/package/bcrypt.wasm) (wasm)

Any suggestions on other bcrypt implementations are welcome.

Remember, even [MD4 would be sufficient](https://github.com/freedomofpress/securedrop/issues/180#issuecomment-29760395) when using a strong password, so consider using a [Diceware passphrase](http://world.std.com/~reinhold/diceware.html).

## Usage

    $ node bcrypt-speed.js [maxtime]

A maxtime is optional and defaults to 100ms. This should be the maximum time you
want to let your users wait while you're verifying their password.

## Example

Example run on a 3 GHz core:

    $ node bcrypt-speed.js
    test duration per number of rounds, up to 100ms

    bcrypt-nodejs (pure js, no deps)
    rounds  ms
      4     14
      5      8
      6     12
      7     24
      8     48
      9     91
     10    181

    twin-bcrypt (pure js, no deps, asm.js)
    rounds  ms
      4     22
      5     16
      6     12
      7     23
      8     49
      9     97
     10    194

    bcryptjs (pure js, no deps)
    rounds  ms
      4     29
      5      3
      6      7
      7     12
      8     27
      9     48
     10     99
     11    200

    bcrypt.wasm (wasm)
    rounds  ms
      4      3
      5      3
      6      6
      7     11
      8     22
      9     46
     10     94
     11    177

    bcrypt (c++, has deps)
    rounds  ms
      4      2
      5      3
      6      6
      7     10
      8     20
      9     41
     10     81
     11    164

## Further reading

Discussion about bcrypt, password cracking speed and Diceware passphrases:
* <https://github.com/freedomofpress/securedrop/issues/180#issuecomment-29680658>
* <https://github.com/freedomofpress/securedrop/issues/180#issuecomment-29665663>

## License

ISC

Copyright (c) 2014, 2015 Tim Kuijsten

Permission to use, copy, modify, and/or distribute this software for any
purpose with or without fee is hereby granted, provided that the above
copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
