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

Run the code
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
