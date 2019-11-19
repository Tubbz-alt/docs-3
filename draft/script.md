# Script

```text
module Script

scalar ScriptID

tx StoreWASM(wasm bytes) ScriptID

tx CreateContract(script ScriptID, msg bytes, assets bank.Asset*) Address

tx SendContract(contract Address, msg bytes, assets bank.Asset*)
```

