# WasmEdge-pickledb-rs
A lightweight and simple key-value store.

Get the code
```
cd /home/tpmccallum/testing_data_storage_in_wasmedge/pickledb-rs
git clone https://github.com/second-state/WasmEdge-pickledb-rs.git
```

Build the code
```
cd /home/tpmccallum/testing_data_storage_in_wasmedge/pickledb-rs/WasmEdge-pickledb-rs
rustwasmc build
```

Create Node js file to run the code

```
vi pickle.js
```

Then add this to pickle.js
```
// Create ssvm instance
const ssvm = require("wasmedge-extensions");

// Use this first time (initial call)
const path = "/home/tpmccallum/testing_data_storage_in_wasmedge/pickledb-rs/WasmEdge-pickledb-rs/pkg/wasmedge_pickledb_rs_bg.wasm";
vm = new ssvm.VM(path, { args:process.argv, env:process.env, preopens:{"/": "/tmp"} });

// AOT path
aot_path = "/home/tpmccallum/wasmedge_pickledb_rs_bg.so"

// If you want to, please go ahead and make an aot file
vm.Compile(aot_path);

// Use this after the first time (subsequent calls)
var vm_aot = new ssvm.VM(aot_path, { EnableAOT:true, rgs:process.argv, env:process.env, preopens:{"/": "/tmp"} });

// Run function
var first_result = vm_aot.RunString("first");

console.log("First result: " + first_result);
```

Run the Node file

Please note: The following is not the intended output, in the very near future pickledb's writing to file will be updated to write to RocksDB.
```
tpmccallum@tpmccallum:/media/nvme/node_rpc/wasm-joey/src/testing_using_node$ node pickle.js 
[2021-09-29 16:04:28.843] [info] compile start
[2021-09-29 16:04:28.921] [info] verify start
[2021-09-29 16:04:28.988] [info] optimize start
[2021-09-29 16:04:35.781] [info] codegen start
[2021-09-29 16:04:41.484] [info] compile done ...
// snip //
... more to come 

```
