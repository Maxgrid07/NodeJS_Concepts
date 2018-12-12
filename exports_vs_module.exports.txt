NodeJS wraps all code as IIFE (Immediately Invoked Function Expression).

// IIFE Signature
(function(exports, require, module, __filename, __dirname) {

})();

Node does not execute any code you write in a file directly. It executes this wrapper function which will have your code in its body. This is what keeps the top-level variables that are defined in any module scoped to that module.

NOTE: In Javascript, objects are passed around by reference.

1. 'exports' is defined as a reference to 'module.exports'. That means they both points to same memory location.
    - We can use the 'exports' object to export properties, but cannot replace the exports object directly (like below example) because it’s just a reference to module.exports.
    - If we change the whole 'exports' object, it would no longer be a reference to 'module.exports'.

    exports.id = 42 // OK
    exports = { id: 42 }; // NOT OK
    module.exports = { id: 42 } //OK

2. At the end of the file, nodejs basically return 'module.exports' to the 'require' function. This can be viewed as below:

    function(exports, require, module, __filename, __dirname) {
        var module = { exports: {} };
        var exports = module.exports;

        // CODE...

        return module.exports;
    }