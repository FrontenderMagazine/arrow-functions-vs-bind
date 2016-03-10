ES6 arrow functions are often a compelling alternative to 
`Function.prototype.bind()`.

 
If an extracted method is to work as a callback, you must specify a fixed 
`this`, otherwise it will be invoked as a function (and `this` will be 
`undefined` or the global object). For example:

    obj.on('anEvent', console.log.bind(console))
    

An alternative is to use an arrow function:

    obj.on('anEvent', x => console.log(x))
    

### `this` via parameters {#this-via-parameters}

The following code demonstrates a neat trick: For some methods, you don’t
need`bind()` for a callback, because they let you specify the value of `this`,
via an additional parameter.`filter()` is one such method:

    const as = new Set([1, 2, 3]);
        const bs = new Set([3, 2, 4]);
        const intersection = [...as].filter(bs.has, bs);
            // [2, 3]
    

However, this code is easier to understand if you use an arrow function:

    const as = new Set([1, 2, 3]);
        const bs = new Set([3, 2, 4]);
        const intersection = [...as].filter(a => bs.has(a));
            // [2, 3]
    

### Partial evaluation {#partial-evaluation}

`bind()` enables you to do [*partial evaluation*][1], you can create new
functions by filling in parameters of an existing function:

    function add(x, y) {
            return x + y;
        }
        const plus1 = add.bind(undefined, 1);
    

Again, I find an arrow function easier to understand:

    const plus1 = y => add(1, y);
    

### Further reading {#further-reading}

 [1]: http://www.2ality.com/2011/09/currying-vs-part-eval.html